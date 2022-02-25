### 前言
由于Filecoin官方提供的京东云IPFS网关已不能正常工作，并且官方网关的访问速度在中国大陆地区非常地蛮，那么下载FileCoin的证明参数文件将会面临经非常大的难题。

### 解决方案1（推荐）：

通过自建IPFS网关的方法来解决IPFS内容的访问问题

#### 1. 部署IPFS节点
请通过 [[Linux一键部署IPFS节点脚本]] 的方式将IPFS节点部署在FileCoin集群的内网其他机器上。
##### IPFS节点要求
- 
	- 8GiB+ 空闲Ram
	- 360GiB+ 磁盘空间位于 /root/路径，用于在下载IPFS路径时作为缓存
	- 注：此路径仅仅是用于IPFS缓存数据块，储存证明文件本身需要占用容量，如果证明文件和/root/路径处于同一磁盘，请确保有接近500GB的空闲磁盘空间，避免导致Out of Space 问题。

#### 2.启用IPFS的网关外部监听
在IPFS节点机器上执行：
```
ipfs config --json Addresses.Gateway '"/ip4/0.0.0.0/tcp/8080"'
systemctl restart ipfs-daemon
```

此时在该机器的8080端口上将会运行一个具有Web服务器属性的IPFS Gateway ，随后请访问
http://<机器IP（内网/外网均可，外网需要确保已经映射端口>:8080/ 
确认出现 ***404 page not found*** ,即证明网关正常工作。

![](https://gateway.ipns.tech/ipfs/QmfCp1RChd1cWxw8P2drzCGq3xD97NPM9KZ2zSU9UDetVn)

#### 3.用 Lotus-shed 进行证明参数下载
编译lotus-shed：
```
cd ./lotus #Lotus 的编译路径
make lotus-shed
```

**关闭 Miner 和 Worker ，清理旧的证明参数文件。**

用lotus-shed下载新的证明参数：
```
export IPFS_GATEWAY=http://<机器IP（内网/外网均可，外网需要确保已经映射端口>:8080/ipfs/
export GOPROXY=https://goproxy.cn
export LOTUS_PATH=/root/.lotus 
export FIL_PROOFS_PARAMETER_CACHE=/path/to/para_cache #请自行指向
export FIL_PROOFS_PARENT_CACHE=/path/to/parent_cache #请自行指向Lotus 编译路径与扇区大小
export TMPDIR=/root/lotus-miner-data/tmp
./lotus/lotus-shed fetch-params --proving-params 64/32GiB #请自行指定Lotus 编译路径与扇区大小
```
以上命令可以写入shell脚本批量运行。

注：自建的IFPS网关可以用于替换原有的IPFS_GATEWAY，确保集群更加稳定。

### 解决方案2：
#### 1.安装Verysync同步软件
```
curl http://www.verysync.com/shell/verysync-linux-installer/go-installer.sh > go-installer.sh 

chmod +x go-installer.sh

./go-installer.sh
```
[Verysync安装教程原文](https://forum.verysync.com/forum.php?mod=viewthread&tid=906&extra=page%3D1)

#### 2.开始同步
访问 http://<机器IP>:8886/

导入以下Key：
```
B4FWFIV773QVUB2WGR66QANMGISVZ74RVDAO6BLQG32V4ZVHJE6CPA
```

>此Key由本站进行维护
- 选择目标路径到储存证明文件的路径
	![](https://gateway.ipns.tech/ipfs/QmPinzDBNm9MatvqX6xGqB3kVd1kqv2Z7vJaLqZnuDdTHz)
- 调整同步策略到如下图的状态
	![](https://gateway.ipns.tech/ipfs/QmVdCc57XcnzvefUrwu8xQMrNBLzLavBMDQyBuGx4V9jJJ)
	
#### 3.等待同步