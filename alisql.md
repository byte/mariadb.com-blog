# AliSQL and some features that have made it into MariaDB Server

I attended a talk on AliSQL by Yingqiang Zhang and found it to be extremely interesting. AliSQL is the fork of MySQL (maintained by Alibaba) that powers all of the group from Tmall, Taobao, Alibaba.com, 1688.com, AliExpress, Cainiao and the payment's network Alipay. 

AliSQL isn't new - they've had this fork since 2011: AliSQL 5.1 (Bugfixes for DDL, eliminate race conditions), 2012: AliSQL 5.5 (parallel replication, optimize hot SKUs), 2014: AliSQL 5.6 (Enhanced threadpool, SQL firewall). The team have found/reported/fixed over 40+ bugs, added 41 new features, and optimised 27 bottlenecks. All recent releases of MySQL have had AliSQL contributions (5.6.25 onwards, 5.7.8 onwards, and even 5.8 branch).

## AliSQL benefitting MariaDB Server
While not mentioned in the talk, its clear that MariaDB Server 10.0+ has benefited from their tree as well -- our [log of contributions](https://mariadb.com/kb/en/mariadb/log-of-mariadb-contributions/) lists Lixun Peng/Taobao as having contributed to [multi-source replication](https://mariadb.com/kb/en/mariadb/multi-source-replication/) (something MariaDB Server had in a shipping GA release since March 2014; a similar feature appears in MySQL 5.7 GA released October 2015). But that is not all, there is also per-thread memory counting and usage, fixed in [MDEV-4011](https://jira.mariadb.org/browse/MDEV-4011). Don't forget that they've constantly released many of their [features as opensource](http://mysql.taobao.org/index.php?title=Patch_source_code).

So what is per-thread memory counting? It is exposed either via SHOW STATUS:

	show status like 'memory_used'\G
	*************************** 1. row ***************************
	Variable_name: Memory_used
			Value: 73808
	1 row in set (0.00 sec)

But that is obviously not all. Have you seen the `INFORMATION_SCHEMA.PROCESSLIST`? Compare the difference when it comes to MySQL 5.7.12 and MariaDB Server 10.1.13:

### MySQL 5.7.12
	select * from INFORMATION_SCHEMA.processlist\G
	*************************** 1. row ***************************
		 ID: 8
	   USER: msandbox
	   HOST: localhost
		 DB: NULL
	COMMAND: Query
	   TIME: 0
	  STATE: executing
	   INFO: select * from INFORMATION_SCHEMA.processlist
	1 row in set (0.00 sec)

### MariaDB Server 10.1.13
	select * from INFORMATION_SCHEMA.processlist\G
	*************************** 1. row ***************************
			   ID: 4
			 USER: msandbox
			 HOST: localhost
			   DB: NULL
		  COMMAND: Query
			 TIME: 0
			STATE: Filling schema table
			 INFO: select * from INFORMATION_SCHEMA.processlist
		  TIME_MS: 0.464
			STAGE: 0
		MAX_STAGE: 0
		 PROGRESS: 0.000
	  MEMORY_USED: 84552
	EXAMINED_ROWS: 0
		 QUERY_ID: 24
	  INFO_BINARY: select * from INFORMATION_SCHEMA.processlist
			  TID: 22005
	1 row in set (0.00 sec)

## What can we look forward to in the future from AliSQL?
It was brought up in the talk that AliSQL is not currently opensource, but there are some very interesting features around it that would likely benefit many MariaDB Server users:

* optimising hot rows, which is a common issue in Alibaba referred to as an "optimisation for hot SKUs", typical during a Single's Day. This has been powering AliSQL in several versions, and they are working on ensuring there is a row cache, a new InnoDB row lock type, as well as group updates of associated transactions.
* They have split the redo log buffers into two, one for each reading and writing.
* InnoDB column compression using ZLIB, which also supports online DDL.
* The idea of flashback and a recycle bin, all related to the ["time machine"](https://drive.google.com/open?id=0B7HE7L1OgKJFeGFISElYODh2NEk) concept that we can [expect to see soon](http://www.bytebot.net/blog/archives/2016/04/14/mariadb-berlin-meetup-notes-slides).
* Another interesting feature is the idea of thinking in terms of a glass of water. There is low water mark protection in where they have an enhanced threadpool that buffers queries while the thread is running. If for some reason it exceeds the the low water level, send it to the high water mark where they have a kind of "SQL firewall" that denies queries via a blacklist strategy. Their rule syntax makes use of an Abstract Syntax Tree (AST) between the parser and optimiser of their server.
* They also do binlog speed throttling, and have enhanced information around deadlocks.

All in, here's hoping that the AliSQL tree is open, so that we can look at features and see what ends up in a future release of MariaDB Server.