# 如何使用golang创建一个简单的http 服务器和客户端



## http服务器

创建一个http服务器很简单，在golang中只需要几步：
- 创建路由器
- 设置路由规则
- 设置服务器
- 监听端口并提供服务

代码如下
```go
package main

import (
	"log"
	"net/http"
	"time"
)

const (
	Addr = ":1234"
)

func main() {
	//创建路由器
	mux := http.NewServeMux()
	//设置路由规则
	mux.HandleFunc("demo", helloWorld)
	//创建服务器
	server := &http.Server{
		Addr:         Addr,
		WriteTimeout: time.Second * 3,
		Handler:      mux,
	}

	//监听端口并提供服务
	log.Println("Starting httpserver at " + Addr)
	log.Fatal(server.ListenAndServe())
}

func helloWorld(w http.ResponseWriter, r *http.Request) {
	time.Sleep(1 * time.Second)
	w.Write([]byte("Hello,World!!!"))
}
```
```bash
 % curl -v "http://127.0.0.1:1234/demo"
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 1234 (#0)
> GET /demo HTTP/1.1
> Host: 127.0.0.1:1234
> User-Agent: curl/7.58.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Date: Sat, 21 Nov 2020 12:12:35 GMT
< Content-Length: 14
< Content-Type: text/plain; charset=utf-8
<
* Connection #0 to host 127.0.0.1 left intact
Hello,World!!!%
```
## Client
这次不通过curl，自己写一个client链接服务器：
- 创建连接池
- 创建客户端
- 请求数据
- 读取内容
代码如下：
```go
package main

import (
	"fmt"
	"io/ioutil"
	"log"
	"net"
	"net/http"
	"time"
)

func main() {
	transport := &http.Transport{
		DialContext: (&net.Dialer{
			Timeout:   30 * time.Second,
			KeepAlive: 30 * time.Second,
			DualStack: true,
		}).DialContext,
		MaxIdleConns:          100,
		IdleConnTimeout:       90 * time.Second,
		TLSHandshakeTimeout:   10 * time.Second,
		ExpectContinueTimeout: 1 * time.Second,
	}
	// 创建客户端
	client := &http.Client{
		Timeout:   time.Second * 30,
		Transport: transport,
	}
	//请求数据
	resp, err := client.Get("http://127.0.0.1:1234/demo")
	if err != nil {
		log.Fatal(err)
	}
	defer resp.Body.Close()
	//读取内容
	bds, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(string(bds))
	fmt.Println("vim-go")
}
```

```bash
 % go run main.go
Hello,World!!!
vim-go
```
