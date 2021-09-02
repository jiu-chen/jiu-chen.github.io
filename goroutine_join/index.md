# go main函数等待所有goroutine结束

在go中，main函数不会主动阻塞等待协程函数执行结束，类似默认调用了 C 中的 detach() 函数
```go
package main

import (
	"fmt"
	"time"
)

func main() {
	for i := 0; i < 10; i++ {
		go func(i int) {
			time.Sleep(1 * time.Second)
			fmt.Println(i)
		}(i)
	}
	fmt.Println("main exit")
}
```
结果只会在控制台输出: main exit  \

而想要实现类 C 语言中的 join() 函数, 通常有两种办法。
一种是通过channel进行同步
```go
package main

import (
	"fmt"
	"time"
)

func main() {
	ch := make(chan int, 2)

	go func() {
		for i := 0; i < 10; i++ {
			time.Sleep(1 * time.Second)
			fmt.Println("go routine1", i)
		}
		ch <- 1
	}()
	go func() {
		for i := 0; i < 10; i++ {
			time.Sleep(1 * time.Second)
			fmt.Println("go routine2", i)
		}
		ch <- 2
	}()

	// 等待
	for i := 0; i < 2; i++ {
		<-ch
	}

	fmt.Println("main exist")
}
```
这种方法需要知道子 goroutine 的个数  
另一种办法是用 sync.WaitGroup，这种方法不需要知道 gotoutine 的个数
```go
package main

import (
	"fmt"
	"sync"
	"time"
)

func main() {
	var wg sync.WaitGroup

	for i := 0; i < 10; i++ {
		wg.Add(1)
		go func(i int) {
			defer wg.Done()
			time.Sleep(1 * time.Second)
			fmt.Println(i)
		}(i)
	}

	wg.Wait() // 等待

	fmt.Println("main exist")
}

```
推荐使用第二种写法，比较灵活;
