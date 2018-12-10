
# CentOS 7安装MongoDB总结详解以及相关配置

## 第一步：下载MongoDB

```
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-4.0.4.tgz
```

## 第二步：解压 MongoDB

```
tar -zxvf mongodb-linux-x86_64-4.0.4.tgz
```

## 第三步：将解压后的文件夹移动到/usr/local/的mongodb目录下

```
mv mongodb-linux-x86_64-4.0.4 /usr/local/mongodb
```

## 第四步：配置系统文件profile

```
vi /etc/profile
```

插入下列内容：

```
export MONGODB_HOME=/usr/local/mongodb  
export PATH=$PATH:$MONGODB_HOME/bin
```

注意保存后要重启系统配置：

```
source /etc/profile
```

## 第五步：创建用于存放数据和日志文件的文件夹，并修改其权限增加读写权限

```
cd /usr/local/mongodb
mkdir -p data/db
chmod -R 777 data/db
mkdir logs
cd logs
touch mongodb.log
```

## 第六步：新增mongodb启动配置

进入到bin目录，增加一个配置文件：

```
cd /usr/local/mongodb/bin  
vi mongodb.conf
```

插入下列内容：

```
dbpath = /usr/local/mongodb/data/db #数据文件存放目录
logpath = /usr/local/mongodb/logs/mongodb.log #日志文件存放目录
port = 27017  #端口
fork = true  #以守护程序的方式启用，即在后台运行
bind_ip=0.0.0.0
```

## 第七步：启动mongod数据库服务，以配置文件的方式启动

```
cd /usr/local/mongodb/bin
./mongod -f mongodb.conf
```



