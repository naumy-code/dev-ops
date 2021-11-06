# Portainer管理多台Docker容器环境

## 1.环境准备

![image-20211106112952384](https://wywtypora.oss-cn-shanghai.aliyuncs.com/image/image-20211106112952384.png)

```bash
# aliyun 2核8G
139.196.95.123  安装docker和Portainer
# aliyun 1核2G 
47.100.34.199   安装docker
# qingcloud 1核2G
139.198.167.214 安装docker
```

## 2.管理docker

### 2.1安装运行portaner

在aliyun 2核8G的服务器上安装portaner

```bash
# 安装portainer
docker pull portainer/portainer
# 启动portainer
docker run -d -p 8080:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --name prtainer  portainer/portainer

systemctl daemon-reload
139.198.167.214:2375
```

### 2.2修改配置文件

3台机器上都修改 <font color=green>**/usr/lib/systemd/system/docker.service**</font>

```bash
# 修改配置文件
vim /usr/lib/systemd/system/docker.service
# 添加配置文件内容
ExecStart= xxxx -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock
xxx是代表原有的参数，追加 -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock 内容
# 保存启动文件后重启服务
systemctl daemon-reload
systemctl restart docker
# 检查看是否生效
ss -unlpt | grep 2375 
```

![image-20211106115620600](https://wywtypora.oss-cn-shanghai.aliyuncs.com/image/image-20211106115620600.png)

![image-20211106115506509](https://wywtypora.oss-cn-shanghai.aliyuncs.com/image/image-20211106115506509.png)

### 2.3添加节点

![](https://wywtypora.oss-cn-shanghai.aliyuncs.com/image/image-20211106115752885.png)

![image-20211106121422712](https://wywtypora.oss-cn-shanghai.aliyuncs.com/image/image-20211106121422712.png)

```bash
# 命名
docker-prod01
docker-prod02
# IP地址
47.100.34.199:2375
139.198.167.214:2375
```

### 2.4效果图

添加好了的docker节点效果图如下。

![image-20211106122151375](https://wywtypora.oss-cn-shanghai.aliyuncs.com/image/image-20211106122151375.png)

## 3.踩坑记录

### 3.1connection refused

FailureGet http://47.100.34.199:2375/_ping: dial tcp 47.100.34.199:2375: connect: connection refused

> 需要修改配置文件信息，添加 -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock 内容

![image-20211106113958518](https://wywtypora.oss-cn-shanghai.aliyuncs.com/image/image-20211106113958518.png)
