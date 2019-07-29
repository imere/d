# 组成原理

MM: Main Memory

M: Memory

MAR: Memory Address Register

MDR: Memory Data Register

I/O: Input/Output

CPU: Center Processing Unit

ALU: Arithmetic Logic Unit

ACC: Accumulator

MQ: Multiplier-Quotient Register

CU: Control Unit

MIPS: Million Instructions Per Second

FLOPS: Floating-Point Operations Per Second

RISC: Reduced Instruction Set Computer

CISC: Complex Instruction Set Computer

## 1. 概论

<details open>
  <summary>冯诺依曼结构</summary>
  <p>存储器, 运算器, 控制器, 输入输出设备</p>
</details>

<details open>
  <summary>现代计算机组成</summary>
  <p>主机 + IO</p>
  <p>主机 -> MM + CPU</p>
  <p>CPU -> ALU + CU</p>
</details>

<details open>
  <summary>细化计算机组成</summary>
  <p>CPU + MM + IO</p>
  <p>CPU -> X + ALU + ACC + MQ</p>
  <p>MM -> M + MDR + MAR</p>
</details>

<details open>
  <summary>机器字长</summary>
  <p>CPU一次能处理的数据位数</p>
</details>

<details open>
  <summary>存储容量(单位: 位)</summary>
  <p>存储单元数(2^MAR位数) x 存储字长(MDR位数)</p>
</details>

## 3. 硬件结构

<details open>
  <summary>总线分类</summary>
  <p>片内总线: 芯片内</p>
  <p>系统总线 -> 数据总线, 地址总线, 控制总线</p>
  <p>通信总线: 系统间</p>
</details>

<details open>
  <summary>总线指标</summary>
  <p>宽度: 根数(bit)</p>
  <p>带宽: MHz x (宽度 / 8) = MBps</p>
</details>

<details open>
  <summary>总线结构</summary>
  <p>单总线</p>
  <p>多总线</p>
</details>

<details open>
  <summary>总线判优</summary>
  <p>链式查询: IO串联传递总线使用权</p>
  <p>计数器定时查询: 按计数器当前给出地址给出总线使用权</p>
  <p>独立请求: IO独立请求, 由总线控制部件从队列决定次序</p>
</details>

<details open>
  <summary>总线通信控制</summary>
  <p>同步: 公共时钟</p>
  <p>异步: 不互锁, 半互锁, 全互锁</p>
</details>

<details open>
  <summary>波特率, 比特率</summary>
  <p>波特率: 单位时间传送二进制数据位数 bps</p>
  <p>比特率: 单位时间传送二进制有效数据位数 bps</p>
</details>

## 4. 存储器

<details open>
  <summary>分类</summary>
  <p>主存: RAM + ROM</p>
  <p>辅存: 磁盘 + 光盘 + ...</p>
  <p>闪存</p>
  <p>缓存</p>
</details>

<details open>
  <summary>层次</summary>
  <p>CPU <-> 缓存</p>
  <p>缓存 <-> 主存</p>
  <p>主存 <-> 辅存</p>
  <p>CPU <-> 主存</p>
</details>

<details open>
  <summary>RAM</summary>
  <p>SRAM: 触发器原理. 断电丢数据. 多用于高速缓存</p>
  <p>DRAM: 电容存电荷原理. 不断电信息也会消失, 2ms内必须对所有存储单元刷新一次. 多用于主存</p>
</details>

<details open>
  <summary>缓存-主存地址映射</summary>
  <p>直接映射</p>
  <p>全相联映射</p>
  <p>组相联映射</p>
</details>

## 5. 输入输出系统

<details open>
  <summary>组成</summary>
  <p>软件系统 + 硬件系统</p>
</details>

<details open>
  <summary>IO指令</summary>
  <p>操作码 + 命令码 + 设备码</p>
</details>

<details open>
  <summary>与主机交换信息方式</summary>
  <p>程序查询</p>
  <p>程序中断: 单重中断, 多重中断</p>
  <p>DMA -> 停止CPU, 周期挪用, CPU与DMA交替访问MM</p>
</details>

## 6. 运算方法

<details open>
  <summary>原码, 补码, 反码</summary>
  <p></p>
</details>

<details open>
  <summary>浮点加减</summary>
  <p>1. 对阶</p>
  <p>2. 规格化: 左规, 右规</p>
  <p>3. 舍入: 0舍1入, 恒置1</p>
</details>

## 7. 指令系统

<details open>
  <summary>机器指令一般格式</summary>
  <p>操作码 + 地址码</p>
  <p>地址码个数: 0, 1, 2, 3, 4</p>
</details>

<details open>
  <summary>指令寻址</summary>
  <p>顺序寻址: PC+1形成</p>
  <p>跳跃寻址: 执行 JMP addr</p>
</details>

<details open>
  <summary>数据寻址</summary>
  <p>指令格式: 操作码OP + 寻址特征 + 形式地址A</p>
  <p>立即寻址</p>
  <p>直接寻址</p>
  <p>隐含寻址</p>
  <p>间接寻址</p>
  <p>寄存器寻址: 类似直接寻址, 但相对寄存器</p>
  <p>寄存器间接寻址: 类似间接寻址, 但相对寄存器</p>
  <p>这里开始的寻址都用到 ALU</p>
  <p>基址寻址: 有专门的基址寄存器BR, 也可用户指定, 但都由系统操作</p>
  <p>变址寻址: 有专门的变址寄存器IX, 也可用户指定, 由用户操作</p>
  <p>相对寻址</p>
