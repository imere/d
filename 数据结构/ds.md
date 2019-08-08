# 数据结构

## 1. 绪论

<details open>
  <summary>算法特性</summary>
  <p>有穷性</p>
  <p>确定性</p>
  <p>可行性</p>
  <p>输入</p>
  <p>输出</p>
</details>

<details open>
  <summary>算法设计要求</summary>
  <p>正确性</p>
  <p>可读性</p>
  <p>健壮性</p>
  <p>效率与低存储量需求</p>
</details>

## 2. 线性表

n 个数据元素的有限序列

<details open>
  <summary>基本操作</summary>
  <p>构造</p>
  <p>销毁</p>
  <p>清空</p>
  <p>判断是否为空</p>
  <p>长度</p>
  <p>返回第 i 个元素</p>
  <p>返回元素位置</p>
  <p>返回前驱</p>
  <p>返回后继</p>
  <p>插入</p>
  <p>删除</p>
  <p>遍历</p>
</details>

顺序表

```c
#define LIST_INIT_SIZE 0 // 初始项数
#define LISTINCREMENT 1  // 分配增量

typedef struct
{
  int data;
} ElemType;

typedef struct
{
  ElemType *elem; // 存基址
  int length;     // 长度
  int listsize;   // 分配的容量, 单位sizeof(ElemType)
} SqList;         // 包含连续地址

int ListInit_Sq(SqList *L)
{
  L->elem = (ElemType *)malloc(LIST_INIT_SIZE * sizeof(ElemType));

  L->length = 0;

  L->listsize = LIST_INIT_SIZE;

  return OK;
}

int ListInsert_Sq(SqList *L, int idx, ElemType e)
{
  if (idx < 1 || idx > L->length + 1) return ERR;

  if (L->length >= L->listsize)
  {
    ElemType *base = (ElemType *)realloc(L->elem, (L->listsize + LISTINCREMENT) * sizeof(ElemType));

    if (!base) exit(ERR);

    L->elem = base;
    L->listsize += LISTINCREMENT;
  }

  ElemType *pos = &L->elem[idx - 1];

  for (ElemType *tmp = &L->elem[L->length - 1]; pos <= tmp; --tmp) *(tmp + 1) = *tmp;

  *pos = e;
  ++(L->length);

  return OK;
}

void ListTraverse_Sq(SqList L)
{
  for (size_t i = 0; i < L.length; i++)
  {
    printf("%2d: %d\n", i + 1, L.elem[i].data);
  }
}

int main()
{
  SqList L;

  ListInit_Sq(&L);

  ElemType e;

  e.data = 123;

  ListInsert_Sq(&L, 1, e);

  ElemType e2;

  e2.data = 234;

  ListInsert_Sq(&L, 2, e2);

  ElemType e3;

  e3.data = 345;

  ListInsert_Sq(&L, 2, e3);

  ListTraverse_Sq(L);

  return 0;
}
/*
1: 123
2: 345
3: 234
*/
```

线性链表

```c
typedef struct LNode
{
  ElemType data;      // 结点数据
  struct LNode *next; // 下一结点
} LNode,              // 结点
    *LinkList;        // 头指针, 可不存储信息, 也可存附加信息
```

静态链表

> 用数组描述的链表

```c
#define MAXSIZE 1000
typedef struct
{
  ElemType data;        // 结点数据
  int index;            // 下一结点位置
} component,            // 结点
    SLinkList[MAXSIZE]; // index为0时可不存储信息, 也可存附加信息
```

循环链表

> 尾指向头

双向链表

> 元素既指向前驱又指向后继

优化

```c
typedef struct LNode
{
  ElemType data;      // 结点数据
  struct LNode *next; // 下一结点
} * Link;             // 结点指针

typedef struct
{
  Link head, tail; // 头尾结点
  int len;         // 长度
} LinkList;        // 链表
```

应用

> 存储多项式

## 3. 栈和队列

### 栈

仅在表尾插入删除的线性表

<details open>
  <summary>基本操作</summary>
  <p>构造</p>
  <p>销毁</p>
  <p>清空</p>
  <p>判断是否为空</p>
  <p>长度</p>
  <p>返回最后一个元素</p>
  <p>插入元素到最后</p>
  <p>删除最后一个元素</p>
  <p>遍历</p>
</details>

顺序栈

```c
#define STACK_INIT_SIZE 100
#define STACKINCREMENT 10
typedef struct
{
  SElemType *base; // 栈底指针, 构造前和销毁后为 NULL
  SElemType *top;  // 栈顶指针, 初值是栈底
  int size;        // 长度
} SqStack;         // 顺序栈
```

