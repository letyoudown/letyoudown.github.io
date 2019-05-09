---
layout:     post                    # 使用的布局（不需要改）
title:      Struts+MyBatis简单搭建    # 标题 
subtitle:   结构的完善                #副标题
date:       2019-05-09              # 时间
author:     WX                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签

- javaweb
---



# Struts+MyBatis简单搭建

> #you are being watched













### 1.文件结构

![1557389964029](https://i.loli.net/2019/05/09/5cd3e66715df5.png)

![1557389983232](https://i.loli.net/2019/05/09/5cd3e6669d671.png))

### 2.配置文件

struts.xml   action类中要有对应的方法、返回值，命名空间可以不要

访问时路径为http://localhost:8888/MavenEMS/aa/showAllUser

ip+端口+项目名+命名空间+action类中的方法名

name="*" 表示为任意

可以改成name="user_*" 访问时就要把最后的方法名改为user_showAllUser

![1557390092101](https://i.loli.net/2019/05/09/5cd3e666b8bf5.png)



UserDAOMapper.xml  也就是DAO的实现 里面写sql语句，下面的是select标签，还有insert等

![1557390205879](https://i.loli.net/2019/05/09/5cd3e666d0aab.png)



mybatis-config.xml   基本配置

![1557390506798](https://i.loli.net/2019/05/09/5cd3e66720c17.png)





最后web.xml里面加过滤器

![1557390654912](https://i.loli.net/2019/05/09/5cd3e667053ea.png)

### 3.代码的简单实现

工具类直接复制

实体类，service类和dao类按规范书写即可

action类

![1557390770755](https://i.loli.net/2019/05/09/5cd3e66707588.png)

页面index.jsp

![1557390822463](https://i.loli.net/2019/05/09/5cd3e66701a56.png)

最后部署到tomcat上跑一下就成了

![1557390857763](https://i.loli.net/2019/05/09/5cd3e66717d58.png)

