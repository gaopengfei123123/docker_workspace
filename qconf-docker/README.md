### 作用:

在本地一键搭建zookeeper集群测试环境, 顺便带一个web页面方便查看

使用qconf链接环境

启动:

```bash
docker-compose up
```

账户配置参考

```yml
services:
  zoo-web:
    image: tobilg/zookeeper-webui
    container_name: zk-web
    ports:
      - "8080:8080"
    networks:
      - frontend
    environment:
      ZK_DEFAULT_NODE: zk1:2181
      USER: admin
      PASSWORD: 123123
      HTTP_PORT: 8080
    depends_on: 
      - zoo1
```

web容器默认绑定本地`8080`端口, 访问指定server, 则使用容器名, 例如 `zk1:2181`, `zk2:2181`

在宿主机访问时, 因为已经绑定了宿主机端口, 使用 `2181`,`2182`,`2183`就行


查看qconf是否成功启动
```
$ docker exec -it qconf-docker_qconf_1 /usr/local/qconf/bin/qconf get_conf zookeeper/config

server.1=qconf_zk1:2888:3888:participant;0.0.0.0:2181
server.2=qconf_zk2:2888:3888:participant;0.0.0.0:2181
server.3=qconf_zk3:2888:3888:participant;0.0.0.0:2181
version=0
```

不得不说, qconf就是一个zookeeper的优化版客户端, 当然也更吃内存