# 其他构建方式

## 直接用 Git repo 进行构建 {#直接用-git-repo-进行构建}

或许你已经注意到了，`docker build`还支持从 URL 构建，比如可以直接从 Git repo 中构建：

```text
$ docker build https://github.com/twang2218/gitlab-ce-zh.git#:8.14
docker build https://github.com/twang2218/gitlab-ce-zh.git\#:8.14
Sending build context to Docker daemon 2.048 kB
Step 1 : FROM gitlab/gitlab-ce:8.14.0-ce.0
8.14.0-ce.0: Pulling from gitlab/gitlab-ce
aed15891ba52: Already exists
773ae8583d14: Already exists
...
```

这行命令指定了构建所需的 Git repo，并且指定默认的`master`分支，构建目录为`/8.14/`，然后 Docker 就会自己去`git clone`这个项目、切换到指定分支、并进入到指定目录后开始构建。

## 用给定的 tar 压缩包构建 {#用给定的-tar-压缩包构建}

```text
$ docker build http://server/context.tar.gz
```

如果所给出的 URL 不是个 Git repo，而是个`tar`压缩包，那么 Docker 引擎会下载这个包，并自动解压缩，以其作为上下文，开始构建。

## 从标准输入中读取 Dockerfile 进行构建 {#从标准输入中读取-dockerfile-进行构建}

```text
docker build - < Dockerfile
```

或

```text
cat Dockerfile | docker build -
```

如果标准输入传入的是文本文件，则将其视为`Dockerfile`，并开始构建。这种形式由于直接从标准输入中读取 Dockerfile 的内容，它没有上下文，因此不可以像其他方法那样可以将本地文件`COPY`进镜像之类的事情。

## 从标准输入中读取上下文压缩包进行构建 {#从标准输入中读取上下文压缩包进行构建}

```text
$ docker build - < context.tar.gz
```

如果发现标准输入的文件格式是`gzip`、`bzip2`以及`xz`的话，将会使其为上下文压缩包，直接将其展开，将里面视为上下文，并开始构建。

