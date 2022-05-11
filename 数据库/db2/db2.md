#### 执行sql

##### -s
	遇到错误就中断
##### -t 
	表示语句使用默认的语句终结符——分号；
##### -v
	表示使用冗长模式，这样 DB2 会显示每一条正在执行命令的信息；
##### -f
```txt
表示其后就是脚本文件；
```
##### -z
	其后面跟日志文件



##### 断开所有连接

	db2 force applications all 
<h5>执行存储过程sql文件</h5>
	db2 -td@ -f  xxx.sql

##### Sql 重构表格
CALL SYSPROC.ADMIN_CMD('REORG TABLE CIF.EDRAFTPAYEE');