应用

> 数制转换, 括号匹配, 行编辑, 迷宫

### 队列

FIFO的线性表

<details open>
  <summary>基本操作</summary>
  <p>构造</p>
  <p>销毁</p>
  <p>清空</p>
  <p>判断是否为空</p>
  <p>长度</p>
  <p>返回第一个元素</p>
  <p>删除第一个元素</p>
  <p>插入元素到最后</p>
  <p>遍历</p>
</details>

链队列

```c
typedef struct QNode
{
  QElemType data;
  struct QNode *next;
} QNode, *QueuePtr;
typedef struct
{
  QueuePtr front; //头指针
  QueuePtr rear;  // 尾指针
} LinkQueue;
```

循环队列

```c
#define MAXSIZE 100 // 最大长度
typedef struct
{
  QElemType *base; // 初始空间
  int front;       // 头指针
  int rear;        // 尾指针
} SqQueue;

int EnQueue(SqQueue &Q, QElemType e)
{
  if ((Q.rear + 1) % MAXSIZE == Q.front)
    return ERR;                    // 队列满

  Q.base[Q.rear] = e;              // 入队
  Q.rear = (Q.rear + 1) % MAXSIZE; // 设置尾指针. 恰好满则头尾相同
  return OK;
}
```

应用

> 银行业务模拟

## 5. 数组和广义表

### 数组

<details open>
  <summary>基本操作</summary>
  <p>构造</p>
  <p>销毁</p>
  <p>指定位置取值</p>
  <p>指定位置赋值</p>
</details>

```c
#define MAX_ARR_DIM 8 // 最大维数
typedef struct
{
  ElemType *base; // 元素基址
  int dim;        // 维数
  int *bounds;    // 维界基址. 记录各维元素数
  int *constants; // 映像函数常量基址. 记录高维基址位置
} Array;
/**
 * @param {Array&} A  数组
 * @param {int} dim  维数
 * @param {int} ...  各维元素个数
 */
int InitArray(Array &A, int dim, ...)
{
  if (dim < 1 || dim > MAX_ARR_DIM) return ERR;

  A.dim = dim;

  A.bounds = (int *)malloc(dim * sizeof(int));
  if (!A.bounds) exit(ERR);

  int len = 1; // 总长度

  va_list ap;
  va_start(ap, dim);
  for (int i = 0; i < dim; i++)
  {
    A.bounds[i] = va_arg(ap, int);
    if (A.bounds[i] < 0) return ERR;
    len *= A.bounds[i];
  }
  va_end(ap);

  A.base = (ElemType *)malloc(len * sizeof(ElemType));
  if (!A.base) exit(ERR);

  A.constants = (int *)malloc(dim * sizeof(int));
  if (!A.constants) exit(ERR);

  A.constants[dim - 1] = 1;
  for (int i = dim - 2; i >= 0; i--)
  {
    A.constants[i] = A.bounds[i + 1] * A.constants[i + 1];
  }

  return OK;
}
```

矩阵的压缩存储

> 特殊矩阵: 对称矩阵, 对角矩阵

> 稀疏矩阵. 存储三元组(行, 列, 值)

### 广义表

<details open>
  <summary>基本操作</summary>
  <p>构造</p>
  <p>从书写形式串构造</p>
  <p>销毁</p>
  <p>复制</p>
  <p>长度</p>
  <p>深度</p>
  <p>判断是否为空</p>
  <p>返回第一个元素</p>
  <p>返回最后一个元素</p>
  <p>插入元素到第一个</p>
  <p>删除第一个元素</p>
  <p>遍历</p>
</details>

```c
typedef enum
{
  ATOM, // 原子
  LIST  // 子表
} ElemTag;
typedef struct GLNode
{
  ElemTag tag; // 区分结点类型
  union {
    AtomType atom; // 原子结点值域
    struct
    {
      struct GLNode *head, *tail; // 子表内指针域
    } ptr;
  };
} * GList; // 广义表
```

## 6. 树和二叉树

<details open>
  <summary>基本操作</summary>
  <p>构造</p>
  <p>销毁</p>
  <p>从definition构造</p>
  <p>清空</p>
  <p>判断是否为空</p>
  <p>深度</p>
  <p>返回根结点</p>
  <p>取结点值</p>
  <p>赋值结点</p>
  <p>返回父结点</p>
  <p>返回左子结点</p>
  <p>返回右子结点</p>
  <p>插入结点为某结点第 i 棵子树</p>
  <p>删除某结点第 i 棵子树</p>
  <p>遍历</p>
