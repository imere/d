# 网络

## 1. 概述

<details open>
  <summary>交换</summary>
  <p>电路交换: 比特流连续到终点</p>
  <p>报文交换: 先到相邻结点, 查转发表到下一结点</p>
  <p>分组交换: 单个分组先到相邻结点, 存储后查转发表到下一结点</p>
</details>

<details open>
  <summary>网络体系结构</summary>
  <table>
    <tr>
      <th>OSI</th>
      <th>TCP/IP</th>
      <th>Five Layer</th>
    </tr>
    <tr>
      <td>Application</td>
      <td rowspan="3">Application</td>
      <td rowspan="3">Application</td>
    </tr>
    <tr>
      <td>Presentation</td>
    </tr>
    <tr>
      <td>Session</td>
    </tr>
    <tr>
      <td>Transport</td>
      <td>Transport</td>
      <td>Transport</td>
    </tr>
    <tr>
      <td>Network</td>
      <td>Internet</td>
      <td>Network</td>
    </tr>
    <tr>
      <td>Data Link</td>
      <td rowspan="2">Network Access</td>
      <td>Data Link</td>
    </tr>
    <tr>
      <td>Physical</td>
      <td>Physical</td>
    </tr>
  </table>
</details>

## 2. 物理层

<details open>
  <summary>任务</summary>
  <p>机械特性</p>
  <p>电气特性</p>
  <p>功能特性</p>
  <p>过程特性</p>
</details>

<details open>
  <summary>编码方式</summary>
  <p>不归零</p>
  <p>归零</p>
  <p>曼彻斯特</p>
  <p>差分曼彻斯特</p>
</details>

<details open>
  <summary>信道复用</summary>
  <p>频分复用FDM</p>
  <p>时分复用TDM</p>
  <p>波分复用WDM: 光的频分复用</p>
  <p>码分复用CDM</p>
</details>

<details open>
  <summary>非对称数字用户线ADSL</summary>
  <p>用数字技术改造模拟电话用户线</p>
</details>
</details>

<details open>
  <summary>FTTx</summary>
  <p></p>
</details>

## 3. 数据链路层

PPP, MAC

<details open>
  <summary>链路</summary>
  <p>一结点到相邻结点的物理线路</p>
</details>

<details open>
  <summary>数据链路</summary>
  <p>物理线路 + 实现通信协议的软硬件</p>
</details>

<details open>
  <summary>封装成帧</summary>
  <p>帧首部 + 帧数据(<=MTU) + 帧尾部</p>
  <p>首尾用帧定界符</p>
</details>

<details open>
  <summary>透明传输</summary>
  <p>转义帧数据中的定界符: 字节填充/字符填充</p>
</details>

<details open>
  <summary>差错检测</summary>
  <p>循环冗余校验CRC</p>
</details>

<details open>
  <summary>CSMA/CD</summary>
  <p></p>
</details>

<details open>
  <summary>PPP协议帧</summary>
  <p>7E(1) + FF(1) + 03(1) + 协议(2) + 数据(<=1500) + FCS(2) + 7E(1)</p>
  <p>字节填充</p>
  <p>0x7E -> 0x7D + 0x5E</p>
  <p>0x7D -> 0x7D + 0x5D</p>
  <p>q < 0x20 -> 0x7D + 0x2q</p>
  <p>零比特填充</p>
</details>

<details open>
  <summary>Ethernet V2 MAC协议帧</summary>
  <p>MAC地址: 组织唯一标识符OUI(3) + 扩展标识符EI(3)</p>
  <p>帧格式: 前同步码(7) + 帧开始定界符(1) + 目的地址(6) + 源地址(6) + 类型(2) + 数据(46~1500) + FCS(4)</p>
</details>

<details open>
  <summary>虚拟局域网</summary>
  <p>MAC源地址后插入VLAN标记(4)</p>
  <p>VLAN标记 -> 802.1Q标记类型(2) + 标记控制信息(2)</p>
</details>

## 4. 网络层

IP

向上只提供简单灵活, 无连接, 尽最大努力交付的数据报服务, 即不提供 QoS 承诺

<details open>
  <summary>网际协议IP</summary>
  <p>VLAN标记 -> 802.1Q标记类型(2) + 标记控制信息(2)</p>
</details>

<details open>
  <summary>中间设备</summary>
  <p>转发器: 物理层</p>
  <p>网桥/桥接器: 数据链路层</p>
  <p>路由器: 网络层</p>
  <p>网关: 网络层以上</p>
</details>

<details open>
  <summary>虚拟互联网络</summary>
  <p>使用(IP)协议 使性能各异的网络 在网络层看起来像是一个统一的网络</p>
</details>

<details open>
  <summary>IPv4数据报格式</summary>
  <p>首部(20~60) + 数据</p>
</details>

<details open>
  <summary>IPv6数据报格式</summary>
  <p>首部(40) + 有效载荷(<=65535)</p>
</details>

<details open>
  <summary>划分子网</summary>
  <p>增加灵活性, 减少主机数</p>
  <p>IP -> 网络号 + 地址号 + 主机号</p>
</details>

<details open>
  <summary>无分类编址CIDR(超网 -> 同CIDR包多个C类地址)</summary>
  <p>增加灵活性, 减少主机数</p>
  <p>IP -> 网络前缀 + 主机号</p>
</details>

<details open>
  <summary>路由选择协议</summary>
  <p>内部网关协议IGP: RIP->距离向量路由协议, OSPF->链路状态协议</p>
  <p>外部网关协议EGP: BPG->路径向量路由协议</p>
