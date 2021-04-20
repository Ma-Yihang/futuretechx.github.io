# 每日一练：
## 实现两个Goroutine通信，要求如下：
- （a）实现ping-pong效果
- （b）在第三个Goroutine中查找前两个Goroutine各自发送了多少消息，并可随时设置各自ping-pong的频率
- （c）保证程序能任意长时间运行，且收到ctrl+c信号后，全身而退（即保证各个Goroutine完整退出）

```go
package main


import (
    "fmt"
    "os"
    "time"
	"context"
	"log"
	"os/signal"
)


// The pinger prints a ping and waits for a pong
func pinger(ctx context.Context, pinger chan int, ponger chan int) {

	<-ctx.Done()
	log.Println("exit pinger")
	_, cancel := context.WithTimeout(context.Background(), 10*time.Second)
	defer cancel()

    for {
        <-pinger
        fmt.Println("ping")
        time.Sleep(500 * time.Millisecond)
        ponger <-  1
    }
}


// The ponger prints a pong and waits for a ping
func ponger(ctx context.Context, pinger chan int, ponger chan int) {

	<-ctx.Done()
	log.Println("exit ponger")
	_, cancel := context.WithTimeout(context.Background(), 10*time.Second)
	defer cancel()

    for {

        <-ponger
        fmt.Println("pong")
        time.Sleep(200 * time.Millisecond)
        pinger <- 1
    }
}

func contalSendRateLimit(){

}

var ctx, cancelFunc = context.WithCancel(context.Background())

func SetupCloseHandler() {
	//register Interrupt signal
	signalChan := make(chan os.Signal, 1)
	signal.Notify(signalChan, os.Interrupt)
	go func() {
		signal := <-signalChan
		log.Printf("Received %v", signal)
		cancelFunc()
		// os.Exit(0)
	}()
}

func main() {

	// wg := sync.WaitGroup{}
	SetupCloseHandler()
    ping := make(chan int)
    pong := make(chan int)

    go pinger(ctx,ping, pong)
    go ponger(ctx,ping, pong)


    // The main goroutine starts the ping/ping by sending into the ping channel
    ping <- 1
	for {
		time.Sleep(5 * time.Second)
	}
    // os.Exit(0)
}

```
