# 数据库

## 1. 数据库系统概述

<details open>
  <summary>数据库, 数据库管理系统, 数据库系统</summary>
  <p>数据库: 关联的数据集合</p>
  <p>数据库管理系统: 管理数据</p>
  <p>数据库系统: 以上两个组合</p>
</details>

<details open>
  <summary>文件系统缺点</summary>
  <p>冗余度大, 共享性差, 数据不一致, 结构化程度低</p>
</details>

<details open>
  <summary>数据库系统特点</summary>
  <p>与程序独立, 支持视图, 可控冗余, 支持共享, 可授权, 完整性约束</p>
</details>

<details open>
  <summary>数据抽象与数据库三种模式</summary>
  <p>视图抽象 --> 外模式 -> 概念抽象 --> 概念模式 -> 物理抽象 --> 内模式</p>
</details>

<details open>
  <summary>基于对象的数据模型</summary>
  <p>实体-联系模型, 面向对象模型</p>
</details>

<details open>
  <summary>基于记录的数据模型</summary>
  <p>关系数据模型, 网络数据模型, 层次数据模型</p>
</details>

<details open>
  <summary>物理数据模型</summary>
  <p>关系数据模型, 网络数据模型, 层次数据模型</p>
</details>

<details open>
  <summary>数据库模式</summary>
  <p>结构定义</p>
</details>

<details open>
  <summary>数据库实例</summary>
  <p>特定时刻存储的数据</p>
</details>

<details open>
  <summary>数据库子语言</summary>
  <p>定义子语言: 定义</p>
  <p>操纵子语言: 除定义外的管理</p>
</details>

<details open>
  <summary>数据库管理系统结构</summary>
  <p>数据定义语言编译执行 -> 安全检查</p>
  <p>查询预处理 -> 安全检查 -> 完整性约束</p>
  <p>查询优化处理 -> 算法</p>
  <p>数据操纵语言预编译 -> 算法</p>
  <p>记录管理 => 并发控制, 数据恢复, 缓冲处理, 数据存取</p>
</details>

## 2. 关系数据库系统

<details open>
  <summary>关系代数</summary>
  <p>并: (SELECT * FROM t1, t2)</p>
  <p>差</p>
  <p>笛卡尔积: (SELECT * FROM t1) UNION (SELECT * FROM t2)</p>
  <p>投影: (SELECT A, B FROM t1)</p>
  <p>选择: (SELECT * FROM t1 WHERE ...)</p>
  <p>交: (SELECT * FROM t1) INNER JOIN (SELECT * FROM t2)</p>
  <p>连接: 笛卡尔积 -> 选择</p>
  <p>自然连接: 笛卡尔积 -> (right join on ...)</p>
</details>

<details open>
  <summary>运算关系安全性</summary>
  <p>没有无限关系、无穷验证</p>
</details>

## 3. 数据库安全性与完整性

不允许受到恶意侵害或未授权修改, 数据始终满足语义约束

<details open>
  <summary>安全性</summary>
  <p>口令, 授权, 加密, 防止微数据推导</p>
</details>

<details open>
  <summary>完整性</summary>
  <p>隐含约束: 定义的约束</p>
  <p>状态约束: 值域, 唯一性, 联系</p>
  <p>变迁约束: 值变的过程</p>
  <p>显式约束: 编写的断言和程序控制的</p>
</details>

## 4. 数据库设计概述与需求分析

对某应用领域, 设计优化的数据库逻辑和物理结构, 使之满足用户要求

<details open>
  <summary>数据库设计</summary>
  <p>需求分析, 定义支持的信息、应用、 操作、 数据项, 预测未来改变</p>
</details>

## 5. 概念数据库设计

分析需求得出数据模型(如实体联系模型 ER, 扩展实体联系模型 EER)

<details open>
  <summary>实体型, 实体模式, 实体</summary>
  <p>实体型: 由实体模式定义</p>
  <p>实体模式: 实体型的定义(数据库模式)</p>
  <p>实体: 实体型的实例简称(元组, 对应数据库的一行数据)</p>
</details>

<details open>
  <summary>联系型</summary>
  <p>不同键间 M个 对 N个 , M:N 的联系</p>
</details>

<details open>
  <summary>联系型实体关联约束</summary>
  <p>全域关联约束: 子类综合即超类</p>
  <p>部分关联约束: 子类综合小于超类</p>
</details>

<details open>
  <summary>演绎, 归纳</summary>
  <p>演绎: 超类 -> 子类</p>
  <p>归纳: 子类 -> 超类</p>
</details>

## 6. 逻辑数据库设计

