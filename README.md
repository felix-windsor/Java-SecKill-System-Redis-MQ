1、启动前，请配置 application.properties 中相关redis、mysql、rabbitmq（需要提前创建好队列，队列名称：seckill.queue）地址。

2、登录地址：[http://localhost:8888/page/login](http://localhost:8888/page/login)

3、商品秒杀列表地址：[http://localhost:8888/goods/list](http://localhost:8888/goods/list)

### 先把 Docker Desktop 启动起来

### Redis 配置
```
docker run -d --name redis-server -p 6379:6379 redis
```
### RabbitMQ 配置

#### 用Docker把RabbitMQ启动起来;
输入如下命令行：
```
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin -e RABBITMQ_DEFAULT_VHOST=/ rabbitmq:3-management
```
删除 RabbitMQ 命令行
```
docker rm -f rabbitmq
```

#### 进入以下网址
```
http://localhost:15672
```
先登录进去
用户名和密码都是 admin
选择 Queues and Streams
![[Pasted image 20251212115447.png]]
队列配置
- Virtual host 选择 / （与应用一致）
- Type 选 Classic
- Name 填写 seckill.queue
- Durability 选 Durable
- Auto delete 选 No
- Arguments 留空即可（不需要 TTL、DLX 等高级参数）

### 后端启动命令
```
mvn spring-boot:run
```

### 登录
手机号
```
18077200000
```
密码
```
123456
```


