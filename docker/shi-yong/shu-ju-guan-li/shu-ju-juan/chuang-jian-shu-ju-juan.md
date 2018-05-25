# 创建数据卷

```text
$ docker volume create my-vol
```

查看所有的`数据卷`

```text
$ docker volume ls
local    my-vol
```

在主机里使用以下命令可以查看指定`数据卷`的信息

```text
$ docker volume inspect my-vol
[
    {
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/my-vol/_data",
        "Name": "my-vol",
        "Options": {},
        "Scope": "local"
    }
]
```

