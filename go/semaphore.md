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

## Set max workers based on CPU capacity

```
func main() {
	var ctx = context.Background()
	var wg sync.WaitGroup

	maxWorkers := runtime.GOMAXPROCS(0)
	sem := semaphore.NewWeighted(int64(maxWorkers))
	for i := 0; i < 10; i++ {
		wg.Add(1)
		go func(id int) {
			defer wg.Done()

			if err := sem.Acquire(ctx, 1); err != nil {
				fmt.Println(err)
				return
			}
			defer sem.Release(1)

			fmt.Printf("Goroutine %d is running\n", id)
			time.Sleep(1 * time.Second)
		}(i)
	}
	wg.Wait()
	fmt.Println("finished")
}
```

