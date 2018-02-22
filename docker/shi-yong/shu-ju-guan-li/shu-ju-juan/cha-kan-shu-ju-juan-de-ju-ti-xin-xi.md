在主机里使用以下命令可以查看`web`容器的信息

```
$ docker inspect web
```

`数据卷`信息在 "Mounts" Key 下面

```
"Mounts": [
    {
        "Type": "volume",
        "Name": "my-vol",
        "Source": "/var/lib/docker/volumes/my-vol/_data",
        "Destination": "/app",
        "Driver": "local",
        "Mode": "",
        "RW": true,
        "Propagation": ""
    }
],
```



