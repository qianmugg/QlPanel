# QlPanel创建青龙面板

1.安装docker
使用 root 权限登录 Centos。确保 yum 包更新到最新。
sudo yum update
安装的yum工具集
yum install -y yum-utils
安装docker-ce的yum源:
yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
安装docker-ce
dnf install docker-ce
或者用yum安装

yum install docker-ce
查看docker服务状态:
systemctl status docker.service
开启自启动:
systemctl enable docker.service
开启服务:
systemctl start docker.service
##2.青龙面板安装
拉取青龙的镜像文件（官方）
docker pull whyour/qinglong:latest
创建容器
docker run -dit \
-v $pwd/ql/config:/ql/config \
-v $pwd/ql/log:/ql/log \
-v $pwd/ql/db:/ql/db \
-v $pwd/ql/scripts:/ql/scripts \
-v $pwd/ql/jbot:/ql/jbot \
-v $pwd/ql/repo:/ql/repo \
-p 5700:5700 \
-e ENABLE_HANGUP=true \
-e ENABLE_WEB_PANEL=true \
--name qinglong \
--hostname qinglong \
--restart always \
whyour/qinglong:latest
然后就可以通过http://ip:5700访问面板了

默认账号：admin 密码：admin
反回到shell 输入：

cat /ql/config/auth.json
输出的结果就是实际的密码了
{"username":"admin","password":"******"
至此，青龙面板就安装完成了！
