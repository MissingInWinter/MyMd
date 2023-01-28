# Linux下配置Java环境



个人新购买了一台云服务器、安装的是centos系统、什么还没有







[Java 下载 |神谕 (oracle.com)](https://www.oracle.com/java/technologies/downloads/#java8)

![java8_download](images\java8_download.png)

在Linux系统中路径开始有一个单斜杠 ‘/’ 代表了从根目录开始、‘/’就表示根目录。（此外像每个目录中都含有的 '.'与'..'分别表示当前目录与上层目录）、最开始来到根目录 cd /       之后查看当前目录文件 ll

![java8_download](images\root.png)

[家庭/学校免费 - NetSarang Website (xshell.com)](https://www.xshell.com/zh/free-for-home-school/)

我个人使用的是xshell和xftp来使用命令行、传输文件



我在根目录下新建一个app目录、个人打算把软件安装在这里

mkdir /app

`tar -zxf /app/jdk-8u351-linux-x64.tar.gz`

`tar -zxvf jdk-8u171-linux-x64.tar.gz -C /app`

解压文件到我们新建的根目录下的app文件夹内

![解压成功](images\解压成功.png)

之后就去配置我们的环境变量

编辑配置文件：

`vim /etc/profile`

在文件末尾按   i   键进入插入模式（或在命令行按大写的G键---跳转到文件末尾、再按小写的o键---在行尾另起一行并进入插入模式）

`export JAVA_HOME=/app/jdk1.8.0`

`export PATH=$JAVA_HOME/bin:$PATH`

![Windows_path_1](images\Windows_path_1.png)

![wq](images\wq.png)

使配置文件生效：

`source /etc/profile`

`java -version`

![java_version](images\java_version.png)

nohup java -jar hello-1.0.jar --server.port=80 >jarlog 2>&1 &



netstat  -nlp|grep 80

![netstat1](images\netstat1.png)

kill 11344
