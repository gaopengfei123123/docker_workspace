### 作用:

在本地一键搭建zookeeper集群测试环境, 顺便带一个web页面方便查看

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