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

## 数组和广义表

<details open>
  <summary>数组基本操作</summary>
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

<details open>
  <summary>广义表基本操作</summary>
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
typedef ElemType AtomType;
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

## 树和二叉树

<details open>
  <summary>基本操作</summary>
  <p>构造</p>
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
