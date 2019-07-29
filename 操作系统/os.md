# 操作系统

## 1. 引论

<details open>
  <summary>未配置操作系统的计算机系统</summary>
  <p>人工操作方式</p>
  <p>脱机输入输出方式</p>
</details>

<details open>
  <summary>批处理系统</summary>
  <p>在一个监督程序控制下对一批作业自动处理</p>
</details>

<details open>
  <summary>单道批处理系统</summary>
  <p>内存只能存放一道作业的批处理系统</p>
  <p>缺点: 不能充分利用资源</p>
</details>

<details open>
  <summary>多道批处理系统</summary>
  <p>采用多道程序设计技术的批处理系统</p>
  <p>多道程序设计技术: 内存存放若干作业, 共享资源, (宏观)同时运行</p>
</details>

<details open>
  <summary>分时系统</summary>
</details>

<details open>
  <summary>实时系统</summary>
  <p>常采用多级容错</p>
  <p>实时任务: 硬实时任务, 软实时任务</p>
</details>

<details open>
  <summary>微机操作系统</summary>
  <p>配置在微型机的系统</p>
</details>

<details open>
  <summary>操作系统基本特征</summary>
  <p>并发性: 多事件同时发生</p>
  <p>共享性: 互斥共享, 同时访问: 资源可供多个并发进程同时使用</p>
  <p>虚拟性: 将物理实体变为若干逻辑对应物</p>
  <p>异步性: 多道环境下, 程序执行时间不可预知, 但结果可再现</p>
</details>

<details open>
  <summary>操作系统的功能</summary>
  <p>处理机管理</p>
  <p>存储器管理</p>
  <p>设备管理</p>
  <p>文件管理</p>
  <p>友好用户接口</p>
  <p>现代操作系统新功能: 安全, 网络, 多媒体</p>
</details>

<details open>
  <summary>操作系统结构</summary>
  <p>无结构</p>
  <p>模块化结构</p>
  <p>分层式结构</p>
  <p>微内核结构</p>
</details>

<details open>
  <summary>操作系统结构</summary>
  <p>无结构</p>
  <p>模块化结构</p>
  <p>分层式结构: 按规则分若干层, 规定单向调用关系</p>
  <p>微内核结构: C/S模式 -> 基本功能内核 + 服务</p>
</details>

## 2. 进程的描述与控制

<details open>
  <summary>进程实体</summary>
  <p>PCB + 程序段 + 相关数据段</p>
</details>

<details open>
  <summary>进程创建</summary>
  <p>从PCB集合申请空闲PCB, 分配内存和资源, 初始化后插入就绪队列</p>
</details>

<details open>
  <summary>进程终止</summary>
  <p>找到要终止的进程的PCB, 终止执行, 终止子孙进程, 释放资源, 移出队列, 回收PCB</p>
</details>

<details open>
  <summary>进程阻塞, 唤醒</summary>
  <p>停止执行, 将PCB插入到阻塞队列, 调度程序重新调度, 等待的事件完成时, 将PCB插入就绪队列</p>
</details>

<details open>
  <summary>进程挂起</summary>
  <p>若阻塞, 状态转换为静止阻塞, 否则转为静止就绪, 将PCB复制到指定内存区待考察</p>
  <p>若正在执行, 调度程序重新调度</p>
</details>

<details open>
  <summary>进程激活</summary>
  <p>若静止阻塞, 状态转换为活动阻塞, 否则转为活动就绪</p>
</details>

<details open>
  <summary>进程通信</summary>
  <p>共享存储器</p>
  <p>管道: 共享文件</p>
  <p>消息传递: 格式化消息</p>
  <p>C/S: 套接字, RPC</p>
</details>

<details open>
  <summary>线程</summary>
  <p>可执行实体, 基本不拥有资源 -> 创建不需另行分配, 终止不需回收, 减少了切换保存恢复的现场信息</p>
</details>

## 3. 处理机调度与死锁

