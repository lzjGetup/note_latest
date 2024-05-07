# redo log

`持久性保证`

![[Pasted image 20240301144948.png]]


# undo log
`原子性保证`
![[Pasted image 20240301145320.png]]

# MVCC

![[Pasted image 20240301145740.png]]


# 表结构隐藏字段

![[Pasted image 20240301150213.png]]

# MVCC实现原理
*undo log*
- 回滚日志，在insert、update、delete的时候产生的便于数据回滚的日志。
- 当insert的时候，产生的undolog日志只在回滚时需要，在事务提交后，可被立即删除。
- 而update、delete的时候，产生的undolog日志不仅在回滚时需要，在快照读时也需要，不会立即被删除。

*undo log 版本链*

![[Pasted image 20240301151024.png]]

*read view*

![[Pasted image 20240301151328.png]]


![[Pasted image 20240301151916.png]]


# 系统数据库

![[Pasted image 20240301154804.png]]

# 常用工具

### mysql

![[Pasted image 20240301154954.png]]

### mysqlbinlog
![[Pasted image 20240301160001.png]]

### mysqlshow

![[Pasted image 20240301160329.png]]


### mysqldump

![[Pasted image 20240301160647.png]]


### mysqlimport/source

![[Pasted image 20240301161521.png]]