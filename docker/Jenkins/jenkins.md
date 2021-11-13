1.创建jenkins的工作目录并赋予权限
```bash
mkdir -p  /usr/local/jenkins/jenkins_home
cd /usr/local/jenkins
chown -R 1000 jenkins_home #把当前目录的拥有者赋值给uid 1000
```

查看密码并登陆
```bash
docker logs -f jenkins

# 初始密码
02e2038140c642dca0f12a219dc52f7c
```

![image-20211112221032554](https://wywtypora.oss-cn-shanghai.aliyuncs.com/image/image-20211112221032554.png)
