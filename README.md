# 一键完成 Shadowsocks 的节点获取、测速和使用

### 痛点

你可能曾经这样...

> 搞了个 SS 服务，有多条线路的那种    
> 用了几天发现，不同的时段要用不同的节点，而且网站上的 SS 节点还会不定期的变化    
> 所以每次要到网站上看下节点变化了没有    
> 还要测试这些节点哪个最快    
> 还要将节点配置同步到路由器或者客户端上    

于是每次上网没花多少时间，折腾 SS 节点倒是浪费了很多时间

### 解决

把这些繁琐操作交给工具去完成吧，让它帮你

1. 从SS服务提供商网站(或其他形式的**来源**)获取节点配置
2. 对节点进行ping测试，并根据响应速度和丢包率对节点进行评分
3. 将节点按评分结果排序，并部署到路由器、SS客户端等**目标**

## 如何开始

1. 安装 Python 2.7.x，并安装所需的 Python 依赖库 `requests`, `pyping`

	可以使用 pip 快速安装依赖库

		pip install requests, pyping

	以及其他可选的依赖库
	
	* `tabulate` 用于以纯文本表格的方式输出节点信息
	* `paramiko` 用于 SSH 操作(部署到极路由)

2. 通过复制 `ssnd.config.example` 来创建并编辑自己的配置 `ssnd.config`，内含具体说明

3. 编写 `main.py` ，从 `source` 导入 Shadowsocks 节点**来源**，并从 `target` 导入部署**目标**，例如：

		from sources import CloudSS
		from targets import HiWiFi

5. 使用 `deploy(source, target)` 函数进行部署

		deploy(CloudSS, HiWiFi)
		
	或亲自编写代码来实现自定义需求

6. 运行 `main.py`，开始部署

		python main.py

## 当前支持

> 截止目前，仅支持以下**来源**和**目标**，因为这些是自己在用或用过的，而非变相推广  
> 所以一起完善吧，让它支持更多来源和目标

当前支持的 **来源**

* cloudss.net
* gogovpn.org
* ishadowsocks.com

当前支持的 **目标**

* 安装有SS插件的极路由 (插件安装 http://ss.gogovpn.org/ss.sh)
* 极玩路由器，或安装有极玩固件的的其他路由器 (详见 http://www.geewan.com)
* shadowsocks-libev，目前仅支持 OS X 平台
* 以纯文本表格的方式输出节点信息

## 一起完善

欢迎提交 pull request 来支持更多**来源**和**目标**


