# learning-envoy

Envoy is the implementation of Istio's data plane. It is currently very popular, but the threshold for learning it is very high. I hope to help those who want to learn it by recording some of its learning process.


## 概念

- Listener: 监听器（listener）是服务(程序)监听者，就是真正干活的。 它是可以由下游客户端连接的命名网络位置（例如，端口、unix域套接字等）。Envoy 公开一个或多个下游主机连接的侦听器。一般是每台主机运行一个 Envoy，使用单进程运行，但是每个进程中可以启动任意数量的 Listener（监听器），目前只监听 TCP，每个监听器都独立配置一定数量的（L3/L4）网络过滤器。Listenter 也可以通过 Listener Discovery Service（LDS）动态获取。

- Listener filter : Listener 使用 listener filter（监听器过滤器）来操作链接的元数据。它的作用是在不更改 Envoy 的核心功能的情况下添加更多的集成功能。Listener filter 的 API 相对简单，因为这些过滤器最终是在新接受的套接字上运行。在链中可以互相衔接以支持更复杂的场景，例如调用速率限制。Envoy 已经包含了多个监听器过滤器。

- Http Route Table: HTTP 的路由规则，例如请求的域名，Path 符合什么规则，转发给哪个 Cluster。

- Cluster : 集群（cluster）是 Envoy 连接到的一组逻辑上相似的上游主机，类似Kubernetes 中的一个 Service 。Envoy 通过服务发现发现集群中的成员。Envoy 可以通过主动运行状况检查来确定集群成员的健康状况。Envoy 如何将请求路由到集群成员由负载均衡策略确定。

- endpoint : 一个具体的“应用实例”，对应 ip 和端口号，类似 Kubernetes 中的一个 Pod。