<details open>
  <summary>调度层次</summary>
  <p>高级调度/作业调度</p>
  <p>低级调度/进程调度: 抢占方式, 非抢占方式</p>
  <p>中级调度/内存调度</p>
</details>

<details open>
  <summary>进程调度算法</summary>
  <p>优先级调度PSA -> 静态优先权, 动态优先权</p>
  <p>高响应比优先调度HRRN -> 计算响应比</p>
  <p>时间片轮转RR -> FIFO排队, 一次最多连续执行一个时间片, 未完成则转到队尾</p>
  <p>多级队列调度 -> 分不同类型队列, 队列间固定优先权抢占</p>
  <p>多级反馈队列调度FB -> 分不同级数队列, 系统从第一级开始FCFS, 直到当前和之前级为空才到下一级. 若当前级某进程未在有限时间片完成则转入下一级末尾. 最后一级队列执行RR</p>
</details>

<details open>
  <summary>实时调度算法</summary>
  <p>最早截止时间优先EDF</p>
  <p>最低松弛度优先LLF -> (根据每个任务宽裕度)</p>
</details>

<details open>
  <summary>死锁条件</summary>
  <p>互斥条件: 资源必须互斥使用</p>
  <p>请求与保持条件: 申请新资源时不释放已有资源</p>
  <p>不剥夺条件: 已有资源不能被抢占</p>
  <p>环路等待条件: 一个有两个及以上进程的等待链, 每个进程都等待下一个进程占的资源</p>
</details>

<details open>
  <summary>预防死锁</summary>
  <p>摒弃请求与保持条件: 开始只申请运行初所需资源, 申请新资源前必须逐步释放已有资源</p>
  <p>摒弃不剥夺条件: 已有资源不够又申请不到时必须释放已有资源</p>
  <p>摒弃环路等待条件: 进程按序编号, 只能按编号顺序申请资源</p>
</details>

<details open>
  <summary>避免死锁</summary>
  <p>安全性算法</p>
  <p>银行家算法</p>
</details>

## 4. 存储器管理

<details open>
  <summary>程序装入</summary>
  <p>绝对装入</p>
  <p>可重定位装入/静态重定位</p>
  <p>动态运行时装入</p>
</details>

<details open>
  <summary>程序链接</summary>
  <p>静态链接</p>
  <p>装入时动态链接</p>
  <p>运行时动态链接</p>
</details>

<details open>
  <summary>连续分配方式</summary>
  <p>单一连续分配 -> 系统区 + 用户区, 只有一道作业</p>
  <p>固定分区分配 -> 固定分区说明表</p>
  <p>动态分区分配: 首次适应, 循环首次适应, 最佳适应, 最坏适应</p>
  <p>伙伴系统 -> 可分配内存块大小范围为 2^L~2^U, 进程申请K字节, 若 2^L < K <= 2^U, 将整块都分配给进程, 否则划为相等两块2^(U-1), 若 2^(U-2) < K <= 2^(U-1), 分配两块中的一块, 否则其中一块再分为相等两块, 继续过程直到分配</p>
  <p>动态重定位分区分配 -> 动态分区分配 + 紧凑</p>
</details>

<details open>
  <summary>分页</summary>
  <p>基本地址变换机构</p>
  <p>页表寄存器 -> 页表始址 + 页表长度</p>
  <p>逻辑地址 -> 页号 + 页内地址</p>
  <p>页表始址 + 页号 -> 内存块号</p>
  <p>内存块号 + 页内地址 -> 物理地址</p>
  <p>越界中断</p>
  <p>有快表的地址变换机构</p>
</details>

<details open>
  <summary>分段</summary>
  <p>基本地址变换机构</p>
  <p>控制寄存器 -> 段表始址 + 段表长度</p>
  <p>有效地址 -> 段号 + 位移量</p>
  <p>段表始址 + 段号 -> 段长 + 基址</p>
  <p>基址 + 位移量 -> 物理地址</p>
  <p>越界中断</p>
</details>

## 5. 虚拟存储器

