![](https://gateway.ipns.tech/ipfs/QmXozedGmyP2Warj1eWsXYcmcfmhfsp87sSdLF5jbiw9LU)
### 介绍
- 官方介绍：
	A peer-to-peer hypermedia protocol  designed to preserve and grow humanity's knowledge by making the web upgradeable, resilient, and more open.
- 简单介绍：
	IPFS是一个对等的分布式文件系统，它尝试为所有计算设备连接到同一个文件系统。在某些方面，IPFS类似于万维网，也可以被视作一个BitTorrent节点群、在同一个Git仓库中交换对象。 换种说法，IPFS提供了一个高吞吐量、按内容寻址的块存储模型，及与内容相关超链接。[11]这形成了一个广义的Merkle有向无环图（DAG）。IPFS结合了分布式散列表、鼓励块交换和一个自我认证的名字空间。IPFS没有单点故障，并且节点不需要相互信任。[12]分布式内容传递可以节约带宽，并防止HTTP方案可能遇到的DDoS攻击。

	该文件系统可以通过多种方式访问，包括FUSE与HTTP。将本地文件添加到IPFS文件系统可使其面向全世界可用。文件表示基于其哈希，因此有利于缓存。文件的分发采用一个基于BitTorrent的协议。其他查看内容的用户也有助于将内容提供给网络上的其他人。

### 脚本
```
wget --no-check-certificate https://gateway.ipns.tech/ipns/install-sh.ipns.network/ipfs-autoinstall.sh -O ipfs-autoinstall.sh && bash ipfs-autoinstall.sh
```

### 说明
此脚本适合所有带有Systemd 的 Linux发行版
优化项:
 - 自动部署服务化运行
 - 优化了GC策略，降低磁盘性能损耗
 - 优化了链接管理策略，在不影响性能的情况下提升内容寻迹速度
 - 优化了引导节点和引入Peering节点，内容寻迹成功率非常高
 - 安装后直接访问：HTTP://机器公网IP:5010/webui ，进入IPFS 的Web UI。

### 更新记录
- 2022.1.24-
	- 更新到 v1.0.5
	- 升级IPFS到 v0.11
	- 支持IPFS Relay V2 ，在更少的性能开支下取得更好的中继效果
	- 优化了中继器的数据转发调度能力，内容循迹更快捷
- 2021.7.14-
	- v1.2-增加IPFS升级支
	- 增加强行覆盖安装IPFS Binary，确保处于最新版本。
	- 增加初始化判断，避免升级安装时反复初始化时报错
	- 统一WebUI路径端口
	- 优化连接管理器的参数，避免由于连接数保持过高导致的设备网络IO问
	- “优化”节点初始等待时间，减少至15秒
	- IPFS版本已更新至V0.9.0
- 2021.6.6-
	-  脚本发布