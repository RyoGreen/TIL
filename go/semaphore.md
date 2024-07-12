# how to use the Semaphore

```
package main

import (
	"context"
	"fmt"
	"time"

	"golang.org/x/sync/semaphore"
)

var s = semaphore.NewWeighted(2)

func process(ctx context.Context) {
	if err := s.Acquire(ctx, 1); err != nil {
		fmt.Println(err)
		return
	}
	defer s.Release(1)
	fmt.Println("Start...")
	time.Sleep(1 * time.Second)
	fmt.Println("Finish")
}

func main() {
	ctx := context.Background()
	go process(ctx)
	go process(ctx)
	go process(ctx)
	time.Sleep(5 * time.Second)
}

```