# redigo sample code 

```
package main

import (
	"fmt"
	"log"
	"slices"
	"time"

	"github.com/garyburd/redigo/redis"
)

var pool *redis.Pool

func main() {
	pool = &redis.Pool{
		MaxIdle:     3,
		MaxActive:   20,
		IdleTimeout: 240 * time.Second,
		Dial:        func() (redis.Conn, error) { return redis.Dial("tcp", ":6379") },
	}
	if err := HealthCheck(); err != nil {
		log.Println(err)
		return
	}

	conn := pool.Get()
	defer conn.Close()

	newIDs := []int{1, 2, 3, 4, 5}
	if err := updateRedisSetMembers(newIDs); err != nil {
		log.Println(err)
		return
	}
	fmt.Println(getRedisSetMembers())
}

func HealthCheck() error {
	conn := pool.Get()
	defer conn.Close()

	if _, err := conn.Do("PING"); err != nil {
		return err
	}
	return nil
}

var key = "key"

func getRedisSetMembers() ([]int, error) {
	conn, err := pool.Dial()
	if err != nil {
		return nil, err
	}
	defer conn.Close()
	return redis.Ints(conn.Do("SMEMBERS", key))
}

func updateRedisSetMembers(targetIDs []int) error {
	conn, err := pool.Dial()
	if err != nil {
		return err
	}
	defer conn.Close()

	currentTargetIDs, err := getRedisSetMembers()
	if err != nil {
		return err
	}
	var (
		insertTargetIDs []int
		deleteTargetIDs []int
	)
	for _, targetID := range targetIDs {
		if !slices.Contains(currentTargetIDs, targetID) {
			insertTargetIDs = append(insertTargetIDs, targetID)
		}
	}
	for _, targetID := range currentTargetIDs {
		if !slices.Contains(targetIDs, targetID) {
			deleteTargetIDs = append(deleteTargetIDs, targetID)
		}
	}

	// transactionを貼る
	if err := conn.Send("MULTI"); err != nil {
		return err
	}

	if len(insertTargetIDs) > 0 {
		if err := conn.Send("SADD", formatRedisCommandArgs(insertTargetIDs)...); err != nil {
			return err
		}
	}
	if len(deleteTargetIDs) > 0 {
		if err := conn.Send("SREM", formatRedisCommandArgs(deleteTargetIDs)...); err != nil {
			return err
		}
	}

	// transactionを実行
	if _, err := conn.Do("EXEC"); err != nil {
		return err
	}
	return nil
}

func formatRedisCommandArgs(targetIDs []int) []any {
	var result []any = []any{key}
	for _, targetID := range targetIDs {
		result = append(result, targetID)
	}
	return result
}
```
