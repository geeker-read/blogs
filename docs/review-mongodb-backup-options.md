# [译] MongoDB 几种备份方案

![](https://cdn.nlark.com/yuque/0/2020/jpeg/639317/1578533002833-91cc0ab1-db73-42e0-9fa2-f0ac1f0c39dd.jpeg)

> 原文：[A Review of MongoDB Backup Options](https://severalnines.com/database-blog/review-mongodb-backup-options)

数据库备份是数据保护与恢复的一种方法。是存储数据库运行状态（Operational state）、结构和数据的一个过程。对防止技术故障或灾难造成数据损失，起到非常重要的作用。因此数据的备份不容忽视。

MongoDB 提供了多种工具和技术来备份数据库。

在本文中，我们将讨论主流的 MongoDB 备份和还原流程。

基本上有三个最常用的选项来备份您的 MongoDB 服务器或群集。

* Mongodump 和 Mongorestore
* MongoDB 云管理
* 数据库快照（Database Snapshots）

除了这些常规选项外，本文还讨论了其他备份方案。

## MongoDump 和 MongoRestore

如果你的数据库比较小（<100GB），并想完全控制你的备份文件。那么 MongoDump 和 MongoRestore 就是最佳搭档。通过这两个 mongo 脚本命令你可以手动备份数据库或集合（collections）。Mongodump 会将将所有数据以 Binary JSON（BSON）格式转储到指定位置。 Mongorestore 可以将这些 BSON 文件来还原到你的数据库。

### 备份整个数据库

`$ sudo mongodump --db mydb --out /var/backups/mongo`

输出：

```
2018-08-20T10:11:57.685-0500    writing mydb.users to /var/backups/mongo/mydb/users.bson
2018-08-20T10:11:57.907-0500    writing mydb.users metadata to /var/backups/mongo/mydb/users.metadata.json
2018-08-20T10:11:57.911-0500    done dumping mydb.users (25000 documents)
2018-08-20T10:11:57.911-0500    writing mydb.system.indexes to /var/backups/mongo/mydb/system.indexes.bson
```

注意条命令的 `--db` 参数，它用来指定要备份的数据库名。如果不指定这个参数，Mongodump 命令将会**备份所有的数据库**。

### 备份单个集合（collection）

`$ mongodump -d mydb -o /var/backups/mongo --collection users`

这条命令会备份 `mydb` 数据库里的 `users` 集合。

### 定期备份

通常我们要定期对 MongoDB 数据库做备份。例如每天凌晨 3:03 点进行备份，这样在 Linux 下可以通过 crontab 来实现。

`$ sudo crontab -e`

添加一行

`3 3 * * * mongodump --out /var/backups/mongo`

### 恢复整个数据库

恢复数据库可以通过 `Mongorestore` 命令和 `--db` 参数来实现。它将读取由 `Mongodump` 创建的 `BSON` 文件并还原你的数据库。

`$ sudo mongorestore --db mydb /var/backups/mongo/mydb`

输出

```
2018-07-20T12:44:30.876-0500    building a list of collections to restore from /var/backups/mongo/mydb/ dir
2018-07-20T12:44:30.908-0500    reading metadata file from /var/backups/mongo/mydb/users.metadata.json
2018-07-20T12:44:30.909-0500    restoring mydb.users from file /var/backups/mongo/mydb/users.bson
2018-07-20T12:45:01.591-0500    restoring indexes for collection mydb.users from metadata
2018-07-20T12:45:01.592-0500    finished restoring mydb.users (25000 documents)
2018-07-20T12:45:01.592-0500    done
```

### 恢复整个集合

`$ mongorestore -d mydb -c users mydb/users.bson`

如果你备份的数据是 JSON 格式，可以用下面这条命令恢复。

`mongoimport --db mydb --collection users --file users.json --jsonArray`

### 优点

* 简单易用
* 对备份文件完全可控
* 可将备份文件存在任意 NFS

### 缺点

* 每次都是完整的备份而不是差异备份
* 大型数据库的备份和恢复很耗时
* 默认下不是时间点（ point-in-time ）备份，意味着在数据的备份过程中可能出现数据的更新，这样就不能保证数据的一致性。可以通过 `--oplog` 参数解决这个问题。它会在数据库备份完成后留下快照。

## MongoDB Ops Manager

Ops Manager 运行在你数据中心，对 MongoDB 进行管理的应用程序。它会持续备份你的数据库，并提供通过时间点（ point-in-time ）恢复数据。它会链接到 MongoDB 实例，先对当前状态数据进行备份。再不断的将压缩/加密的数据发送到 Ops Manager 来进行持续备份。

### 优点：

* 默认下是时间点（ point-in-time ）备份
* 基本不会对生产环境带来性能问题
* 支持集群的一致性快照
* Flexibility to exclude non-critical collections（汗！，没明白什么意思？）

### 缺点

* 恢复数据库时，网络延迟会随着快照变大而增大

## MongoDB 云管理

基于云的备份解决方案，安装 Cloud Manager 即可对数据库进行备份和恢复。它会将备份的数据保存在 MongoDB 云端。

### 优点

* 非常易用，可视化
* 持续备份

### 缺点

* 备份数据不可控，因为存在云端
* 成本（花钱）
* 恢复慢

## 数据库文件快照

这个备份数据库最最简单的方案，你可以将 `data/` 里的所有文件一并复制到任意安全的地方，在复制之前应先停止对数据库的写入操作，以保证数据一致性。使用 `db.fsyncLock()` 命令停止写入操作。

**有两种快照类型：**

1. 云快照
2. 操作系统快照

一般云服务提供商都会提供备份快照功能。如果使用 Linux 可以通过打 LVM 快照。LVM 快照不能移植到其他机器，所以基于云的快照会好于操作系统快照。

### 优点

* 易用
* 快照完全可控
* 差异性快照
* 无需下载快照来进行恢复，可以为快照创建一个数据卷。

### 缺点

* 只能恢复断开点（breakup points）时的数据
* 维护有时会复杂
* 集群下可能需要 DevOps 团队介入

## MongoDB Consistent Backup

MongoDB 集群一致性备份的工具。可以备份集群的一个或多个分片数据库。

`$ mongodb-consistent-backup -H localhost -P 27017 -u USERNAME -p PASSWORD -l /var/backups/mongo`

兼容 MongoRestore 命令。

`$ mongorestore --host localhost --port 27017 -u USERNAME -p PASSWORD --oplogReplay --dir /var/backups/mongo/mydb/dump`

### 优点

* 开源
* 可用在集群
* 可远程备份
* 弹性伸缩
* 易安装、易运行

### 缺点

* 不成熟产品
* 远程上传选项少
* 保存在磁盘不支持数据加密
* 官方代码缺乏测试

## ClusterControl

ClusterControl 是一个一体化、自动化的数据库管理系统。 可以轻松地监控、部署、管理和扩展数据库集群。 支持 MySQL、MongoDB、PostgreSQL、Percona XtraDB 和 Galera Cluster。 

可自动执行几乎所有数据库操作，例如部署群集、从任何群集中添加或删除节点、连续备份、扩展群集等。

所有这些，您都可以从 ClusterControl 提供的 GUI 中进行操作。

### 优点

* 易安装、易使用
* 多种可选备份方案
* 定期备份
* 备份验证
* 备份报告

### 缺点

* 两种备份方法都在内部使用 mongodump，在处理大型数据库时会遇到一些问题。

## 结论

好的备份策略是任何数据库管理系统的关键部分。 MongoDB 提供了许多备份和恢复/还原选项。 

除了好的备份方法外，拥有多个数据库副本也非常重要，这有助于在无需停机下还原数据库。

有时对于较大的数据库，备份过程可能会占用大量资源。 因此，您的服务器应配备好一些的 CPU，内存和更多磁盘空间来处理此类负载。

由于某些原因，备份过程可能会增加服务器的负载，因此应该在晚上或非高峰时间运行备份过程。

---

极客阅读：[geeker-read.com](https://geeker-read.com)

<img src="https://github.com/geeker-read/weekly_issues/raw/master/docs/wx.png" width="450" />