</details>

## 5. 运输层

TCP, UDP

为相互通信的应用进程提供逻辑通信

<details open>
  <summary>用户数据报协议UDP</summary>
  <p>面向报文</p>
  <p>[伪首部 +] 源端口(2) + 目的端口(2) + 长度(2) + 检验和(2) + 数据</p>
  <p>伪首部(只用于检验和计算) -> 源IP(4) + 目的IP(4) + 0(1) + 17(1) + UDP长度(2)</p>
</details>

<details open>
  <summary>套接字socket</summary>
  <p>(IP:port)</p>
</details>

<details open>
  <summary>传输控制协议TCP</summary>
  <p>面向连接</p>
</details>

<details open>
  <summary>停止等待协议</summary>
  <p>无差错: A 发送 M1 后, B 收到 M1, A 收到 B 的 M1 确认, A 继续发送 M2</p>
  <p>有差错: A 发送 M1 后, B 没收到 M1, A 没收到 B 的 M1 确认, A 超时重传 M1</p>
</details>

<details open>
  <summary>自动重传请求ARQ</summary>
  <p>确认丢失: A 发送 M1 后, B 收到 M1, A 没收到 B 的 M1 确认, A 超时重传 M1, B 丢弃重复的 M1, A 收到 B 重传的 M1 确认</p>
  <p>确认迟到: A 发送 M1 后, B 收到 M1, A 没收到 B 的 M1 确认, A 超时重传M1, B 丢弃重复的 M1, A 收到 B 重传的 M1 确认, A 收到 B 迟到的 M1 确认, 忽略迟到确认</p>
</details>

<details open>
  <summary>TCP拥塞避免</summary>
  <p>慢开始: cwnd <= ssthresh, 发送窗口=cwnd, 从小逐渐增大发送窗口和拥塞窗口, 每一个RTT使cwnd x 2</p>
  <p>拥塞避免: cwnd >= ssthresh, 每一个RTT使cwnd + 1. 出现超时使ssthresh / 2, 执行慢开始</p>
  <p>快重传: 发送方连收三个相同 M 确认, 得知接收方没有收到 M, 立即重传 M</p>
  <p>快恢复: 发送方得知接收方没有收到个别报文, cwnd = ssthresh = cwnd / 2, 执行拥塞避免</p>
</details>

## 6. 应用层

TCP: BGP, FTP, TELNET, HTTP, SMTP

UDP: RIP, TFTP, DNS, DHCP, SNMP

<details open>
  <summary>信息检索系统</summary>
  <p>全文检索</p>
  <p>分类目录检索</p>
</details>

## 7. 网络安全

<details open>
  <summary>数字签名</summary>
  <p>私钥签名公钥验证</p>
</details>

<details open>
  <summary>SSL 过程</summary>
  <p>协商加密算法: A 给 B 可选加密算法, B 选一个回复</p>
  <p>服务器鉴别: B 给 A 数字签名的公钥, A 用 CA 的公钥验证确实是 B 签名的</p>
  <p>会话秘钥计算: A 产生对称秘钥, 用 B 的 公钥加密后给 B, B 用加密报文指出握手完成</p>
  <p>开始安全传输</p>
</details>

## 8. 互联网音视频服务

万维网服务器 -> 元文件 -> 播放器 -> 万维网服务器/媒体服务器

<details open>
  <summary>时延抖动</summary>
  <p></p>
</details>

<details open>
  <summary>实时流协议RTSP</summary>
  <p>控制流传送</p>
</details>

<details open>
  <summary>实时运输协议RTP</summary>
  <p>端到端运输, 不提供QoS</p>
</details>

<details open>
  <summary>实时运输控制协议RTCP</summary>
  <p>监视反馈QoS, 媒体同步</p>
  <p>接收端报告分组RR: 两端了解状态, 调整速率</p>
  <p>发送端报告分组SR: 产生的分组时间戳, 绝对时钟</p>
</details>

<details open>
  <summary>调度机制</summary>
  <p>先进先出FIFO</p>
  <p>加权公平排队WFQ</p>
</details>

<details open>
  <summary>资源预留协议RSVP</summary>
  <p>PATH</p>
  <p>RESV</p>
  <p>(PATH询问, RESV响应, 保留最小流量值)</p>
</details>

## 9. 无线网络和移动网络

<details open>
  <summary>CSMA/CA协议</summary>
  <p>隐蔽站问题: 没检测到其他站, 发生碰撞</p>
  <p>暴露站问题: 检测到其他站, 不敢发送</p>
  <p>源站准备发第一个MAC帧时, 若检测到空闲, 等待DIFS(128us), 若没有高优先的帧发送, 开始发送, 否则让高优先发送. 目的站收到后, 等待SIFS(28us), 返回确认帧ACK, 若源站超时没收到ACK, 源站重传, 直到收到ACK或放弃.</p>
  <p>若不是第一个帧, 等待DIFS后还要执行二进制指数退避</p>
</details>

## APPENDIX

1. 距离向量算法

- 对地址为 X 的相邻路由器发来的 RIP 报文, 修改使下一跳地址为 X, 距离加 1. 得到报文: 目的网络 N, 距离 d, 下一跳 X

- 若原来路由表没有 N, 把项目加到路由表

  - 否则若下一跳路由地址是 X, 更新路由表

    - 否则若收到的 d 小于路由表中的, 更新路由表

      - 否则什么也不做

- 若 3min 还没收到相邻路由器的更新路由表, 把此相邻路由器标记为不可达

- 返回
