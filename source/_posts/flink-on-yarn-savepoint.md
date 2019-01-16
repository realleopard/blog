---
title: Savepoint 在 Flink On Yarn 下的使用
date: 2019-01-15 11:20:18
categories:
- flink
tags: 
- flink
- flink on yarn

---

<!--more-->

# 配置文件
在 flink-conf.yaml 中配置 savepoint 的存储位置

```
state.savepoints.dir: hdfs:///flink/flink-checkpoints
```

# 列出当前job
```
flink list -yid [for yarn, applicationId] -z [zookeepernamesapce, for high availablity mode]

flink list -yid application_1541130324309_128080 -z cluster_by_job
```

# 停止job，并存储状态
```
flink cancel -s JobId -yid [for yarn, applicationId] -z [zookeepernamespace, for ha] 

flink cancel -s  cababd2aadf69a263eda49df0f1efa82 -yid application_1541130324309_126267 -z cluster_by_job
```

# 从指定 savepoint 启动 job
```
flink run -s  hdfs:///flink/flink-checkpoints/savepoint-cababd-b92695040cfe  [args]
```

# 强力建议
