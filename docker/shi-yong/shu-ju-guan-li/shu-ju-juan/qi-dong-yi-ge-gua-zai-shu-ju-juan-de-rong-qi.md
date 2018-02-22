# 启动一个挂载数据卷的容器

在用`docker run`命令的时候，使用`--mount`标记来将`数据卷`挂载到容器里。在一次`docker run`中可以挂载多个`数据卷`。

```
$ docker run -d -P \
    --name web \
    # -v /src/webapp:/opt/webapp \
    --mount type=bind,source=/src/webapp,target=/opt/webapp \
    training/webapp \
    python app.py
```

上面的命令加载主机的`/src/webapp`目录到容器的`/opt/webapp`目录。这个功能在进行测试的时候十分方便，比如用户可以放置一些程序到本地目录中，来查看容器是否正常工作。本地目录的路径必须是绝对路径，以前使用`-v`参数时如果本地目录不存在 Docker 会自动为你创建一个文件夹，现在使用`--mount`参数时如果本地目录不存在，Docker 会报错。

Docker 挂载主机目录的默认权限是`读写`，用户也可以通过增加`readonly`指定为`只读`。

```
$ docker run -d -P \
    --name web \
    # -v /src/webapp:/opt/webapp:ro \
    --mount type=bind,source=/src/webapp,target=/opt/webapp,readonly \
    training/webapp \
    python app.py
```

### 挂载一个本地主机文件作为数据卷 {#挂载一个本地主机文件作为数据卷}

`--mount`标记也可以从主机挂载单个文件到容器中

```
$ docker run --rm -it \
   # -v $HOME/.bash_history:/root/.bash_history \
   --mount type=bind,source=$HOME/.bash_history,target=/root/.bash_history \
   ubuntu:17.10 \
   bash

root@2affd44b4667:/# history
1  ls
2  diskutil list
```

这样就可以记录在容器输入过的命令了。

