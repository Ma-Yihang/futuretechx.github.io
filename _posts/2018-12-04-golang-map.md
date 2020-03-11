## map的定义
- 简单形式：map[K]V
- 嵌套形式：map[K1]map[K2]V K1是外层的key，value又是一个map,这个map的key是K1,vaule是V
- 比如一个例子：
```go
m:=map[string]string {
  "name":"featuretechx",
  "study":"golang",
  "site":"shanghai"
}

//其他定义形式：
m2:=make(map[string]int)   //m2==empty map

var m3 map[string]int //m3==nil


// map的遍历：
for k,v:=range m {
    fmt.Println(k,v)
}

// key 在map中是无序的。如取key中没有的下标，不会报错。会返回一个空的字符串。比如

causeName:=m["cause"]
fmt.Println(causeName) //打印空字符串

// 如何判断一个key对于的value是否存在
if causeName,ok:=m["cause"];ok{
    fmt.Println(causeNmae)
}else{
    fmt.Println("key does not exist!!!") //不存在ok为false 
}

//删除一个元素
delete(m,"name")
```
