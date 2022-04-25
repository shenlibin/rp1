### 安装 ###

1. 下载 redis-xxx.tar.gz

2. tar xzvf redis-xxx.tar.gz 解压缩

3. make   编译

   应该会报错,百度自行解决

4. make PREFIX=/usr/xxxx   install

   这里 "/usr/xxxx"就是redis的安装路径

5. cd /usr/xxxx/bin

   ./redis-server 启动一下看看

   ./redis-server xxxx/redis.conf 
   
   redis.conf 在解压缩出来的目录里

### 配置 ###

​	vi redis.conf 

1. 后台启动:daemonize no  ---> yes

2. 外部ip绑定:bind 127.0.0.1

3. 保护模式:protected-mode yes ----> no 

4. 连接需要密码:requirepass  password

5. 总数据库个数:databases num

6. 

   

   

### 客户端工具 ###

cd /usr/xxxx/bin

./redis-cli 进入客户端命令模式

指定端口

./redis-cli -p xxxx

指定ip

./redis-cli -h  xxxx

指定密码

./redis-cli -a xxxx

测试

​	ping  返回PONG

​	set key1 value1

​	get key1

### 数据类型

###### string(byte[])



###### hash



###### list



###### set



###### sortedset



###### 层级目录



### 持久化

###### bgsave

优点:可以直接调用,触发条件在自己掌控范围

缺点:必须手动触发,量大的编程比较繁琐容易遗忘



###### rdb

在redis.conf中

dbfilename dump.rdb  数据库持久化的文件名"dump.rdb"

dir ./ 	数据库持久化文件的保存路径当前文件夹"./"

save 900 1   代表如果在900秒内  有1次数据的变化,就触发持久化(在每900秒的时候才触发?)

save 300 10    代表如果在300秒内  有10次数据的变化,就持久化(在每300秒的时候才触发?)

saven 60 1000    代表如果在60秒内  有1000次数据的变化,就持久化(在每60秒的时候才触发?)

优点:一次配置,自动触发

缺点:如果没有达到触发条件和时间,数据可能会丢失



###### aof

在redis.conf中  

appendonly yes   开启  和rdb互斥???

appendfilename "appendonly.aof"  文件名

命令行追加模式

将数据库启动之后收到的所有的操作都记录在aof文件中,待数据库重启时将命令再模拟运行一遍达到恢复数据的效果

优点:不会丢失数据

缺点:当aof文件很大的时候,恢复数据性能消耗很大





### 集群

好处:保持高可用性提高可靠性,读写分离分散存取的IO压力

集群节点数一般为单数个n



##### 环境搭建

因为redis可以用不同的conf文件启动不同的服务,所以只要配置多个conf文件来启动就可以了

基于redisconf文件可以include 的特性,可以提取公有配置减少编码量

###### 读写分离

见文件夹  redis-cluster 中的include配置,由一个公共的文件redis-common.conf

和3个节点的私有配置文件组成



###### 主备切换,哨兵

哨兵:	当主节点离线时,推举一个从节点升级为主节点

哨兵有多个,自己本身也是一个集群?



sentinel.conf同redis.conf 是用来启动哨兵的配置文件

同redis.conf 配置集群一样,配置多个哨兵的文件



mymaster 是类似于一个变量,贯穿全配置文件吧,后面的2 是哨兵个数的(n+1)/2

sentinel monitor mymaster 192.168.50.132 6379 2



`

























