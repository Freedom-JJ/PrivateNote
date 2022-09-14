## 简介：

本安装教程针对直接下载zip格式的mysql，如果是msi可以直接傻瓜式安装。

1.进入mysql下的bin目录下

![image-20220901193740051](C:/Users/DoYou/AppData/Roaming/Typora/typora-user-images/image-20220901193740051.png)

2.需要初始化mysql服务

```
mysqld --initialize --user=root --console
```

**最后会得到初始化的密码**，然后登录进root账号修改密码

```
mysql -u root -p
```

3.在windows上安装服务

```
mysqld --install
```

这样就成功的安装了mysql的自启动服务

