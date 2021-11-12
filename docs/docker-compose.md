

# Docker-compose安装SonarQube
## 1.安装Docker-compose

#### 1.Linux官方推荐方法安装Docker-Compose

Linux系统默认是没有安装`docker-compose`工具的，可以进入下面的网址。

> https://docs.docker.com/desktop/

进入亡之后，选择`Product Manuals` —>`Docker compose`—>`Liunx`后，可以看到三条命令，依次执行就可以安装`docker-compose`工具了。

**第一条命令：**

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# 或者
yum install docker-compose
```

如果一次安装不成功，可以多安装几次。一般是网络问题。

**第二条命令：**

```jsx
sudo chmod +x /usr/local/bin/docker-compose
```

**第三条命令：**

```jsx
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

安装好以后，用`docker-compose --version` 进行检查，如果能出现版本，说明安装成功了。

<font color=red>**查看是否安装成功：**</font>

```bash
docker-compose --version
```



![image-20211013110701706](https://img-blog.csdnimg.cn/img_convert/1630fb019b6ad30644711cefc311f7a3.png)

#### 2.编写docker-compose.yml文件

查询docker-comcpose.yml文件位置，并进行修改。

```shell
whereis docker-compose.yml
# 或者
locate docker-compose.yml
# 或者
find / -name "docker-compose*"
```

![image-20211013111353118](https://img-blog.csdnimg.cn/img_convert/7ec56f627eb468117efc82d555f297ea.png)