规范化, 模式优化, 性能估计

<details open>
  <summary>函数依赖</summary>
  <p>完全函数依赖: 若给出 AB->Z, 则只有 AB->Z</p>
  <p>部分函数依赖: 若给出 AB->Z, 则还有A->Z或B->Z</p>
</details>

<details open>
  <summary>主键, 候选键, 全键, 外键</summary>
  <p>主键: 候选键中选出的一组</p>
  <p>候选键: 唯一性, 最小性</p>
  <p>全键: 所有属性都是候选键</p>
  <p>外键: 另一个关系的候选键</p>
</details>

<details open>
  <summary>Armstrong推理</summary>
  <p>合并, 伪传递, 分解</p>
  <p>(综合讲就是对AB->Z左边各种推理子集的传递替换)</p>
</details>

<details open>
  <summary>闭包</summary>
  <p>F = {AB -> C, C -> D}, A+ = {AB, C, D}: (Armstrong推理中出现的每一个未拆分量都存在于推理源的闭包)</p>
</details>

<details open>
  <summary>最小函数依赖集</summary>
  <p></p>
</details>

<details open>
  <summary>范式 Normal Form</summary>
  <p>1NF: 属性都是简单属性</p>
  <p>2NF: 1NF 且 没有部分依赖主键</p>
  <p>3NF: 2NF 且 没有传递依赖</p>
</details>

<details open>
  <summary>无损连接, 依赖保持</summary>
  <p>无损连接: 联系型自然连接后恢复为原始信息</p>
  <p>依赖保持: 不丢失原有的函数依赖关系</p>
</details>

<details open>
  <summary>3NF分解</summary>
  <p></p>
</details>

<details open>
  <summary>关系模式优化</summary>
  <p>水平分解(多表同模式), 垂直分解(范式)</p>
</details>

## 7. 物理数据库设计

选取合适的物理存储结构, 方法

## 12. 并发控制技术

<details open>
  <summary>事务原子性被破坏因素</summary>
  <p>多事务并发, 不同事物操作交叉: 需保证交叉运行的事务对原子性无影响</p>
  <p>事务运行中被终止: 需保证终止的事务证对数据和其它事务无影响</p>
</details>

<details open>
  <summary>事务状态</summary>
  <p>活动状态 -> 部分提交状态 -> 提交状态</p>
  <p>活动状态 -> 失败状态 -> 异常结束状态</p>
  <p>部分提交状态 -> 失败状态</p>
</details>

<details open>
  <summary>事务性质</summary>
  <p>原子性Atomicity</p>
  <p>数据库正确保持性Consistency</p>
  <p>操作结果永久保持性Durability</p>
  <p>独立性Isolation</p>
  <p>可串行性Serializability</p>
</details>

<details open>
  <summary>锁类型</summary>
  <p>共享锁, 互斥锁</p>
</details>

<details open>
  <summary>两段锁协议</summary>
  <p>加锁: 可申请获得任何项的任何锁, 但不能释放</p>
  <p>解锁: 可释放获得的任何项的任何锁, 但不能申请</p>
</details>

<details open>
  <summary>树协议</summary>
  <p>有向无环树形图, 只能加 X 锁. 父节点被事务 T 加锁后才能由 T 向子节点加锁, 由事务 T 加锁解锁后不能再由 T 加锁</p>
</details>

<details open>
  <summary>多版本并发控制技术</summary>
  <p>多版本时间印协议</p>
</details>

<details open>
  <summary>多粒度锁协议</summary>
  <table>
    <tr>
      <th></th>
      <th>S</th>
      <th>X</th>
      <th>IS</th>
      <th>IX</th>
      <th>SIX</th>
    </tr>
    <tr>
      <th>S</th>
      <td>1</td>
      <td>x</td>
      <td>1</td>
      <td>x</td>
      <td>x</td>
    </tr>
    <tr>
      <th>X</th>
      <td>x</td>
      <td>x</td>
      <td>x</td>
      <td>x</td>
      <td>x</td>
    </tr>
    <tr>
      <th>IS</th>
      <td>1</td>
      <td>x</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>IX</th>
      <td>x</td>
      <td>x</td>
      <td>1</td>
      <td>1</td>
      <td>x</td>
    </tr>
    <tr>
      <th>SIX</th>
      <td>x</td>
      <td>x</td>
      <td>1</td>
      <td>x</td>
      <td>x</td>
    </tr>
  </table>
</details>

<details open>
  <summary>日志恢复技术</summary>
  <p>推迟更新技术: 先把新值写日志, 统一更新</p>
  <p>即时更新技术: 先把事务写日志, 成功后立即更新</p>