</details>

### 二叉树

<details open>
  <summary>基本操作</summary>
  <p>构造</p>
  <p>销毁</p>
  <p>从definition构造</p>
  <p>清空</p>
  <p>判断是否为空</p>
  <p>深度</p>
  <p>返回根结点</p>
  <p>取结点值</p>
  <p>赋值结点</p>
  <p>返回父结点</p>
  <p>返回左子结点</p>
  <p>返回右子结点</p>
  <p>返回左兄弟</p>
  <p>返回右兄弟</p>
  <p>插入结点为某结点某子树</p>
  <p>删除某结点某子树</p>
  <p>先序遍历</p>
  <p>中序遍历</p>
  <p>后序遍历</p>
  <p>层序遍历</p>
</details>

顺序存储

> 适用完全二叉树

```c
#define MAX_TREE_SIZE 100 // 最大结点数
typedef TElemType SqBiTree[MAX_TREE_SIZE];
SqBiTree bt;
```

链式存储

```c
typedef struct BiTNode
{
  TElemType data;
  struct BiTNode *l, *r; // 子树
} BiTNode, *BiTree;
```

遍历

> 先(根)序遍历 DLR

> 中(根)序遍历 LDR

> 后(根)序遍历 LRD

二叉线索存储

> 用空链域存前驱或后继

```c
typedef enum PointerTag
{
  Link,  // 指针
  Thread // 线索
};
typedef struct BiThrNode
{
  TElemType data;
  struct BiThrNode *l, *r; // 左右子树
  PointerTag LTag, RTag;   // 左右标志
} BiThrNode, *BiThrTree;
```

### 树

双亲表存储

> 结点位置存数组

```c
#define MAX_TREE_SIZE 100
typedef struct PTNode
{
  TElemType data;
  int parent; // 双亲位置
} PTNode;     // 结点
typedef struct
{
  PTNode nodes[MAX_TREE_SIZE];
  int r, // 根位置
      n; // 结点数
} PTree;
```

孩子链表存储

> 结点子树位置链表存数组

```c
typedef struct CTNode
{
  TElemType data;
  struct CTNode *next;
} * ChildPtr; // 孩子结点
typedef struct
{
  TElemType data;
  ChildPtr firstChild; // 孩子链表头指针
} CTBox;
typedef struct
{
  CTBox nodes[MAX_TREE_SIZE];
  int r, // 根位置
      n; // 结点数
} CTree;
```

二叉链表(孩子-兄弟)存储

### 森林

### 赫夫曼(Huffman)树

> 带权路径长度最短的树

### 赫夫曼编码

> n 种字符出现频率作权设计赫夫曼树

```c
typedef struct
{
  unsigned int weight;
  unsigned int parent, l, r;
} HTNode, *HuffmanTree;     // 动态分配数组存储赫夫曼树
typedef char **HuffmanCode; // 动态分配数组存储赫夫曼编码表
```

## 7. 图

完全图

> 有 1/2 * n * (n-1) 条边的无向图

有向完全图

> 有 n * (n-1) 条弧的有向图

稀疏图

> 有很少边或弧的图(e < nlogn)

网

> 带权的图

度

> 和顶点关联的边数

简单路径

> 顶点不重复出现的路径

连通图

> 任两个顶点都连通

强连通分量

> 有向图的极大连通子图

<details open>
  <summary>基本操作</summary>
  <p>构造</p>
  <p>销毁</p>
  <p>返回顶点位置</p>
  <p>返回顶点值</p>
  <p>赋值顶点</p>
  <p>返回顶点的第一个邻接顶点</p>
  <p>返回顶点相对于另一个顶点的下一个邻接顶点</p>
  <p>新增顶点</p>
  <p>删除顶点及相关弧</p>
  <p>新增弧</p>
  <p>删除弧</p>
  <p>DFS遍历</p>
  <p>BFS遍历</p>
</details>

数组(邻接矩阵)表示

> 方便

```c
#define INFINITY INT_MAX
#define MAX_VERTEX_NUM 20
typedef enum
{
  DG,  // 有向图
  DN,  // 由向网
  UDG, // 无向图
  UDN  // 无向网
} GraphKind;
typedef struct ArcCell
{
  VRType adj;     // 顶点关系类型. 无权图: 0,1表示是否相邻, 有权图: 权值类型
  InfoType *info; // 弧相关信息的指针
} ArcCell, AdjMatrix[MAX_VERTEX_NUM][MAX_VERTEX_NUM];
typedef struct
{
  VertexType vexs[MAX_VERTEX_NUM]; // 顶点向量
  AdjMatrix arcs;                  // 邻接矩阵
  int vexnum, arcnum;              // 当前顶点数, 弧数
  GraphKind kind;                  // 种类标志
} MGraph;
```

