源码地址：https://github.com/happyletme/requestnew

第一篇：https://testerhome.com/topics/13269

第二篇：https://testerhome.com/topics/14801
主要实现了项目管理，模块管理，用例管理，步骤管理，动态Sql配置，访问地址配置，开发数据库配置，邮箱配置，执行模块；之后需要去优化的模块http接口采用文件传输方式，接口依赖，日志模块，邮件模块，统计分析和html报告(目前采用HTMLTestRunner自动生成的报告),失败重跑次数动态配置目前写死3次，定时执行模块
环境：
Python 3.6.4
Django 2.0.2
django-bootstrap3
pymysql,pymssql,DBUtils
Requests
Unittest

登录界面


项目和模块界面
涉及的主要是项目和模块的管理,数据的增删改查






用例和步骤界面
这里的用例有点像unittest的一个case，步骤相当于case下面的test函数，一个case对应多个step




接口方式目前提供了3种,get,post表单，post body体的方式，断言开关打开则使用断言，涉及到的变量都是${}表示






动态sql配置界面
动态sql绑定的主键是步骤名，提供了前置后置方式，是否为查询方式






访问地址配置和开发数据库配置




整个项目运行先挑选用例点击生成脚本按钮,生成任务目录和测试脚本


在task目录下生成本次命名的任务和对应用例名字的脚本


生成脚本如


最后点击执行任务，选择配置的访问Ip和数据库


生成报告


最近项目不忙，抱着写写看的想法，测试新人，请各位大神多多指点。


本次主要涉及到前端样式优化以及部分bug修复






修复bug：
1.环境配置取消必须绑定端口号
2.接口测试取消必须连接数据库
3.修复邮箱未配置无发执行任务
优化：
1.优化登录页面
2.优化菜单模块和页面样式和部分按钮
3.优化定时模块

之后会优化断言模块和实现接口依赖模块




配置：

linux:

1.根据testhome安装python3.6和对应的python库

2.把源代码放到linux下（我创建了pj目录，项目放在/home/pj下）

3.选择一个mysql数据库作为测试库，在django的setting.py文件的86行配置数据库的信息(ip,端口，数据库名称，用户名，密码)

4.进入到项目根目录，数据库迁移：python manage.py makemigrations在request应用下的migrations目录下创建了一个 0001_initial.py 文件，执行python manage.py migrate，执行完成库表生成

5.创建第一个用户python manage.py createsuperuser，之后的用户登录http://192.168.100.158:8000/admin/去创建用户组和用户以及分配权限

6.在pj目录下创建logs目录，下面创建request.log文件存放项目启动文件

7.在django的setting.py文件的28行，添加自己linux的ip（我的是ALLOWED_HOSTS = ['192.168.100.158']）

8.把启动shell和关闭shell放在根目录下（requestnew）,sh start.sh,项目就启动了；项目关闭则执行sh shutdown.sh

9.如果目录结构想要有所调整或者启动端口（默认8000）有所调整，需要修改启动和关闭文件

10.其他机子能访问到（配置的ip:8000）就成功了。

windows要靠编译器启动;

1.根据testhome安装python3.6和对应的python库

2.选择一个mysql数据库作为测试库，在django的setting.py文件的86行配置数据库的信息(ip,端口，数据库名称，用户名，密码)

3.进入到项目根目录，数据库迁移：python manage.py makemigrations在request应用下的migrations目录下创建了一个 0001_initial.py 文件，执行python manage.py migrate，执行完成库表生成

4.创建第一个用户python manage.py createsuperuser

5.django的setting.py文件的28行，因为是本地启动保持ALLOWED_HOSTS = []就好了

6.配置编译器启动方式，选择django server启动，HOST填写127.0.0.1，port填写8000，运行

7.访问127.0.0.1:8000，能访问到就ok了
