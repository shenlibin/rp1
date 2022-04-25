### 关机重启

shutdown -r now  现在重启

shutdown -h now 现在关机



### 网卡开机自启

cd /etc/sysconfig/network-scripts/

vi ifcfg-ensxxxxx

修改 onboot=yes

service network start

### 时间

date -R 查看时间

修改时区

​	vi /etc/profile    加一行  export TZ='Asia/Shanghai'



设置时间

​	date -s "2020-01-01 09:09:09"     

​	hwclock -w     将时间设置到bios中 重启不失效

网络同步时间

​	 yum install -y ntpdate 

​	 ntpdate ntp.aliyun.com 



### 文件操作 ###

pwd 查看当前目录

cp   /xx/xx/xxx.xx  /xxx/xxx/   复制文件

​	后面一个目录不打文件名,表示不变更文件名,如果需要变更文件名就要打上

mv  移动文件,同cp  可以用来重命名

rm /xx/xx/xxx.xx 删除文件

rm -rf  /xx/xx/ 删除文件夹

touch xxx  新建一个空白文件

mkdir -p  xxx   -p表示父路径不存在会创建,不加-p 父路径不存在会报错

ls 命令  查看文件

​	-a 列出所有文件和目录 包括隐藏文件"."开头的

​	-l 以列表的形式打出所有文件的信息

​	-t 按时间排序

​	-r 通常和t组合  逆排序

​	-R 递归出所有的子文件夹和内容,慎用

​	



### 网络 ###

##### 防火墙 #####

###### firewall ######

systemctl start firewalld:启用防火墙

systemctl stop firewalld:停用防火墙

systemctl enable firewalld:设置开机启动

systemctl disable firewalld:设置停止并禁用开机启动



firewall-cmd --state:查看状态

firewall-cmd --query-port=xxx/tcp:防火墙查看端口可用状态

firewall-cmd --permanent --add-port=xxx/tcp:添加某端口通过  --permanent 不加是临时 reload之后就失效,加了之后reload永久生效

firewall-cmd -reload:重启防火墙







###### iptables ######  













### VI 文本编辑/查找 ##







### 解压文件 

解压文件

tar -zxvf  xxxxxx.tar.gz







### jdk配置

export JAVA_HOME=/usr/local/java/jre1.8.0_301

export JRE_HOME=${JAVA_HOME}

export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib:$CLASSPATH

export JAVA_PATH=${JAVA_HOME}/bin:${JRE_HOME}/bin:

export PATH=$PATH:${JAVA_PATH}

最后  source /etc/profile 刷新一下配置







