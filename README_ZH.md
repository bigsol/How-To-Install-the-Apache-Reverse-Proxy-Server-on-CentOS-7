# 如何在centos7上安装apache反向代理
如何在centos7上安装apache反向代理

<p><b>1 — 安装apache</b></p>
sudo yum update httpd<br><br>

sudo yum install httpd<br><br>

<p><b>2 — 检查web服务器</b></p>
当第一次安装完成后，apache不会自动运行。你需要手动启动apache

sudo systemctl start httpd<br><br>

验证服务是否运行执行这个命令

sudo systemctl status httpd<br><br>

你将会看到服务正在启动状态

![aaaa](https://user-images.githubusercontent.com/51197053/140646159-102eefb1-55a6-4418-a082-3b1f76e3094e.png)<br><br>


在浏览器地址栏上输入你的ip地址

http://your_server_ip

你会看到apache默认页面
![mstsc_zYtpec1PFY](https://user-images.githubusercontent.com/51197053/140646319-04f0e72b-f889-492f-bb87-38b41992ba0a.png)<br><br>

<p><b>3 — 操作apache程序</b></p>
<li>现在你的apache正在运行，介绍一些基础操作命令<br><br>

停止apache服务

sudo systemctl stop httpd<br><br>

启动apache服务

sudo systemctl start httpd<br><br>

重启apache服务

sudo systemctl start httpd<br><br>

如果配置文件改变了，重新加载配置文件

sudo systemctl reload httpd<br><br>

默认情况下,apache开机自启,如果你想关闭

sudo systemctl disable httpd<br><br>

恢复apache开机自启,如果你想关闭

sudo systemctl enable httpd<br><br>

<p><b>4 — 使用反向代理</b></p>

使用反向代理前，请确保以下modules已经安装

```
1- mod_proxy

2- mod_proxy_http
```

使用以下命令查看已经安装的modules

$ httpd -M

这个命令将返回一个当前正在运行的modules列表,如果那两个modules在列表当中则在httpd.conf中添加下列几行代码

$ sudo vim /etc/httpd/conf/httpd.conf

```vim
LoadModule proxy_module modules/mod_proxy.so

LoadModule lbmethod_byrequests_module modules/mod_lbmethod_byrequests.so

LoadModule proxy_balancer_module modules/mod_proxy_balancer.so

LoadModule proxy_http_module modules/mod_proxy_http.so

LoadModule proxy_ajp_module modules/mod_proxy_ajp.so

<VirtualHost *:80>

    ProxyPreserveHost On

    ProxyPass / http://192.168.1.50/

    ProxyPassReverse / http://192.168.1.50/

</VirtualHost>
```

重启apache服务器

$ sudo systemctl restart httpd

在浏览器地址栏上输入你的ip地址

http://your_server_ip