</details>

## 8. CPU 结构和功能

<details open>
  <summary>功能</summary>
  <p>指令控制, 操作控制, 时间控制, 数据加工, 处理中断</p>
</details>

<details open>
  <summary>指令周期</summary>
  <p>取址(+分析) [ [-> 间址] -> 执行 [-> 中断] ]</p>
</details>

<details open>
  <summary>指令流水</summary>
  <p>指令细化, 并行执行</p>
  <p>读写冲突: 后推法(周期有停顿), 定向/旁路技术(直接将结果送到其他指令需要的地方)</p>
  <p>多发技术: 普通流水, 超标量流水, 超流水线, 超长指令字</p>
</details>

<details open>
  <summary>中断判优</summary>
  <p>硬件排队</p>
  <p>软件排队</p>
</details>

<details open>
  <summary>中断入口查找方式</summary>
  <p>硬件向量</p>
  <p>软件查询</p>
</details>

## 9. 控制单元的功能

<details open>
  <summary>取址->分析->执行 过程</summary>
  <p>取址: PC->MAR->X->MDR->IR</p>
  <p>CU将PC指向的地址送入MAR, CU命令M读, M将对应MAR所指单元的指令读入MDR, 由MDR送入CU的IR, CU控制PC+1</p>

  <p>分析/译码: OP(IR)->CU</p>
  <p>CU分析操作码</p>

  <p>间址: Ad(IR)->MAR->X->MDR[->Ad(IR)]</p>
  <p>若CU分析出有间址操作, MDR中的形式地址送到MAR, CU命令M读, M将对应MAR所指单元读出的有效地址读入MDR[, 由MDR送入IR的地址字段]</p>

  <p>执行: 若为加法操作</p>
  <p>CU将地址码送入MAR, 命令M读, 将对应MAR所指单元读出的数据送入MDR, 由MDR送入ACC</p>

  <p>中断: SP->MAR->X, PC->MDR->X, MDR->M(MAR)</p>
  <p>CU将中断时存储器的特殊地址送入MAR, 命令M写, 并将PC内容送到MDR, 命令M写, 由MDR送入MAR指示的主存单元, 之后CU将中断地址送入PC, 执行后关中断</p>
</details>

## 10. 控制单元设计

<details open>
  <summary>微指令编码方式</summary>
  <p>直接编码/直接控制: (每一位都是控制信号)</p>
  <p>字段直接编码: 分字段后每个字段译码都是控制信号</p>
  <p>字段间接编码: 分字段后一字段译码还需由另一字段中某些微命令解释才是控制信号</p>
  <p>混合编码: 直接编码 + 字段编码</p>
  <p>其他</p>
</details>

## APPENDIX

### 1. 浮点加减

a = 0.1101 x 2 ^ 01

b = (-0.1010) x 2 ^ 11

求 a + b

**注意阶码、尾数基数均为 2**

因基值为 2, 尾数 S 规格化形式为 1/2 <= |S| < 1

S > 0 时, [S 补 规格化形式] = 00.1...

S < 0 时, [S 补 规格化形式] = 11.0...

**特例: S < 0 时, S = -1/2 不是规格化数, S = -1 是规格化数**

0. 舍入: 对阶, 右规可能丢失低位尾数, 影响精度

- 0 舍 1 入

  > 右移时, 被移的最高位是 0 则舍, 是 1 则尾数末位加 1, 若尾数溢出(即符合右规条件)再次右规

- 恒置 1

  > 右移时, 尾数末位置 1

1. 求[a 补], [b 补]

- [a 补] = 00,01;00.1101, [b 补] = 00,11;11.0110

  > 注意格式如: [a 补] = 00,01;00.1101 中, "00,01"为双符号位阶码, "00.1101"为双符号位尾数

  > 正数的补码同原码, 负数的补码为符号位外取反加 1

2. 对阶

- 求阶差

  > [阶差 补] = [阶 a 补] - [阶 b 补] = 00.01 - 00.01 = 00,01 + 11,01 = 11,10 = -2

- 小阶向大阶看齐

  > 因 [阶 a 补] 小, [a 补] 阶码加 2, 尾数右移 2 位: [a 补]' = 00,11;00.0011

- 尾数求和

  > [a+b 补] = [a 补]' + [b 补] = 00.11;(00.0011 + 11.0110) = 00.11;11.1001

3. 规格化

- 尾数为 00.0... 或 11.1...时左规. 阶码减 1, 尾数左移 1 位, 重复判断

  > 由上步得 [a+b 补] = 00.11;11.1001 符合条件

  > 最终 [a+b 补] = 00.10;11.0010

- 尾数为 01. ... 或 10. ...时右规. 阶码加 1, 尾数右移 1 位, 重复判断

  > 此例不符

  > 若有例 [c+d 补] = 00.10;01.0010, 右规得 0011;00.1001

4. 求原码

- 由 [a+b 补] = 00.10;11.0010 得 a+b = 00.10;11.1110 = (-0.1110) x 2 ^ 10