<details open>
  <summary>特征</summary>
  <p>多次性: 一个作业分多次调入内存</p>
  <p>对换性: 暂不使用的程序, 数据从内存暂调至对换区</p>
  <p>虚拟性: 逻辑性的, 不实际存在</p>
</details>

<details open>
  <summary>关键技术</summary>
  <p>请求分页</p>
  <p>请求分段</p>
  <p>页置换</p>
  <p>段置换</p>
</details>

<details open>
  <summary>请求分页原理</summary>
  <p>只将作业部分页面装入内存</p>
  <p>页表机制 -> 内存块号 + 存取访问字段 + 状态位 + 访问字段 + 修改字段 + 外存地址</p>
  <p>地址变换</p>
</details>

<details open>
  <summary>调页策略</summary>
  <p>请求调页: 发现缺页立刻发出缺页中断, 将所需页调入内存</p>
  <p>预调页: 预计不久访问的页预先调入内存, 主要用于首次或整体换入</p>
</details>

<details open>
  <summary>页置换算法</summary>
  <p>最近最久未使用LRU: 淘汰最近最久未使用页面</p>
  <p>页面缓冲池算法PBA: 被换出的页留在内存空闲块, 形成一个空闲页面缓冲池</p>
</details>

## APPENDIX

### 1. 避免死锁

银行家算法资源分配:

| Process |    Max    |  Need   | Available |
| :-----: | :-------: | :-----: | :-------: |
|   P0    |  0 0 4 4  | 0 0 1 2 |  1 6 2 2  |
|   P1    |  2 7 5 0  | 1 7 5 0 |
|   P2    | 3 6 10 10 | 2 3 5 6 |
|   P3    |  0 9 8 4  | 0 6 5 2 |
|   P4    | 0 6 6 10  | 0 6 5 6 |

Allocation = Max - Need

| Process | Allocation |
| :-----: | :--------: |
|   P0    |  0 0 3 2   |
|   P1    |  1 0 0 0   |
|   P2    |  1 3 5 4   |
|   P3    |  0 3 3 2   |
|   P4    |  0 0 1 4   |

安全性检查:

1. 开始时, Work = Available

2. 找到进程 Finish=False 且 Need<=Work

3. 分配后进程可完成时由 False->True, 同时释放资源, 即 Work = Work + Allocation

4. 跳到第 2 步, 存在序列使 Finish 都为 True 时状态安全

|     |   Work   |  Need   | Allocation | Work+Allocation |   Finish    |
| :-: | :------: | :-----: | :--------: | :-------------: | :---------: |
| P0  | 1 6 2 2  | 0 0 1 2 |  0 0 3 2   |     1 6 5 4     | False->True |
| P3  | 1 6 5 4  | 0 6 5 2 |  0 3 3 2   |     1 9 8 6     | False->True |
| P4  | 1 9 8 6  | 0 6 5 6 |  0 0 1 4   |    1 9 9 10     | False->True |
| P1  | 1 9 9 10 | 1 7 5 0 |  1 0 0 0   |    2 9 9 10     | False->True |
| P2  | 2 9 9 10 | 2 3 5 6 |  1 3 5 4   |   3 12 14 14    | False->True |

由步骤知序列应首先依 Need 升序

银行家算法:

若 P2 发出请求 Request(1, 2, 2, 2)

1. Request(1, 2, 2, 2) <= Need(2, 3, 5, 6)

2. Request(1, 2, 2, 2) <= Available(1, 6, 2, 2)

3. 若分配, 则可用减少: Available=Available(1, 6, 2, 2)-Request(1, 2, 2, 2)=(0, 4, 0, 0), P2 得到分配: Allocation=Allocation(1, 3, 5, 4)+Request(1, 2, 2, 2)=(2, 5, 7, 6), P2 需求减少: Need=Need(2, 3, 5, 6)-Request(1, 2, 2, 2)=(1, 1, 3, 4)

4. 进行安全检查, 发现无法进入安全状态
