# Go进阶之服务发现
## 客户端发现
一个服务实例被启动时，它的网络地址会被写到注册表上；当服务实例终止时，再从注册表中删除；这个服务实例的注册表通过心跳机制动态刷新；客户端使用一个负载均衡算法，去选择一个可用的服务实例，来响应这个请求。
![image](https://user-images.githubusercontent.com/34125846/114561528-36061200-9ca0-11eb-8c17-594f1eaaaee6.png)
## 服务端发现
客户端通过负载均衡器向一个服务发送请求，这个负载均衡器会查询服务注册表，并将请求路由到可用的服务实例上。服务实例在服务注册表上被注册和注销(Consul Template+Nginx，kubernetes+etcd)。
![image](https://user-images.githubusercontent.com/34125846/114561643-533ae080-9ca0-11eb-9fe2-dfd8fd56c9be.png)

