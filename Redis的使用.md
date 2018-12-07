## 配置
默认配置RDB持久化方式

# 1.1后台运行

1.	Redis-server &

2.	修改配置文件：daemonize yes

# 通用命令
Exists key 是否存在这个键

Keys pattern 根据正则表达式查询存在的键
Eg：keys *

Ps –ef | grep –i redis 查看redis启动的进程

Kill -9 进程号

killall 进程名 杀掉所有进程

Save(主进程快照)/bgsave（子进程快照）手动进行RDB持久化（快照）

上面的命令，如果出现:ERR或者没有备份成功，原因启动redis没有在root用户下面执行服务

<font color=red>注意：子进程快照的时候会占用和主内存样的内存资源</font>


Bgrewriteaof对aof持久化文件进行优化，文件中只保留最终的修改记录  

# String 的使用
```shell
Set key value 表示设置一个值
Eg: set name Tom
Mset key value key value .. 设置多个键值
Eg：mset a 1 b 1 .
Get key 根据键获取值
Eg: get name
Mget key1 key2 . . . 根据多个键获取多个值
E：mget a b
Setrange key 10 newString 从第10个位置开始替换成newString
Init：1541914268@qq.com result：1541914268@163.com
Eg：setrange key 11 163.com
Rename key newKey重命名键
Eg: rename email newEmail
Append key str 在后面追加str
Eg：append name str
```
# Redis集群
创建六个redis服务器实例，实现三主三从
分别是6379 6380 6381 6382 6383 6384

Redis一共有16384个插槽

查看集群中所有的节点：cluster nodes
## 1.设置主从关系
![image](https://note.youdao.com/yws/public/resource/efb6208c50a0bfbe546f4b74f48360aa/xmlnote/53355A4B11A34EE1A8277FD56658065B/7519)
## 2.配置文件
port 7000

cluster-enabled yes

cluster-config-file nodes.conf

cluster-node-timeout 5000

appendonly yes

pidfile

## 3. 启动redis服务实例
Usr/local/redis/bin/redis-server usr/local/redis/cluster/6379/redis.conf
## 4.创建集群的命令，
5.0之后不再使用redis-trib.rb, Ruby脚本创建集群。使用redis-cli创建：
```shell
/usr/local/redis/bin/redis-cli --cluster create 192.168.241.128:7001 192.168.241.128:6380 192.168.241.128:6381 192.168.241.128:6382 192.168.241.128:6383 192.168.241.128:6384 --cluster-replicas 1
```
## 5.登录客户端
/usr/local/redis/bin/redis-cli -c -p 6383
## 6.集群执行过程
1.	接收命令 set abc 123。
2.	通过key(abc)计算出插槽值，然后根据插槽值找到对应的节点（abc对应的插槽值为7680）
3.	重定向到该节点执行命令。
插槽和key的关系
通过 CRC16来计算出哈希值，然后对哈希值对16384取余，其结果就是对应的插槽值
## 7.添加节点
Redis –cluster add-nodes newIP:newPort exitingIp:exitPort
Eg: Redis - -cluster add-nodes 192.168.241.128:6385 192.168.241.128:6379
## 8.分配节点hash槽
Redis - -cluster reshard newIP:newPort
Eg：redis –cluster reshard 192.168.241.128:6385

再输入所分配的个数

输入给那个ID分配

输入从那个ID给上面那个ID的hash槽

其中如果输入all则是在所有的节点中平均分配给指定的ID

直到输入done开始分配

<font color=red>说明：上面的id是节点的唯一ID
 
## 9.删除节点
1. 首先把删除节点的hash槽分配到其它节点上
2. 删除该节点
使用命令：redis-cli - -cluster del-nodes ip:port id
Eg: redis-cli - -cluster del-nodes 192.168.241.128:6381 2c02eed11562e190a045dcd98ed98ceb5031fa4c 
3. 关闭集群一个节点
/usr/local/redis/bin/redis-cli –p port shutdown

## 10.使用
出现这个错的，因为jedis的jar包的版本不对。
 ![image](https://note.youdao.com/yws/public/resource/efb6208c50a0bfbe546f4b74f48360aa/xmlnote/8BEE944613344BD0ABC08F050CD6F964/7559)
集群的代码使用
```java
@Test
public void jedisCluster() {
    Set<HostAndPort> set = new HashSet<HostAndPort>();
    set.add(new HostAndPort("192.168.241.128", 7001));
    set.add(new HostAndPort("192.168.241.128", 7002));
    set.add(new HostAndPort("192.168.241.128", 7003));
    set.add(new HostAndPort("192.168.241.128", 7004));
    set.add(new HostAndPort("192.168.241.128", 7005));
    set.add(new HostAndPort("192.168.241.128", 7006));
    JedisCluster cluster = new JedisCluster(set);
    cluster.set("cluster1", "cluster1 test");
    cluster.set("cluster2", "cluster2 test");
    String cluster1 = cluster.get("cluster1");
    String cluster2 = cluster.get("cluster2");
    System.out.println(cluster1);
    System.out.println(cluster2);
}
```


