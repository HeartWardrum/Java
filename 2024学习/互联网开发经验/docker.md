https://www.bilibili.com/video/BV1Zn4y1X7AZ?p=11&spm_id_from=pageDriver&vd_source=60de449f23a9496cd95f00798d033502

# Docker

## 什么是Docker

Docker是一个应用打包、分发、部署的工具

可以将它理解为一个轻量的虚拟机，它只虚拟你软件需要的运行环境，多余的一点不要。

而普通的虚拟机则是一个完整而庞大的系统，包含各种不管你要不要的软件。

## 比起虚拟机，Docker的优势

- 支持的系统非常多，各类的windows和Linux都支持。
- 性能好，只虚拟软件所需运行环境，最大化减少没用的配置。
- 一个命令就能自动部署好所需环境
- 稳定性好，不同系统都一样的部署方式

## 打包、分发、部署

打包：把软件所需的依赖、第三方库、软件打包到一起，变成一个安装包

分发：你可以把你打包好的“安装包”上传到一个镜像仓库，其他人可以非常方便的获取和安装

部署：拿着“安装包”，一个命令便可以运行起来你的应用，自动模拟出一模一样的运行环境，不管是在windows/mac/Linux

##  镜像/容器

镜像类似一个Java类

容器就是一个实例化对象

## 常用命令

以操作nginx为例

### 下载镜像：

docker search 检索

docker pull 下载

docker images 列表

docker rmi  删除

~~~shell
docker search nginx
docker pull nginx:版本号
docker images 查看镜像列表
~~~



### 启动容器

docker run 运行

docker ps 查看

docker start 启动

docker restart 重启

docker stats 状态

docker logs 日志

docker exec 进入

docker rm 删除  docker rm -f 容器id  可以强制删除启动着的容器

~~~shell
docker run nginx #控制台会阻死
ctrl + c 关闭nginx容器
docker ps -a 查看所有启动与未启动的容器
找到容器id后
docker start 容器id
~~~

~~~shell
docker run -d --name mynginx -p 88:80 nginx
-d表示后台启动， --name 后面加自定义的名字 -p表示端口映射，将宿主机的88端口映射到该nginx容器的80端口
~~~



`docker exec -it mynginx /bin/bash` 是一条用于在运行中的Docker容器中启动一个交互式终端的命令。具体来说，这条命令的作用是进入名为 `mynginx` 的容器，并在其中启动一个 Bash shell，从而允许你在该容器内交互式地执行命令。

### 命令解析
- `docker exec`：这是Docker命令，用于在运行中的容器内执行新命令。
- `-i`：表示交互模式（interactive）。保持STDIN打开，以便你可以在容器中输入命令。
- `-t`：为创建的终端分配一个伪终端（pseudo-TTY）。这使得终端行为更像一个真正的终端，适合运行交互式命令行应用。
- `mynginx`：这是容器的名称或ID。你需要替换成你实际容器的名称或ID。
- `/bin/bash`：这是在容器中执行的命令。在这种情况下，它启动了Bash shell。

### 使用示例
假设你已经有一个名为 `mynginx` 的nginx容器在运行，可以使用以下步骤进入容器：

1. **查看正在运行的容器**：
   ```sh
   docker ps
   ```

   输出示例：
   ```sh
   CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
   d4c5fcd4b983        nginx               "nginx -g 'daemon of…"   2 minutes ago       Up 2 minutes        0.0.0.0:80->80/tcp     mynginx
   ```

2. **进入容器**：
   ```sh
   docker exec -it mynginx /bin/bash
   ```

   这会在容器内启动一个Bash shell，你可以在其中执行各种命令，如查看nginx配置文件、检查日志等。

### 示例场景
假设你需要在 `mynginx` 容器中查看nginx配置文件，可以按如下步骤操作：

1. **进入容器**：
   ```sh
   docker exec -it mynginx /bin/bash
   ```

2. **在容器内查看nginx配置文件**：
   ```sh
   cat /etc/nginx/nginx.conf
   ```

3. **在容器内退出Bash shell**：
   在Bash shell中输入 `exit` 退出容器的终端会话。

### 总结
`docker exec -it mynginx /bin/bash` 是一个非常有用的命令，可以让你进入运行中的Docker容器进行交互式操作。这对于调试、查看配置文件、检查日志以及执行其他命令行操作非常方便。

### 保存镜像

docker commit 提交

docker save 保存

docker load 加载

~~~shell
docker commit -m "update index.html" mynginx mynginx:v1.0

docker images

docker save -o mynginx.tar mynginx:v1.0

然后可以将这个tar包拿到各个地方

docker load -i mygninx.tar 可以将tar包变成镜像

docker run -d --name app01 -p 80:80 mynginx:v1.0 启动镜像
~~~

### 分享社区

docker login 

docker 
