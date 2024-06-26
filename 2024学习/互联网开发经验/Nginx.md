

# 什么是Nginx

是一款轻量级的Web服务器、反向代理服务器及电子邮件代理服务器

## 反向代理

（正向）代理：客户端隐藏自己的IP/端口，以此来保护自己或者访问原来不能访问的网络

反向代理：服务端隐藏真实IP、端口，只把处理结果返回，对外只暴露代理服务器的ip和端口

### 2. 在 CentOS/RHEL 上安装 Nginx

1. **安装 EPEL 仓库:**

   ```
   bash
   复制代码
   sudo yum install epel-release
   ```

2. **安装 Nginx:**

   ```
   bash
   复制代码
   sudo yum install nginx
   ```

3. **启动 Nginx 并设置开机自启动:**

   ```
   bash复制代码sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

4. **检查 Nginx 状态:**

   ```
   bash
   复制代码
   sudo systemctl status nginx
   ```

nginx -t 

nginx -s reload

~~~conf
#指定用户
user root;
#指定线程数 核心数的两倍 我的阿里云服务器核心是2
worker_processes 4;

~~~