链式(邻接表)

> 稀疏矩阵省空间

```c
typedef struct ArcNode
{
  int adjvex;              // 指向的顶点位置
  struct ArcNode *nextarc; // 下一条弧指针
  InfoType *info;          // 弧相关信息
} ArcNode;
typedef struct VNode
{
  VertexType data;   // 顶点信息
  ArcNode *firstarc; // 第一条依附该顶点弧的指针
} VNode, AdjList[MAX_VERTEX_NUM];
typedef struct
{
  AdjList vertices;
  int vexnum, arcnum; // 当前顶点数, 弧数
  int kind;           // 种类标志
} ALGraph;
```

十字链表

```c
typedef struct ArcBox
{
  int tailvex, headvex;         // 尾和头顶点位置
  struct ArcBox *hlink, *tlink; // 弧头相同和弧尾相同的弧链域
  InfoType *info;               // 弧相关信息
} ArcBox;
typedef struct VexNode
{
  VertexType data;
  ArcBox *firstin, *firstout; // 指向该顶点的第一条入弧出弧
} VexNode;
typedef struct
{
  VexNode xlist[MAX_VERTEX_NUM]; // 表头向量
  int vexnum, arcnum;
} OLGraph;
```

邻接多重表

> 无向图链式存储

```c
typedef enum
{
  unvisited,
  visited
} VisitIf;
typedef struct EBox
{
  VisitIf mark;               // 访问标记
  int ivex, jvex;             // 该边依附的两个顶点位置
  struct EBox *ilink, *jlink; // 分别指向依附两个顶点的下一条边
  InfoType *info;             // 边信息指针
} EBox;
typedef struct VexBox
{
  VertexType data;
  EBox *firstedge; // 指向第一条依附该顶点的边
} VexBox;
typedef struct
{
  VexBox adjmulist[MAX_VERTEX_NUM];
  int vexnum, edgenum; // 当前顶点数, 边数
} AMLGraph;
```

遍历

> DFS

```c
void DFS(Graph G, int v)
{
  visited[v] = TRUE;
  Visit(v);
  for (w = FirstAdjacentVertex(G, v); w >= 0; w = NextAdjacentVertex(G, v, w))
  {
    if (!visited[w]) DFS(G, w);
  }
}
```

> BFS

```c
void BFS(Graph G, int (*Visit)(int v))
{
  for (v = 0; v < G.vexnum; ++v) visited[v] = FALSE;

  InitQueue(Q);

  for (v = 0; v < G.vexnum; ++v)
    if (!visited[v])
    {
      visited[v] = TRUE;
      Visit(v);
      EnQueue(Q, v);
      while (!QueueEmpty(Q))
      {
        DeQueue(Q, u);
        for (w = FirstAdjacentVertex(u); w >= 0; w = NextAdjacentVertex(G, u, w))
        {
          if (!visited[w])
          {
            visited[w] = TRUE;
            Visit(w);
            EnQueue(Q, w);
          }
        }
      }
    }
}
```

应用

> 最小(代价)生成树

```c
struct
{
  VertexType adjvex;
  VRType lowcost;
} closedge[MAX_VERTEX_NUM]; // 记录从顶点集 U 到 V-U 的代价最小的边的辅助数组定义

// 普里姆算法
void MiniSpanTree_PRIM(MGraph G, VertexType u)
{
  int k = LocateVex(G, u); // 确定顶点 u 位置

  for (int j = 0; j < G.vexnum; j++) // 辅助数组初始化
  {
    if (j != k)
      closedge[j] = {u, G.arcs[k][j].adj}; // { adjvex, lowcost }
  }

  closedge[k].lowcost = 0; // 初始时 U = { u }

  for (int i = 0; i < G.vexnum; i++) // 选其余 G.vexnum-1 个顶点
  {
    k = minimum(closedge);   //求 T 的下一个结点
    closedge[k].lowcost = 0; // 第 k 点移入 U
    for (j = 0; j < G.vexnum; j++)
    {
      if (G.arcs[k][j].adj < closedge[j].lowcost) // 新顶点移入 U 后重选最小边
        closedge[j] = {G.vexs[k], G.arcs[k][j].adj};
    }
  }
}
```

> 最短路径

> 拓扑排序

> 关键路径