</details>

<details open>
  <summary>缓冲技术</summary>
  <p>日志缓冲</p>
  <p>数据库缓冲</p>
</details>

<details open>
  <summary>检测点</summary>
  <p>只需找最近的检测点开始恢复</p>
</details>

<details open>
  <summary>影子页面技术</summary>
  <p>事务开始时: 页面产生两个副本, 影子页 + 当前页</p>
  <p>事务执行时: 操作当前页, 若成功, 修改索引指向到当前页, 否则指向原页</p>
</details>

<details open>
  <summary>可恢复调度</summary>
  <p>任何情况都能保证数据库正确恢复的调度</p>
  <p>若一个事务读取一个被更新的数据项, 更新数据项的事务必须已提交</p>
  <table>
    <tr>
      <th>T1</th>
      <th>T2</th>
    </tr>
    <tr>
      <td>READ(A)</td>
    </tr>
    <tr>
      <td>WRITE(A)</td>
    </tr>
    <tr>
      <td></td>
      <td>READ(A)</td>
    </tr>
    <tr>
      <td>READ(B)</td>
      <td></td>
      <td>若T1失败, 嵌套撤销</td>
    </tr>
  </table>
  <p>可设提交位, T1提交后才可读, 否则等待</p>
</details>

<details open>
  <summary>一维数据划分</summary>
  <p>Round-Robin: i mod N</p>
  <p>Hash</p>
  <p>Range: 将某一属性分为 N 个值域区间, 实例分 N 份按区间存储</p>
  <p>Hybrid-Range: Range + Round-Robin</p>
</details>

<details open>
  <summary>查询优化</summary>
  <p>基于左线性树</p>
  <p>基于右线性树</p>
</details>

### 21. 数据仓库与联机分析处理技术

<details open>
  <summary>多维数据集合的关系表示方法</summary>
  <p>星形模式 Star schema: 单级索引</p>
  <p>雪花模式 Snowflake schema: 多级索引</p>
</details>

### 22. 数据挖掘技术

<details open>
  <summary>Apriori</summary>
  <p></p>
</details>

<details open>
  <summary>k-means</summary>
  <p></p>
</details>

## APPENDIX

### 1. 无损连接判断

### 2. 3NF 分解

R<U, F>

U = { A, B, C, D, E, F, G, H }

F = { A->CGH, AD->C, DE->F, G->H }

1. 若 F 中存在依赖 X->A 使 U 与集合{ X, A }相同, 原 R 加到结果集, 直接跳到 5 步

- 此例没有

2. 求最小函数依赖集 G

- 将依赖确定分解为单属性

  F = { A->C, A->G, A->H, AD->C, DE->F, G->H }

- 去除冗余依赖

  若去除 A->C, F = { A->G, A->H, AD->C, DE->F, G->H }. 因 F 中不存在 A+->C, 得 A->C 不冗余

  > A->G, A->H => A+ = { A, G, H }

  若去除 A->G, F = { A->C, A->H, AD->C, DE->F, G->H }. 因 F 中不存在 A+->G, 得 A->G 不冗余

  > A->C, A->H => A+ = { A, C, H }

  若去除 A->H, F = { A->C, A->G, AD->C, DE->F, G->H }. 因 F 中存在 A+->H, 去除 A->H

  > A->C, A->G->H, A+ = { A, C, G, H }

  若去除 AD->C, F = { A->C, A->G, DE->F, G->H }. 因 F 中存在 (AD)+->C, 去除 AD->C

  > A->C, A->G->H, (AD)+ = { A, C, D, G, H }

  若去除 DE->F, F = { A->C, A->G, G->H }. 因 F 中不存在 (DE)+->F, 得 DE->F 不冗余

  > (DE+) = { D, E }

  若去除 G->H, F = { A->C, A->G, DE->F }. 因 F 中不存在 G+->H, 得 G->H 不冗余

  > G+ = { G }

- 去除依赖左部冗余. 以上得 F = { A->C, A->G, DE->F, G->H }

  - DE->F:

    若去除 D, F = { A->C, A->G, E->F, G->H }, 因 F 中不存在 D+->F, 得 D 不冗余

    若去除 E, F = { A->C, A->G, D->F, G->H }, 因 F 中不存在 E+->F, 得 E 不冗余

- 以上得最小依赖集 G = { A->C, A->G, DE->F, G->H }

3. 将每个 G 中没有而 F 中有的依赖中的属性关系加到结果集

- 此例没有

4. 将每个 G 中的依赖关系加到结果集 (至此结果集为依赖保持的 3NF)

