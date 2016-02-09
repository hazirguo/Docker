本文描述如何在 Ubuntu 14.04 上安装 Docker。

## 前提条件

### Ubuntu 版本要求

Docker 只能安装在 64 位系统上，而且 Linux 内核版本至少是 3.10 及以上。而我的使用的 Ubuntu 版本均满足这两个条件：

```
guohl@linux:~$ uname -a
Linux linux 3.13.0-24-generic #46-Ubuntu SMP Thu Apr 10 19:08:14 UTC 2014 i686 i686 i686 GNU/Linux
```

*可选*：建议安装 `linux-image-extra` 内核包，该包允许你使用 `aufs` 存储驱动。使用下面命令来安装：

```
$ sudo apt-get update
$ sudo apt-get install linux-image-extra-$(uname -r)
```

### 更新 apt 源

Docker 的 apt 库包含了 Docker 1.7.1 以及更高版本：

1. 增加新的 `gpg` key：

    ```
    $ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    ```

2. 打开 `/etc/apt/sources.list.d/docker.list` 文件，对 Ubuntu 14.04 系统而言，向该文件写入：

    ```
    deb https://apt.dockerproject.org/repo ubuntu-trusty main
    ```

3. 保存关闭之后，更新 apt 包索引：

    ```
    $ sudo apt-get update
    ```

4. 如果存在旧的版本移除：

    ```
    $ sudo apt-get purge lxc-docker
    ```

5. 验证 `apt` 命令从正确的库中获取：

    ```
    $ sudo apt-cache policy docker-engine
    ```

## 安装 Docker

确保安装前提已经完成之后，可以通过下面的步骤来安装 Docker：

1. 安装 Docker

    ```
    $ sudo apt-get install docker-engine
    ```

2. 启动 Docker 守护进程：

   ```
   $ sudo service docker start
   ```

3. 验证 Docker 是否安装成功：

   ```
   $ sudo docker run hello-world
   ```

   这个命令会下载一个测试镜像，并且在容器中运行，当这个容器运行时，将会打印出提示信息，然后退出。

# 更新 Docker

使用 `apt-get` 更新 Docker 到最新版：

```
$ sudo apt-get install docker-engine
```

# 卸载

如果卸载 Docker 安装包：

```
$ sudo apt-get purge docker-engine
```

如果卸载 Docker 包及其依赖包：

```
$ sudo apt-get autoremove --purge docker-engine
```

上面的命令不会删除镜像、容器、卷等数据，如果你想移除这些，运行下面的命令：

```
$ sudo rm -rf /var/lib/docker
```
