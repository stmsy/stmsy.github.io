---
title: Deploy A MongoDB Shard Cluster
---

When trying to store in MongoDB a large number of tweets obtained using the [Search API](https://dev.twitter.com/rest/public/search), I tried and deployed a shard cluster that consists of:

1. 3 query routers (`mongos`)
2. 3 config servers (`mongod`)
3. 3 shard servers (`mongod`), 
  
where each set of query router and config and shard servers run in 3 different Debian machines, with Debian 8.5 and MongoDB 3.2.11. 

First edit `/etc/hosts` as follows:

```shell
192.168.101.100   deb0
192.168.101.101   deb1
192.168.101.102   deb2

192.168.101.100   query0.example.com
192.168.101.100   config0.example.com
192.168.101.100   shard0.example.com
192.168.101.101   query1.example.com
192.168.101.101   config1.example.com
192.168.101.101   shard1.example.com
192.168.101.102   query2.example.com
192.168.101.102   config2.example.com
192.168.101.102   shard2.example.com
```

and create directories with the `root` privilege

1. `/var/lib/mongodb/shard`

2. `/var/lib/mongodb/config`

3. `/var/lib/mongodb/logs/shard`

4. `/var/lib/mongodb/logs/config`

5.  `/var/lib/mongodb/logs/query`

for the databases and logs in all of the machines. Moreover, before starting several `mongod` or `mongos` processes, you may want to edit and configure `/etc/security/limits.conf` as necessary.

Then issue the following commands in each of the three machines to run the several `mongod` process for the config and shard servers. Here I supporse that `numactl` is preinstalled from the APT repository and Transparent Huge Pages is disabled. Refer to [Disable Transparent Huge Pages (THP)](https://docs.mongodb.com/v3.2/tutorial/transparent-huge-pages/) and [Performance Best Practices for Mongo DB](https://www.mongodb.com/collateral/mongodb-performance-best-practices) for more detail.

```shell
$ sudo numactl --interleave=all mongod --configsvr --port 27019 --dbpath /var/lib/mongodb/config --fork --logpath /var/lib/mongodb/logs/config/config.log --maxConns 300
```

```shell
$ sudo numactl --interleave=all mongod --shardsvr --port 27018 --dbpath /var/lib/mongodb/shard --fork --logpath /var/lib/mongodb/logs/shards/shard/shard.log --maxConns 300
```

After starting the `mongod` processes as above, run the `mongos` process for each machine.

```shell
$ sudo numactl --interleave=all mongos --port 27017 --configdb config0.example.com:27019,config1.example.com:27019,config2.example.com:27019 --fork --logpath /var/lib/mongodb/logs/mongos/mongos.log --maxConns 300
```

and open the interactive shell as follows.

```shell
$ mongo --host query0.example.com --port 27017
```

Finally issue the following commands to add shards, enable sharding and choose the database collection to be sharded with nicely.

```
mongos> use admin
mongos> db.runCommand({"addShard": "shard0.example.com:27018"})
mongos> db.runCommand({"addShard": "shard1.example.com:27018"})
mongos> db.runCommand({"addShard": "shard2.example.com:27018"})
mongos> db.runCommand({"enableSharding": "databaseName"})
mongos> db.runCommand({"shardCollection": "databaseName.collectionToBeSharded", "key": {"someKey": 1}})
```