- 此时结果集为 { R(A, C), R(A, G), R(D, E, F), R(G, H) }

5. 添加一个关系 R(X, A) 到结果集, 满足 { X, A } 是原 R 的一个候选键

- 这里设取候选键 DE, 此时结果集为 { R(A, C), R(A, G), R(D, E, F), R(G, H), R(D, E) }

  > 原 R 从 F 中看出的候选键有 A, AD, DE, G.

6. 若存在 R1<=R2, 去除 R1 (至此结果集为依赖保持且无损连接的 3NF)

- 因 R(D, E) <= R(D, E, F), 去除 R(D, E). 结果集为 { R(A, C), R(A, G), R(D, E, F), R(G, H) }

### 3. 可串行性测试

调度 S 的事务集 { T1, T2, T3 }

| 时间 |    T1    |    T2    |    T3    |
| :--: | :------: | :------: | :------: |
|  ↓   | READ(Q)  |          |          |
|  ↓   |          | WRITE(Q) |          |
|  ↓   |          |          | READ(Q)  |
|  ↓   | WRITE(Q) |          |          |
|  ↓   |          |          | WRITE(Q) |

1. 构造 S 前趋图

- S 化为 S"

  - S 中加两个附加事务 Tb, Tf. Tb 作第一个, Tf 作最后一个

    | Tb  |    T1    |    T2    |    T3    | Tf  |
    | :-: | :------: | :------: | :------: | :-: |
    | op  |          |          |          |     |
    |     | READ(Q)  |          |          |     |
    |     |          | WRITE(Q) |          |     |
    |     |          |          | READ(Q)  |     |
    |     | WRITE(Q) |          |          |     |
    |     |          |          | WRITE(Q) |     |
    |     |          |          |          | op  |

  - 对事务集中存取的每个 Q, Tb 包含一个 WRITE(Q), Tf 包含一个 READ(Q)

    由于只有 Q

    |    Tb    |    T1    |    T2    |    T3    |   Tf    |
    | :------: | :------: | :------: | :------: | :-----: |
    | WRITE(Q) |          |          |          |         |
    |          | READ(Q)  |          |          |         |
    |          |          | WRITE(Q) |          |         |
    |          |          |          | READ(Q)  |         |
    |          | WRITE(Q) |          |          |         |
    |          |          |          | WRITE(Q) |         |
    |          |          |          |          | READ(Q) |

- 构造 S" 的标号前趋图

  - 若 Tj 读取 Ti 写的 Q, 加一条标记 0 的边: Ti -> 0 -> Tj

    即 READ 紧跟 WRITE 时

    Tb -> 0 -> T1, T2 -> 0 -> T3, T3 -> 0 -> Tf

  - 当且仅当不存在 Ti 到 Tf 的路径(且 i != b)时, 去掉连接 Ti 的边

    由于存在 T3 -> 0 -> Tf, 不去掉连接 T3 的边

  - 若有 Tj 读取 Ti 写的 Q, Tk 执行 WRITE(Q), 那么对 Tk 不是 Tb 的每一项 Q

    - 若 Ti = Tb 且 Tj != Tf, 加入边 Tj -> 0 -> Tk

      即 Tb 紧接的后一个非 Tf 的读取 Tb 写的 Q

      即 T1 读 Tb, j = 1

      由表知 T2, T3 都有 WRITE, 加入这两个 k : T1 -> 0 -> T2, T1 -> 0 -> T3

    - 若 Ti != Tb 且 Tj = Tf, 加入边 Tk -> 0 -> Ti

      即 Tf 读取 Tf 紧接的前一个非 Tb 的写的 Q

      即 Tf 读 T3, i = 3

      由表知 T1, T2 都有 WRITE, 加入这两个 k : T1 -> 0 -> T3, T2 -> 0 -> T3

    - 若 Ti != Tb 且 Tj != Tf, 加入边 Tj -> p -> Tk 和 Tk -> p -> Ti. 其中 p 是大于 0 且没做过边标号的正整数

      即不看事务 Tb, Tf

      因有 T2 -> 0 -> T3, 且 T1 有 WRITE, j = 3, i = 2, k = 1

      加入边 T3 -> 1 -> T1, T1 -> 1 -> T2

2. 回路测试算法测前趋图是否有回路

- 最终边有

  Tb -> 0 -> T1

  T1 -> 0 -> T2

  T2 -> 0 -> T3

  T3 -> 0 -> Tf

  T1 -> 0 -> T3

  T1 -> 1 -> T2

  T3 -> 1 -> T1

3. 若没有回路, S 是冲突可串行, 否则不是

- 没有回路, S 冲突可串行
