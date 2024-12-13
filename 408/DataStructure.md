<center>**<font color="red" size="28">数据结构</font>**</center>



# 0、时间复杂度

## 1.频率最高的语句（执行深度最深的 /阶数最多的）

## 2. 语句执行次数和问题规模n的关系

## 3. 忽略常数

![image-20241017210952655](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017210952655.png)

![image-20241017211000233](C:/Users/33813/AppData/Roaming/Typora/typora-user-images/image-20241017211000233.png)

![image-20241017211008348](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017211008348.png)



# 数组、矩阵存储和广义表



## 特殊矩阵的压缩存储

分为按行优先和按列优先存储 

注意点 ： ==一维数组默认从0下标开始==

`array [n][m]` n个数组（0~n-1），每个数组里都有m（0 ~ m-1）个元素

![image-20241124175558277](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124175558277.png)

**行/列/页优先**



### ==对称矩阵==的压缩存储



![image-20241124175822092](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124175822092.png)

**以……为顺序将 二维数组的一部分存储在一维数组当中**

### 三角矩阵



![image-20241124180025625](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124180025625.png)

**多一个就去存那个固定的c值**

![image-20241124181356800](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124181356800.png)

**c==0 就是线性代数里比较特殊的上/下三角矩阵**

###  对角矩阵

![](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124180339303.png)

**以对角线的顺序存储**



### 稀疏矩阵

![image-20241124180403044](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124180403044.png)

**密度小于0.05 （非零元素少时）**

![image-20241124181712867](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124181712867.png)

![image-20241124181757465](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124181757465.png)

### 十字链表存储稀疏矩阵

![image-20241124181839495](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124181839495.png)

![image-20241124181929350](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124181929350.png)

![image-20241124182002045](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124182002045.png)



## 广义表

![image-20241124180457077](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124180457077.png)



![image-20241124180545920](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124180545920.png)

![image-20241124180625820](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124180625820.png)

![image-20241124180728470](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241124180728470.png)

**三对角矩阵概念！**

![image-20241017211021475](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017211021475.png)



![825357dbaf9fecd541cf159647cf60a](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/825357dbaf9fecd541cf159647cf60a.jpg)

**m~ij~ 的i j取决于 按行/列优先存储**







# <font size=25 color=red>一、链表</font>

==增操作 ： 构建链表！==

## 顺序表（数组实现）：

> 使用数组，静态分配。

```c++
#include<iostream>
using namespace std;
#define max_size 10
typedef struct 
{
    int data[max_size];//顺序表最大长度
    int length;//顺序表当前长度
    
}Sqlist;
void init(Sqlist &l)//创
{
    
    l.length=0;//当前长度为0

    
}
void add(Sqlist &l,int x)//增
{
    l.data[++l.length]=x;
    
}
// void del(Sqlist &l,int idx)//删
// {
   
// }
void change(Sqlist &l,int idx,int x)//改
{
    l.data[idx]=x;//包含了查找
    
}
bool isEmpty(Sqlist &l)
{
    if(l.length)
    return 0;
    else
    return 1;
}
int main()
{
    Sqlist l;
     init(l);
     add(l,5);
     add(l,3);
     change(l,2,8);
     for(int i=1;i<=l.length;i++)
     cout<<l.data[i]<<' ';//查
     cout<<endl<<isEmpty(l);
     
     
}
```



## 链表（链式实现）

> 使用new/malloc ，delete/free 动态分配内存空间！

### ==创+初始化==

~~~c++
typedef struct ListNode
{
    int val;
    ListNode *next;
    ListNode():next(nullptr){}//无参构造
    ListNode(int x):val(x),next(nullptr){}//初始化
    
}*list;


 ListNode *a=new ListNode(-1);//a是指针(地址)//创
    list b=new ListNode(2);
~~~

### ==构建链表==

#### 头插法

~~~c++
void add_head(list &l,int x)//头插法  -->栈--> 头节点就是栈顶
{
    ListNode *newnode=new ListNode(x);//新结点
    newnode->next=l->next;
    l->next=newnode;
    
}
~~~

#### 尾插法

~~~c++
void add_tail(list &l,int x)//尾插法  
{
    ListNode *tail=l;//定义一个尾结点
    while(tail->next!=nullptr)
        tail=tail->next;//找到end位置(不是null)
        
    ListNode *s=new ListNode(x);//创建新结点
    
    tail->next=s;
    tail=s;//更新尾指针位置
        
    
    
}
~~~

#### 按指定位置插入新节点

~~~c++
void insert(list &l,int idx,int x)//在链表指定位置插入结点
{
    if(idx==0)
    return ;  
    if(idx==1)
    {
        add_head(l,x);
        return ;
    }
    list tmp=l;//步进结点,替代原有的链表
    int pos=0;
    ListNode *newnode=new ListNode(x);//创建新结点
  
    while(tmp!=nullptr)
    {
        if(pos==idx-1)//如果找到了前驱结点
        {
            newnode->next=tmp->next;
            tmp->next=newnode;
            return ;
       
        }
        pos++;
     
        tmp=tmp->next;
    }
    
}

~~~

### ==查找==

#### 按位查找

~~~c++
int query_value(list l,int x)//按位查找值
{
    int idx=1;
 
    while(l!=nullptr)
    {
        l=l->next;//不管头节点
        if(l==nullptr)//边界条件
        break;
        
       
        if(idx==x)
        return l->val;
        idx++;
        
    }
    return -1;
    
    
}

~~~



#### 按值查找

~~~c++
int query_index (list l,int x)//按值查找,不能加list &l 防止步进时修改链表的头节点
{
    int pos=1;//标记位置
    while(l!=nullptr)
    {
         l=l->next;
         if(l==nullptr)//防止空指针访问异常
         return -1;
         
        if(l->val==x)
        {
            return pos;
        } 
        pos++;
        
    }
    return -1;
    
}
~~~

### ==删除==指定位置的结点

~~~c++
void del(list &l,int k)//删除第k个结点,头节点表示第0个位置
{
   
    //特判
    if(k==0)
    return ;//头节点不删
   
    
    list tmp=l;//步进结点,替代原有的链表
    int pos=0;
    while(tmp->next!=nullptr)
    {
        if(pos==k-1)//找到了这个结点的前驱结点才删除
        {
           tmp->next=tmp->next->next;  
           return ;
        }
        
         tmp=tmp->next;
         pos++;
    }
    return ;
    
}
~~~

### ==判空&计算长度==

~~~c++
bool isEmpty(list l)
{
    if(l->next==nullptr)
    return 1;
    else
    return 0;
    
}
~~~

~~~c++
int countLen(list l)//统计链表长度,如果加了地址符链表当前头节点的位置就会变化
//如果不是修改原链表最好不要地址传参 或者可以用一个结点复制原  头结点 （反正有头节点就可以访问整个链表了）
{
    int len=0;
    while(l!=nullptr)
    {
        l=l->next;
        len++;
    }
    return len-1;
}
~~~

<font color='red' size=6>！！注意问题：不要随便移动初始的头节点（哨兵结点，固定，），要固定住，然后使用步进结点步进去遍历  。 遍历时要防止空指针异常，特判极端（极小极大/一般）边界情况</font>

---



## ！循环链表(环形链表，！但指向==表头==)

###  ==循环单链表==和==循环双链表== 

**<font size='16' color='red'>循环是有<u>作用</u>的</font>**

![image-20240924231426150](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240924231426150.png)

![image-20240924231442290](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240924231442290.png)

### **初始化：**![image-20241013213720089](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013213720089.png)



![image-20241013213147658](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013213147658.png)

**删除也同理！**

![image-20240924231456953](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240924231456953.png)

![image-20240924231510937](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240924231510937.png)

![image-20240924231537034](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240924231537034.png)

![image-20240924231552815](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240924231552815.png)



> 可设置头尾指针（类似带头尾结点！

![Screenshot_2024-10-10-12-52-26-019_net.csdn.csdnplus](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/Screenshot_2024-10-10-12-52-26-019_net.csdn.csdnplus.png)



![image-20241013213814034](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013213814034.png)

![image-20241013213906802](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013213906802.png)

## <u>双链表（带头结点）</u>

### 创+初始化

~~~C++
//初始化（构造函数）
typedef struct bioListNode
{
    int val;
    bioListNode *next;
    bioListNode *prior;
    bioListNode(int x):val(x),next(nullptr),prior(nullptr){}
    
}*bioList;

//创
   bioListNode *a=new bioListNode(-1);
    bioListNode *b=new bioListNode(-1);
    a->next=b;
    b->prior=a;//初始化定义头结点和尾结点（都是不存真正的值的）
//这样 《头插法》 和 《尾插法》 就更容易了
~~~

### 在p结点之后插入s结点

~~~c++
void insert(bioListNode *p,bioListNode *s)//传入两个结点,在p结点之后插入一个新的结点
{
    s->next=p->next;
    p->next->prior=s;
    s->prior=p;
    p->next=s;
}
~~~



### 双链表的删除（按位删除）

```cpp
void del(bioListNode *p) // 删除结点p
{
    if (p == nullptr) return;

    if (p->prior != nullptr) {
        p->prior->next = p->next;
    }
    if (p->next != nullptr) {
        p->next->prior = p->prior;
    }
    delete p;
}
```

### 双链表查找指定结点

#### 按值查找

~~~C++
bioListNode* find_by_value(bioList l, int value) {
    while (l != nullptr) {
        if (l->val == value) {
            return l; // 找到值为value的节点
        }
        l = l->next;
    }
    return nullptr; // 未找到值为value的节点
}
~~~

#### 按位查找

~~~C++
bioListNode* find_by_index(bioList l, int index) {
    int current_index = 0;
    while (l != nullptr) {
        if (current_index == index) {
            return l; // 找到索引为index的节点
        }
        l = l->next;
        current_index++;
    }
    return nullptr; // 未找到索引为index的节点
}
~~~



### 双链表的遍历（可向==前==也可向==后==）



<img src="C:/Users/33813/AppData/Roaming/Typora/typora-user-images/image-20240924222050321.png" alt="image-20240924222050321" height='200' width='100000' />



# basic：==数组==的缺陷和链表的区别

~~~C++
#include<iostream>
using namespace std;
const int N=1e3+10;
#define Maxsize 20
int a[N];

typedef struct sqlist
{
  int data[Maxsize];
  int length;
  
};

void init(sqlist &l)//初始化
{
    l.length=0;
    for(int i=0;i<l.length;i++)l.data[i]=0;
    
}
void insert(sqlist &l,int k,int x)//在指定位置插入元素
{
    l.length++;
    if(l.length>=Maxsize)
    return ;
    for(int i=l.length;i>k;i--) l.data[i]=l.data[i-1];
    l.data[k]=x;
    
}
void del(sqlist &l,int k)//在指定位置删除元素
{
    if(k>=l.length)
    return ;
    for(int i=k;i<l.length-1;i++)l.data[i]=l.data[i+1];
    l.length--;
       
       
    
    
}
void print(sqlist l)
{
    for(int i=0;i<l.length;i++)cout<<l.data[i]<<' ';
    cout<<endl;
}
int main()
{
    sqlist l;
    init(l);
    insert(l,0,5);
    insert(l,0,8);
    insert(l,1,9);
    insert(l,2,9);
    print(l);
    del(l,2);
    print(l);
    cout<<l.length;
    
    
    
    return 0;
}
~~~



## 应用 ： 多项式的 -存储-  &&  多项式的 -相加-





~~~C++
~~~





---





~~~C++
~~~







---

# 二、栈与队列

---



## 栈

### 顺序栈

~~~c++
#include<iostream>
using namespace std;
const int maxsize=25;
typedef struct 
{
    int val[maxsize];
    int top;//栈顶指针
    
}stack;
void init(stack &st)//初始化
{
    st.top=0;//表示没有元素
    for(int i=0;i<=maxsize;i++)
        st.val[i]=0;
}
void add(stack &st,int x)//增
{
    st.val[++st.top]=x;
}
void pop(stack &st)
{
    st.val[st.top--];
}
bool isEmpty(stack st)
{
    if(!st.top)return 1;
    else return 0;
}
int countLen(stack st)
{
    return st.top;
}
void print(stack st)
{
    while(st.top)
    cout<<st.val[st.top--]<<
{
    stack st;//创" ";
    
}
int main()
    init(st);
    add(st,8);
    add(st,5);
    add(st,6);
    add(st,4);
    add(st,6);
    add(st,3);
    pop(st);
    cout<<st.val[st.top];//查
    cout<<endl<<countLen(st)<<endl;
    print(st);
    // (3) 6 4 6 5 8
    
    return 0;
}
~~~

### 链栈

> ### 带头结点

#### 创&初始化：new方法

#### 入栈 ： 单链表头插法

#### 出栈 ：单链表头（存数据的头）删

#### 判空 ：st->next==nullptr

#### 查值：st->next->val

#### 计（算）长（度）：遍历计算



## 应用 ： 表达式求值 





**结合队列可求杨辉三角！**

~~~C++
#include<iostream>
#include<stack>
#include<unordered_map>
using namespace std;
stack<char>op;
stack<int>num;
unordered_map<char,int> h{{'+',1},{'-',1},{'/',2},{'*',2}};
void eval()
{
    int num1=num.top();
    num.pop();
    int num2=num.top();
    num.pop();//注意要弹出
    char c=op.top();
    op.pop();
    int ans=0;
    if(c=='+')ans=num1+num2;
    if(c=='-')ans=num2-num1;
    if(c=='/')ans=num2/num1;//注意栈是倒着存的
    if(c=='*')ans=num1*num2;
    num.push(ans);


    
}
int main()
{
    string s;
    cin>>s;
    for(int i=0;i<s.size();i++)
    {
        if(s[i]>='0'&&s[i]<='9')
        {
            int x=0,j=i;
            while(j<s.size()&&(s[j]>='0'&&s[j]<='9'))
            {   
                x=x*10+s[j]-'0';
                j++;
            }
           
            num.push(x); 
            i=j-1;
        }
        else if(s[i]=='(')
            op.push(s[i]);
            
        else if(s[i]==')')
        {
            while(op.top()!='(')//这里不用判空
            {
                eval();
            }
            op.pop();
        }
        else
        {
            while(op.size()&&h[s[i]]<=h[op.top()])
            eval();//要判空 （特判！）
            
            op.push(s[i]);
        }
        
    }
    while(op.size())eval();
    
    cout<<num.top();
    return 0;
    
    
}
~~~

#### 注意点：

**判空 扫尾操作  双指针闪现（防止延迟！）**

---



## 队列

> ### 带头结点

> 这里讨论的是只可队尾插入队头弹出的队列（非 真·双端队列和`假·双端队列`）

#### 初始化 （利用结构体的嵌套）

~~~c++
#include<iostream>
using namespace std;
typedef struct ListNode// 结点结构体 --> 结构体变量 里面存有 int值还有一个next指针（地址）
{
    int val;
    ListNode *next;
    ListNode(int val)
    {
        this->val=val;
        this->next=nullptr;
    }//初始化
};

typedef struct 
{
   ListNode *front,*rear;//有两个结点结构体，里面存有next指针（地址）和值
}listQueue;
int main()
{
    //创建带头节点的链队
    listQueue l;//l是个 结构体对象 不能使用-> 来引用！
   l.front=l.rear=new ListNode(-1);
    return 0;
}
~~~



<font size=25 color=red>这个头指针是不存值的（也即是带头节点）-->与以上同理</font>

<font size=25 color=red>**结点结构体正常搞**</font>

<font size=25 color=red>**给链队设置头尾指针** 这样可以访问到头尾元素</font>



#### 入队 (使用尾插法)

~~~c++
void add_tail(listQueue &l,int x)//尾插法
{
    ListNode *newNode= new ListNode(x);
    l.rear->next=newNode;
    l.rear=newNode;
    
}
void print(listQueue l)
{
    ListNode *head=l.front->next;
    while(head!=nullptr)
    {
        cout<<head->val<<"-->";
        head=head->next;
    }
    cout<<"NULL";
    cout<<endl;
}
~~~

#### 出队（头删法）

~~~c++
void pop_front(listQueue &l)
{
    
    ListNode *head=l.front;
    if(head->next==nullptr)return ;
    head->next=head->next->next;
}
~~~

#### 判空

~~~C++
bool isEmpty(listQueue l)
{
    if(l.front==l.rear)return 1;
    else return 0;
    
}
~~~

#### 打印

~~~C++
void print(listQueue l)
{
    ListNode *head=l.front->next;
    while(head!=nullptr)
    {
        cout<<head->val<<"-->";
        head=head->next;
    }
    cout<<"NULL";
    cout<<endl;
}
~~~



#### 双端队列（两端都可进出）

~~~c++
// void pop_rear(listQueue &l)//尾删法
// {
//     ListNode *tail=l.rear;
    
    
// }


void add_head(listQueue &l,int x)//头插
{
    ListNode *head=l.front;
    ListNode *newNode=new ListNode(x);
    newNode->next=head->next;
    head->next=newNode;
}

~~~

#### 单调队列

~~~c++
#include<iostream>
#include<deque>
using namespace std;
const int N=1e6+10;
int a[N];
int n,k;
int main()
{
    cin>>n>>k;
    for(int i=1;i<=n;i++)cin>>a[i];
    deque<int> q;
    //找最小值
   for(int i=1;i<=n;i++)//枚举每一个点
    {
        //i起码要大于窗口长度
       if(i>k&&a[i-k]==q.front())q.pop_front();//如果滑出窗口的话（一定要保证窗口元素个数不大于k）
       
       while(q.size()&&a[i]<q.back())q.pop_back();
        q.push_back(a[i]);
       
        if(i>=k)
        cout<<q.front()<<' ';
        
    }
    cout<<endl;
    q.clear();
     for(int i=1;i<=n;i++)//枚举每一个点
    {
        while(q.size()&&a[i]>q.back())q.pop_back();
        q.push_back(a[i]);//队列存值
        //若队头滑出了窗口，则弹出队头，保持窗口的元素在k之内
        if(i-k>=1&&a[i-k]==q.front())
        q.pop_front();
        
        //窗口形成
        if(i>=k)cout<<q.front()<<" ";
        
        
    }
    
    return 0;
}
~~~



==**存下标**==

~~~C++
 for(int i=1;i<=n;i++)
    {
        //不可q.size()>=k
        if(i>k&&i-k==q.front())q.pop_front();
        while(q.size()&&a[q.back()]>a[i])q.pop_back();
        q.push_back(i);
        if(i>=k)cout<<a[q.front()]<<' ';
    }
~~~

#### 循环队列

~~~C++
#include <iostream>
using namespace std;
#define max_size 100
// typedef struct cq //如果此处写了下面一定要写
// {

// }circular_queue;
typedef struct 
{
  int data[max_size];
  int front;
  int rear;

}circular_queue;
void init (circular_queue *q)
{
  q->front=q->rear=0;
}
bool isEmpty(circular_queue *q)
{
  if(q->front==q->rear)
    return 1;
  else
    return 0;

}
bool isFull(circular_queue *q)
{
  if((q->rear+1)%max_size==q->front)
    return 1;
  else 
    return 0;

}
int dequeue(circular_queue *q)
{
  int x;
  if(isEmpty(q))
    return 0;
  else
  {
    x=q->data[q->front];
    q->front=(q->front+1)%max_size;
  }
  return x;


}
bool enqueue(circular_queue *q,int x)
{
  if(isFull(q))
    return 0;
  else
  {
    q->data[q->rear]=x;
    q->rear=(q->rear+1)%max_size;

  }
  return 1;

  
}
void print(circular_queue *q)
{
  while(!isEmpty(q))
  {
    cout<<dequeue(q)<<' ';
  }
}
int main()
{
  circular_queue q;
  init(&q);
  int n;
  cin>>n;
  for(int i=0;i<n;i++)
  {
    int x;
    cin>>x;
    enqueue(&q,x);
  }
  print(&q);
  cout<<q.data[q.front]<<" "<<q.data[q.rear-1]; //输出队头和队尾

  return 0;
}
~~~

![image-20241015132005982](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015132005982.png)

![image-20241015132014127](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015132014127.png)

**图 1and  3 是空位不同的循环队列**

**图 2 是判断队列的长度！！！** 



# 三、串（String）

![image-20240925153840008](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925153840008.png)

**如果经常用到拼接（长度经常扩展变化）就要使用动态存储结构！**

![image-20240925153922279](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925153922279.png)

==清空串和销毁串不一样，前者内存空间中还有剩余，后者不是；==

####  1.串的比较

![image-20240925154140041](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925154140041.png)

> **`按照字典序排序优先看每个字母，如果前缀都一样就要看长度！`**

拓展：采用不同的编码方式，每个字符所占空间不同，考研中只需默认每个字符占==1B==即可



#### 2.串的顺序存储

![image-20240925154440498](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925154440498.png)

**销毁这个串： free释放内存空间！**

![image-20240925154450549](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925154450549.png)

**==如果用数组空间去存的话，一个空间是一字节，一字节的空间只能存0-255（整型）==**

![image-20240925154455828](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925154455828.png)

![image-20240925155500570](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925155500570.png)

#### 3.串的链式存储



![image-20240925154500645](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925154500645.png)



#### 4.串的基本操作

##### (1) 截取子串

![image-20240925154506513](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925154506513.png)

##### (2) 比较字符串

![image-20240925154515710](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925154515710.png)

##### (3) 索引字符串



![image-20240925154526505](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240925154526505.png)

##### (4)其他

判空：length

拷贝：遍历赋值

清空：令length=0；

~~~c++
#include<iostream>
using namespace std;
typedef struct StringNode
{
    char val[4];
    StringNode *next;
    StringNode(char c)///构造函数
    {
        val[0] = c;  // 初始化第一个字符
        val[1] = '\0';  // 确保字符串终止符存在
        val[2] = '\0';  // 初始化其余字符为终止符
        val[3] = '\0';  // 初始化其余字符为终止符
        next=nullptr;
    }
    
    
}*Sstring;

void print(StringNode *s)
{
    while(s!=nullptr)
    {
        cout<<s->val[0];
        s=s->next;
        
    }

~~~





#### 注意点

~~~c++
// StringNode* catString(StringNode *a,StringNode *b)//拼接字符串
// {
    
//     StringNode *res=new StringNode('#');
//     StringNode *cur=res;
   
//   while(a!=nullptr)
//   {
//       cur->next=a;
//       a=a->next;
//       cur=cur->next;
//   }
//   while(b!=nullptr)
//   {
//       cur->next=b;
//       b=b->next;
//       cur=cur->next;
//   }
//   return res->next;//传回地址
    
// }
StringNode* catString(StringNode *a, StringNode *b) {
    // 创建一个新的头节点
    StringNode *res = new StringNode('#');
    StringNode *cur = res;

    // 遍历a，复制节点
    StringNode *tempA = a->next; // 跳过a的头节点
    while (tempA != nullptr) {
        cur->next = new StringNode(tempA->val[0]); // 创建新节点
        cur = cur->next;
        tempA = tempA->next;
    }

    // 遍历b，复制节点
    StringNode *tempB = b->next; // 跳过b的头节点
    while (tempB != nullptr) {
        cur->next = new StringNode(tempB->val[0]); // 创建新节点
        cur = cur->next;
        tempB = tempB->next;
    }

    return res; // 返回新的链表
}
~~~



~~~C++

int main()
{
    int n;
    cin>>n;
    StringNode *a=new StringNode('#');//初始化 创造一个字符串
    
    for(int i=0;i<n;i++)//存住字符串
    {
        char c;
        cin>>c;
        StringNode *tmp=new StringNode(c);//创建一个结点
        a=append(a,tmp);
       
    //   输入 c b g f  
    }
    StringNode *b=new StringNode('j');
    StringNode *ans=catString(a,b);
    
    print(a);
    //如果按照注释那样会使得a为cbgfj
    return 0;
}
~~~

> **返回字符串基本都是带#头节点的和单链表统一！！**
>
> ##### 如果按照注释那样会使得a为cbgfj

## BF 算法（暴力匹配）

![image-20241017200841618](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017200841618.png)

直接使用双重循环

或是双指针

![image-20241017200920166](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017200920166.png)

### 时间复杂度分析

![image-20241017200939277](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017200939277.png)





# 四、KMP算法

> 主要就是前缀数组next

~~~C++
#include<iostream>
const int N=1e5+10,M=1e6+10;
char p[N],s[M];
int n,m;
int ne[N];
using namespace std;
int main()
{
    cin>>n>>p+1>>m>>s+1;
    //构造ne数组
    for(int i=2,j=0;i<=n;i++)
    {
        while(j && p[i]!=p[j+1])j=ne[j];
        if(p[i]==p[j+1])j++;
        //while if不可替换位置
        ne[i]=j;
    }
    for(int i=1,j=0;i<=m;i++)
    {
        while(j&&s[i]!=p[j+1])j=ne[j];
        if(s[i]==p[j+1])j++;
        if(j==n)
        {
            cout<<i-n<<" ";
            j=ne[j];//？
        }
    }
    return 0;
}
~~~



# 五、树

## SUM

![image-20240929191740657](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240929191740657.png)

## ==树的存储结构==

### 1、双亲表示法



![image-20240929191601508](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240929191601508.png)

**增**：无需按照层序插入新结点



**删除结点**：

有**两种**方案 ，**第一种**使双亲指针设置为-1  

第二种将尾部数据移到该位置将其覆盖！！（good）



缺点 ： 如果删除的不是叶子结点的话就会有问题 ，因为要删除儿子结点，这就涉及到了查询操作，

所以要**从头开始遍历**，如果用第一个删除，还要判断这个无效数据，就更慢了



### 2、孩子表示法（邻接表）-->hash表&树/图的存储

[hash表](#十五、哈希表(散列查找))

**就是邻接表！！！**

### **<font color=red size=25>3、孩子兄弟表示法</font>**

<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240929193349960.png" alt="image-20240929193349960" style="zoom:150%;" />



#### 初始化

~~~c++
//左第一个儿子
//右兄弟
typedef struct CSNode
{
    int val;
    CSNode * firstSon,rightBrother;//层次不一样！！ 类比leftchild 和 rightchild
    
}*CSTree;
~~~

树与森林都可以转化为二叉树 然后操作就如[二叉树](#二叉树)

## 树与二叉树的转化

![image-20240929195721503](C:/Users/33813/AppData/Roaming/Typora/typora-user-images/image-20240929195721503.png)







## 森林和二叉树的转化

![image-20241017201857035](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017201857035.png)



![image-20241017202042876](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017202042876.png)

## SUM



![image-20241017202110296](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017202110296.png)

### 树的遍历

#### 先根遍历

**第一次经过就访问！**



![image-20241017203219748](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017203219748.png)

#### 后根遍历

**最后一次经过才访问**

![image-20241017203304337](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017203304337.png)

**等效于二叉树的中序遍历**

#### 层次遍历

![image-20241017203331994](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017203331994.png)

**先根后根都是dfs**

**层次是bfs**





### 森林的遍历

#### 先序遍历

![image-20241017203434814](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017203434814.png)

#### 中序遍历

![image-20241017203438865](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017203438865.png)

![image-20241017203442009](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017203442009.png)

**以下为等效遍历**

### SUM



![image-20241017203448919](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017203448919.png)

**问题：如何使用代码将森林和树转化为二叉树！**

Todo：

~~~C++
#include<iostream>
using namespace std;

struct Tree {
    int data;
    Tree *first_child;  // 第一个孩子
    Tree *self_bro;     // 兄弟节点

    // 构造函数
    Tree(int x) : data(x), first_child(nullptr), self_bro(nullptr) {}
};

// 添加孩子节点
void addChild(Tree *parent, int x) {
    Tree *newNode = new Tree(x);
    
    // 如果parent还没有孩子，就直接添加为第一个孩子
    if (parent->first_child == nullptr) {
        parent->first_child = newNode;
    } else {
        // 如果已经有孩子，找到最后一个兄弟节点，将新节点作为它的兄弟
        Tree *child = parent->first_child;
        while (child->self_bro != nullptr) {
            child = child->self_bro;
        }
        child->self_bro = newNode;
    }
}

// 前序遍历树（孩子兄弟表示法）
void preOrder(Tree *root) {
    if (root == nullptr) return;

    // 打印当前节点
    cout << root->data << " ";

    // 先递归遍历第一个孩子
    preOrder(root->first_child);
    
    // 再递归遍历兄弟节点
    preOrder(root->self_bro);
}

int main() {
    // 创建根节点
    Tree *root = new Tree(1);
    
    // 添加子节点和兄弟节点
    addChild(root, 2);  // 2作为1的孩子
    addChild(root, 3);  // 3作为1的孩子的兄弟
    addChild(root, 4);  // 4作为1的孩子的兄弟
    
    // 给2节点添加孩子
    addChild(root->first_child, 5);   // 5作为2的孩子
    addChild(root->first_child, 6);   // 6作为5的兄弟
    addChild(root->first_child, 7);   // 7作为6的兄弟

    // 前序遍历树，验证结构
    cout << "Pre-order traversal of the tree: ";
    preOrder(root);
    cout << endl;

    return 0;
}
~~~



## ==二叉树==

### 完全二叉树

### 判断是否是完全二叉树

**使用bfs存 存第一个NULL（也可以存别的东西等效替代 如正无穷） 如果null之后队列还有数的话就说明不是完全二叉树！！**

![image-20241017163824454](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017163824454.png)

### ==顺序存储==

#### 初始化

~~~C++
//tree[]
//Size
    int n;
    cin>>n;
    Size=n;
    for(int i=1;i<=Size;i++)cin>>tree[i];//构造
~~~

#### 求树的深度

~~~c++
int dfs(int u)//返回树的深度
{
    if(u*2>Size)
    return 1;
     height=dfs(u*2)+1;//符合 完全二叉树/满二叉树
    //max(dfs(u*2),dfs(u*2+1))+1;//普通树
    
    return height;
 
}
~~~

#### 求树的遍历顺序

~~~C++
void trace(int u)//输出递归路线
{
    if(u*2>Size)//当到达树的叶子结点时
    {
        cout<<u<<' ';
        return ;
    }
    
    cout<<u<<' ';//到达每一层的操作
    
    trace(u*2);
    //返回后做操作
    trace(u*2+1);
    //返回后做操作
    
}

//OR---------------------------------------------------------------------------------------------------

 void trace(int u)//输出递归路线
{
    if(u>Size)return ;//溢出深度时
    
    cout<<u<<' ';
    
    trace(u*2);
    //返回后做操作
    trace(u*2+1);
    //返回后做操作
}
   
~~~

### ==链式存储==

#### 初始化

~~~C++
typedef struct listTreeNode
{
    int val;
    listTreeNode *lchild;
    listTreeNode *rchild;
    
    listTreeNode(int x):val(x),lchild(nullptr),rchild(nullptr){}
    
}*ListTree;
~~~



#### 构造树（bfs）

~~~C++
//利用 层序遍历 构造完全二叉树(bfs)
void creatNode(int x,listTreeNode *l)//传入根节点
{
    queue<listTreeNode*>q;
    q.push(l);//让根结点入队
    listTreeNode *newNode=new listTreeNode(x);
    
    while(!q.empty())//队列不空
    {
     auto t=q.front();//提取队头
     q.pop();//弹出队头
     //寻找当前队头的邻居，并加入队列
    if(t->lchild!=nullptr) q.push(t->lchild);
    else 
    {
        t->lchild=newNode;
        return ;
        
    }
    
    if(t->rchild!=nullptr)q.push(t->rchild);
    else 
    {
        t->rchild=newNode;
        return ;
        
    }
    
    }
  
}
~~~

#### 前序遍历

~~~C++
void trace(ListTree t)
{
    if(t==nullptr)
    return ;
    
   cout<<t->val<<' ';//visit(u)
   
    trace(t->lchild);
  
    trace(t->rchild);
      
    
}
~~~

#### 计算深度

~~~C++
int height(listTreeNode *l)
{
    if(l->lchild==nullptr)
    return 1;
    
    return height(l->lchild)+1;
    
}
~~~



#### 测试数据

~~~c++
int main()
{
    int n;
    cin>>n;
    listTreeNode *l=new listTreeNode(0);
    for(int i=0;i<n;i++)
    {
        int x;
        cin>>x;
        if(i==0)
        {
         l->val=x;   
         continue;
        }
        
        
        creatNode(x,l);
        
    }
    trace(l);
    
    
    
    return 0;
}
~~~

## 树的前序/中序/后序遍历 构建树

## 树的非递归形式输出前序/中序/后序遍历序列

![image-20241206142828150](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241206142828150.png)

~~~c++
#include<iostream>
using namespace std;
// global
typedef struct biotree
{
    char data;
    biotree *lc;
    biotree *rc;
    biotree(char val):data(val),lc(nullptr),rc(nullptr){};
    
};
biotree* createTree() //返回从根节点开始的整棵树
{
    char c;
    cin>>c;
    if(c == '#')
        return nullptr;
    else
        {
            biotree *newnode = new biotree(c);
            newnode->lc = createTree(); // 利用返回值连接 --》 思考
            newnode->rc = createTree();
            return newnode;
            
        }
}

void middleTraveler(biotree *root)
{
    
    if(root == nullptr)
    return ;
    
    int top = -1;
    biotree *nodestack[100];
    // 先将根节点弹入栈顶
    biotree *p = root;
    while(p || top>=0)
    {
        if(p)
        {
            nodestack[++top] = p;
            p = p->lc;
            // 优先往左边找
        }
        else // 如果当前结点的左边是空（说明已经是最左边的一个了）就到当前结点的右边
        {
          cout<<nodestack[top]->data<<' ';
          p = nodestack[top--]->rc; // 再去右子树中找最左边的结点
          
        }
    }
}
int main()
{
    
    
    biotree *root = createTree();
    middleTraveler(root);
    
  
    
    return 0;
}
~~~

**输入：ABC#D##E##FG##H## （==前序==）**
**输出：C D B E A G F H  （==中序==）**

存到栈里就相当于是进入递归下一层

**弹出栈就是返回上一层**

**旧知识推新知识非常重要**





## 线索二叉树

### 	线索二叉树的中序/前序/后序遍历序列

​	![image-20241110190454478](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110190454478.png)

### 问题 ：如果从某个节点开始能否开始中序遍历整颗二叉树？

![image-20241110190859359](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110190859359.png)

## 中序~线索二叉树的存储

![image-20241110190938336](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110190938336.png)

**==指向前驱和后继的指针就是线索==**

![image-20241110191122369](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191122369.png)

![image-20241110191135518](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191135518.png)

### 找中序前驱

#### 土方法：





![image-20241110191154758](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191154758.png)

#### 线索化查找：

### 中序线索化：



![image-20241110191321314](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191321314.png)

### 先序线索化

![image-20241110191324208](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191324208.png)

![image-20241110191358251](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191358251.png)

![image-20241110191401045](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191401045.png)

### 后序线索化：



![image-20241110191435896](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191435896.png)

# ==《通过线索二叉树找前驱/后继》==



### 找中序后继：

![image-20241110191643405](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191643405.png)

![image-20241110191752039](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191752039.png)

### 找中序前驱：



![image-20241110191808466](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191808466.png)

![image-20241110191814016](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191814016.png)

### 找先序后继：



![image-20241110191825685](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191825685.png)

### 找先序前驱:

![image-20241110191839090](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191839090.png)

### 找后序前驱：

![image-20241110191850562](C:/Users/33813/AppData/Roaming/Typora/typora-user-images/image-20241110191850562.png)

### 找后序后继：



![image-20241110191904128](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191904128.png)

![image-20241110191916949](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241110191916949.png)















## 哈夫曼树

### 代码实现

~~~C++
~~~

**WPL：树的带权路径长度！！！**

### SUM



![image-20241017211415016](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017211415016.png)

## trie树（拓展）

~~~C++
~~~



# 六、并查集

![image-20241009203612672](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009203612672.png)

## 简单方法

~~~C++
#include<iostream>
using namespace std;
//----------------------------------------------------------------------
#define size 13 //初始化结点个数
int UFset[size];//节点编号
int val[size];//结点值 
//------------------------------------------------------------------------field
int find(int s[],int x)//返回x所属的根节点
{
    while(s[x]>=0) x=s[x];
    return x;
    
}

void Union(int s[],int root1,int root2)//合并集合
{
    if(root1==root2)return ;
    else s[root1]=root2;
    
}
//---------------------------------------------------------------------function
int main()
{
    int n;
    cin>>n;
    
    for(int i=0;i<size;i++)UFset[i]=-1;//只有 s[x]是 -1 的才是 根结点 ---initialize
    for(int i=0;i<n;i++)
    {
        int x;
        cin>>x;
        val[i]=x;//--------------------//赋值（assignment）
    }
    
    cout<<val[find(UFset,4)]<<endl;//一开始都是离散的点根节点都是本身
    
    Union(UFset,find(UFset,0),find(UFset,1));
    Union(UFset,find(UFset,1),find(UFset,2));
    Union(UFset,find(UFset,3),find(UFset,4));
    if(find(UFset,3)==find(UFset,2))cout<<1;
    else cout<<0;

    
    
    return 0;
}
~~~

**==缺点==： union操作有可能会使大树合并到小树上导致树的深度增加，导致下次find时要耗费很长时间**

## 时间复杂度：

union 内部操作为O(1)（前提是已经查到了root）;

而一次find操作最差情况的时间复杂度 是 O(n) 在n个结点且深度刚好为n的情况下、

---



## 优化union

**==主要思路==：  就是将小树并到大树上避免树的深度越来越深**

**操作：让s[root]不存-1 而是存 -（该root 树下面的结点数包括自身）**

~~~C++}
void Union(int s[],int root1,int root2)//优化
{
    if(root1==root2)return ;
    
    if(s[root2]<s[root1])//注意是负数
    {
       
        s[root2]+=s[root1]; 
        s[root1]=root2;
    }
    else
    {
        // s[root2]=root1;
        s[root1]+=s[root2];w
        s[root2]=root1;
        //注意顺序问题
    }
    
}
~~~

最坏时间情况为O(logn)

## （压缩路径）

~~~C++
int find(int x)//找到编号为x的结点的根节点
{
    if(x!=p[x])
        p[x]=find(p[x]);
        
        //return x; 不能
         return p[x];
        
}
//p【root】=root
~~~

时间复杂度 为O (logn)

**递的过程找到根结点**

**归的时候让所有结点指向根结点**

![image-20241009211307951](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009211307951.png)



![image-20241009211933606](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009211933606.png)

## ’终极‘优化（不是按深度来比较的！）

**而是按结点总数来比较的！**

**结合压缩路径和小树合并到大树！**

（按size结点大小）

~~~C++
#include<iostream>
using namespace std;
const int N=1e5+10;
int p[N];
int find(int x)
{
    return p[x]>=0?p[x]=find(p[x]):x;
}

int main()
{
  int n;
  cin>>n;
  
  for(int i=1;i<=n;i++)p[i]=-1;//只有根的p[root]才是负数 并且绝对值等于这个集合的结点数

  int u;
  cin>>u;
  while(u--)//并 主要是在这个操作优化
  {
    int a,b;
    cin>>a>>b;
    int pa=find(a);
    int pb=find(b);
    if(pa==pb)
    continue;
    if(p[pa]<p[pb])//注意负数
    {
       
        p[pa]+=p[pb];
         p[pb]=pa;
    }
    else
    {
      p[pb]+=p[pa];
       p[pa]=pb;
    }
  }
  int q;
  cin>>q;
  while(q--)
  {
    int a,b;
    cin>>a>>b;
    if(find(a)==find(b))
      puts("Yes");
    else
      puts("No");
    
  } 

  return 0;
}
~~~

![image-20241015213454839](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015213454839.png)

**如果是按size比较的话 就将深度高的接到深度低的上了 就会增加深度**

## 真·终极优化（按深度）

~~~C++
#include<iostream>
using namespace std;
const int N=1e5+10;
int p[N];
int height[N];//高度只存在根节点上
int find(int x)
{
    return p[x]!=x?p[x]=find(p[x]):x;
}

int main()
{
  int n;
  cin>>n;
  
  for(int i=1;i<=n;i++)
  {
    p[i]=i;
    height[i]=1;
  }
  int u;
  cin>>u;
  while(u--)//并
  {
    int a,b;
    cin>>a>>b;
    int pa=find(a);
    int pb=find(b);
    if(pa==pb)
    continue;
    if(height[pa]<height[pb])
      p[pa]=pb;
    else if(height[pa]>height[pb])
      p[pb]=pa;
    else
    {
      p[pa]=pb;
      height[pb]++;
    }
    
    
  }
  int q;
  cin>>q;
  while(q--)
  {
    int a,b;
    cin>>a>>b;
    if(find(a)==find(b))
      puts("Yes");
    else
      puts("No");
    
  } 
  for(int i=1;i<=n;i++)
  {
      cout<<height[i]<<' ';
  }


 

  return 0;
}
~~~

**将深度小的接到深度高的上面去！！！！**

（使用数组存height深度）



# 七、图

[邻接表入门](#五、树)

## 1.图的存储

#### 1.邻接矩阵（适用于 稠密图 ）

**边如果很少（稀疏图）就会有很多空间浪费**



![image-20241009213321006](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009213321006.png)

##### 定义

~~~C++
typedef struct 
{
    char vex[N];//顶点信息可以是结构体
    int edge[N][N];//边  无权图的话可以是bool类型
    int vexnum ,arcnum;
    //存储这个图的点个数和边个数
}graph;
~~~

![image-20241009213547037](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009213547037.png)

~~~C++

int main()
{
    int n;//n个顶点
    cin>>n;
    graph g;
    for(int i=0;i<n;i++)cin>>g.vex[i];
    //edge[a][b] a->b;
    int q;
    cin>>q;
    while(q--)
    {
        int a,b;//连接两个顶点
        cin>>a>>b;//输入两个顶点的编号
        g.edge[a][b]=1;
        g.edge[b][a]=1;
    }//建立图的关系
    int ans=0;//记录这个图的度
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
             if(g.edge[i][j])
             ans++;
            cout<<g.edge[i][j]<<" ";
        }
        cout<<endl;
    }
        cout<<ans/2;//度的数量
    
    return 0;
}
~~~



##### 带权图的存储



![image-20241009213558354](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009213558354.png)



**带权图先初始化所有边是0或者正无穷的都是可以的！**

![image-20241009213605823](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009213605823.png)







> 涉及线性代数和矩阵的存储
>
> ![image-20241009214016575](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009214016575.png)
>
> 



##### 邻接矩阵的性质（涉及压缩矩阵的存储）



![image-20241009213628105](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009213628105.png)





![image-20241009213635502](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009213635502.png)

![image-20241009213642866](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009213642866.png)

#### 2.邻接表（适用于稀疏图）

![image-20241009220501867](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009220501867.png)

---





![image-20241009220508380](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009220508380.png)

---





![image-20241009220514633](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241009220514633.png)



> **vertices 顶点集（合）**
>
> **vertex 顶点**



##### 初始化&&定义

~~~C++
const int N=1e3;
int n;

typedef struct Arcnode  // 弧/边
{
    int adjvex;//指向的顶点的编号
    Arcnode *next;
    
}Arcnode;//相当于是链表结点
//好习惯

typedef struct Vnode //顶点结构体结点 (存每个结点的信息)
{
    int val;//结点的值
    Arcnode *first;//存这个结点的头指针位置
    
}adjList[N];//存每个结点

//存图结构体
typedef struct 
{
  adjList vertices;// 数组类型 顶点集合
  int vexnum,arcnum;//顶点总和和边/弧总数
}graph;


void initialize(graph *g)//传入地址
{
    for(int i=0;i<n;i++)g->vertices[i].first=nullptr;
}
~~~

##### 添加边结点

~~~C++
void add(graph *g,int a,int b)//传入结点编号   ~~不带头结点的
{
  Arcnode *newNode = new Arcnode;
  newNode->adjvex=b;
  newNode->next=g->vertices[a].first;
  g->vertices[a].first=newNode;
  
  
  Arcnode *newNode_reverse =new Arcnode;
  newNode_reverse->adjvex=a;
  newNode_reverse->next=g->vertices[b].first;
  g->vertices[b].first=newNode_reverse;
  

  
}//功能：a<->b 插入(无向图)
~~~

##### 传参和基本操作注意（c语言和c++特性区别）

~~~C++
    graph g; //注意c语言和c++区别
    cin>>n;//结点个数 
    initialize(&g);//c语言特性 传参函数形参那边不允许写& 所以尽量写指针形式
    for(int i=0;i<n;i++)cin>>g.vertices[i].val;//输入结点值
   
    int q;
    cin>>q;
    while(q--)
    {
        int a,b;
        cin>>a>>b;
        //连接结点
        add(&g,a,b);
    
        
    }
    int x=0;
    while(cin>>x)
    {
        for(Arcnode *i=g.vertices[x].first;i!=nullptr;i=i->next)
            cout<<i->adjvex<<' ';
         //枚举类型注意
         //注意释放内存（when）
         
    }
~~~

##### 对于 有向图 枚举 入边 和 出边（简单）

~~~C++
    //枚举入边
    int x;
    cin>>x;
    for(int i=0;i<n;i++)//枚举每一个编号
    {
        if(i==x)
            continue;
        for(Arcnode *j=g.vertices[i].first;j!=nullptr;j=j->next)
        {
           if(j->adjvex==x)
            cout<<i<<' ';//此为入边的结点
        }
        cout<<endl;
    }  
~~~



## 2.==图的基本操作==（对于邻接表和邻接矩阵）

> **注意：有无向图有向图之分！！！**

### 判断图是否存在边<x,y> 有向边（弧） （x,y） 无向边

对于邻接表：遍历链表 时间复杂度：O(1)~O(|V|)  （考虑最好和最坏情况）

![image-20241010224253432](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224253432.png)

---





![image-20241010224311616](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224311616.png)
---

---





![image-20241010224337676](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224337676.png)

---

![image-20241010224346968](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224346968.png)

**邻接矩阵的删除**

---



![image-20241010224404081](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224404081.png)

**邻接表的删除**

---



 ![image-20241010224512653](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224512653.png)

**有向图的删除**

---

![image-20241010224520701](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224520701.png)

**对于邻接表直接头插法即可！！**

---

![image-20241010224528077](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224528077.png)



---



![image-20241010224535557](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224535557.png)

---

![image-20241010224543631](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224543631.png)

---



**带权图的权值获取和查询**

![image-20241010224550180](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241010224550180.png)

---



## 3. 图的遍历

### 1.图的BFS遍历

> **对于  <无向图>  && <邻接表>  的bfs**

~~~C++
#include<iostream>
using namespace std;
const int N=1e3;
int n;

int q[N];

typedef struct Arcnode  // 弧/边
{
    int adjvex;//指向的顶点的编号
    Arcnode *next;
    
}Arcnode;//相当于是链表结点
//好习惯

typedef struct Vnode //顶点结构体结点 (存每个结点的信息)
{
    int val;//结点的值
    Arcnode *first;//存这个结点的头指针位置
    
}adjList[N];//存每个结点

//存图结构体
typedef struct 
{
  adjList vertices;// 数组类型 顶点集合
  int vexnum,arcnum;//顶点总和和边/弧总数
}graph;

void add(graph *g,int a,int b)//传入结点编号   ~~不带头结点的
{
  Arcnode *newNode = new Arcnode;
  newNode->adjvex=b;
  newNode->next=g->vertices[a].first;
  g->vertices[a].first=newNode;
  
  Arcnode *newNode_reverse = new Arcnode;
  newNode_reverse->adjvex=a;
  newNode_reverse->next=g->vertices[b].first;
  g->vertices[b].first=newNode_reverse;
  
}//功能：a<->b 插入(无向图)
void initialize(graph *g)//传入地址
{
    for(int i=0;i<n;i++)g->vertices[i].first=nullptr;
}
void bfs(graph *g,int v)//从结点v开始的bfs遍历
{
    //初始化
    bool st[N];//标记是否访问过
    int hh=0,tt=-1;
    q[++tt]=v;
    st[v]=1;
    
    while(tt>=hh)//队列不空
    {
        int t=q[hh++];//取弹队头
        for(Arcnode *i=g->vertices[t].first;i!=nullptr;i=i->next)
        {
           if(!st[i->adjvex])
           {
               cout<<i->adjvex<<" ";
               st[i->adjvex]=1;
               q[++tt]=i->adjvex;
               
           }
           
        }
    }
    
}
int main()
{
    graph g;
  
    cin>>n;//结点个数 
    initialize(&g);
    for(int i=0;i<n;i++)cin>>g.vertices[i].val;//输入结点值
    
  
    
    int q;
    cin>>q;
    while(q--)
    {
        int a,b;
        cin>>a>>b;
        //连接结点
        add(&g,a,b);
    
        
    }
    bfs(&g,0);
  
  
    
    return 0;
}
~~~



#### 如果图不止一个连通块

#### -->就无法遍历完所有顶点!!!\

>  **所要添加的操作是：**

~~~C++
void bfs(graph *g,int v)//从结点v开始的bfs遍历
{
    //初始化
    cout<<v<<" ";
    int hh=0,tt=-1;
    q[++tt]=v;
    st[v]=1;
    
    while(tt>=hh)//队列不空
    {
        int t=q[hh++];//取弹队头
        for(Arcnode *i=g->vertices[t].first;i!=nullptr;i=i->next)
        {
           if(!st[i->adjvex])
           {
               cout<<i->adjvex<<" ";
               st[i->adjvex]=1;
               q[++tt]=i->adjvex;
               
           }
           
        }
    }
    
}

void bfsTraveler(graph *g)
{
  for(int i=0;i<n;i++)st[i]=0;
  //先初始化

  for(int i=0;i<n;i++)
  {
      if(!st[i])
      {
         bfs(g,i); 
         cout<<endl<<"-------"<<endl;
      }
       
       
  }
  
    
}
~~~

### 复杂度分析

![image-20241011192142663](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011192142663.png)





---

### 广度优先生成树

![](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011192137652.png)



### 2.图的DFS遍历

> 针对于 无向图 和 邻接表的dfs遍历

~~~C++
void dfs(graph *g,int v)
{
    
    for(Arcnode *i=g->vertices[v].first;i!=nullptr;i=i->next)
    {
      
        if(!st[i->adjvex])
        {   
            cout<<i->adjvex<<' ';
            st[i->adjvex]=1;
            dfs(g,i->adjvex);
        }
    }
    
}
~~~

#### 如果图不止一个连通块

#### -->就无法遍历完所有顶点!!!

~~~C++
void dfs(graph *g,int v)
{
    cout<<v<<" ";//为什么结点处理放这里可以（一定满足）
    
    for(Arcnode *i=g->vertices[v].first;i!=nullptr;i=i->next)
    {
        if(!st[i->adjvex])
        {   
            st[i->adjvex]=1;
            dfs(g,i->adjvex);
        }
    }
    
}


void dfstravel(graph *g)
{
       
    
    for(int i=0;i<n;i++)st[i]=0;//初始化
  

    for(int i=0;i<n;i++)
    {
        
        if(!st[i])
        {
          st[i]=1;
          dfs(g,i);  
          cout<<endl<<"--------"<<endl;
        }
            
    }
}
~~~



### 复杂度分析

![](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011210933645.png)

**思维：dfs找全部解，一旦tle了就记忆化，剪枝或者改为bfs（最短路），实在不行就dp！！**



![image-20241011211122218](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211122218.png)

---



![image-20241011211157535](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211157535.png)

![image-20241011211202359](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211202359.png)

---



### 深度优先生成树/森林

![image-20241015133355580](C:/Users/33813/AppData/Roaming/Typora/typora-user-images/image-20241015133355580.png)



![image-20241011211207045](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211207045.png)

![image-20241011211211264](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211211264.png)

![image-20241011211215101](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211215101.png)

---









## *最短路

### 0.bfs  （✓） （win + .）



### 1.dijkstra

![image-20241013142449294](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013142449294.png)

![image-20241013142453353](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013142453353.png)

```C++
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 510;

int n, m;
int g[N][N];
int dist[N];//记录最短路径！！
bool st[N];//标记是否找到最短路

int dijkstra()
{
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;//标记起点

    for (int i = 0; i < n - 1; i ++ )
    {
        int t = -1;
        for (int j = 1; j <= n; j ++ )
            if (!st[j] && (t == -1 || dist[t] > dist[j]))// 找到当前未标记的节点中距离最小的节点
                t = j;

        for (int j = 1; j <= n; j ++ )
            dist[j] = min(dist[j], dist[t] + g[t][j]);// 更新邻接节点的距离

        st[t] = true;
    }

    if (dist[n] == 0x3f3f3f3f) return -1;
    return dist[n];
}

int main()
{
    scanf("%d%d", &n, &m);

    memset(g, 0x3f, sizeof g);
    while (m -- )
    {
        int a, b, c;
        scanf("%d%d%d", &a, &b, &c);

        g[a][b] = min(g[a][b], c);//防止重边
    }

    printf("%d\n", dijkstra());

    return 0;
}


```

### 时间复杂度（与prim极其类似）

### 2.floyd



**key：中转点**

![image-20241013140817638](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013140817638.png)

![image-20241013140846502](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013140846502.png)







~~~C++
#include<iostream>
#include<cstring>
using namespace std;
const int N=1e3+10;
int mp[N][N];
int vex[N];
int n;
int path[N][N];
void floyd()
{
    for(int i=0;i<n;i++)//枚举中转点
        for(int j=0;j<n;j++)
            for(int k=0;k<n;k++)
                if(mp[j][k]>mp[j][i]+mp[i][k])
                {
                    mp[j][k]=mp[j][i]+mp[i][k];
                    path[j][k]=i;//类似bfs中的last数组记录路径
                }      
     
}

int main()
{
  
    cin>>n;
    memset(mp,0x3f,sizeof mp);//0x3f3f3f3f
    memset(path,-1,sizeof path);
   int x;
   cin>>x;
    while(x--)
    {
      int a,b,val;
      cin>>a>>b>>val;
      mp[a][b]=mp[b][a]=val;//两个连等号
      
    }
    floyd();
  
    int st,ed;
    cin>>st>>ed;
    while(ed!=st)
    {
        cout<<ed<<' ';
        ed=path[st][ed];
        
    }
    return 0;
}
~~~

**时空复杂度：0(v3次方) o(v2次方)**

**floyd可以解决带负权边的问题！**



![image-20241013141204822](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013141204822.png)



![image-20241013141213311](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013141213311.png)

**时空复杂度具体还是得看图的存储结构**

---

# 拓扑排序（可判断回路）

**key ： 拓扑排序一定是有向无环图！**



![image-20241013143603689](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013143603689.png)

![image-20241013143703056](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013143703056.png)

### 邻接矩阵法

~~~C++
#include<iostream>
#include<vector>
using namespace std;
const int N=10000;
int g[N][N];
int st[N];
int top=0;
int cnt;//记录当前的顶点数
int n;
int inedge[N];
vector<int>ans;
int bfs()
{
       while(top)
    {
        ans.push_back(st[top]);
        int t=st[top];
        cnt++;
        top--;
        for(int i=1;i<=n;i++)
        {
            if(g[t][i])
            {
              inedge[i]--;  
                   
            if(inedge[i]==0)
            {
              st[++top]=i;  
              g[t][i]=0;//删去这条边
            }
            
            }
        }
        
        
    }
    if(cnt<n)
        return 0;
    else
        return 1;
}
int main()
{
 
    cin>>n;
    int x;
    cin>>x;
    while(x--)
    {
        int a,b;
        cin>>a>>b;
       
        if(!g[a][b])//防止重边重复计数
        inedge[b]++;//统计入边  
        g[a][b]=1;//表明有边
    }
    for(int i=n;i>=1;i--)
    {
        if(inedge[i]==0) 
            st[++top]=i;
    }
    //先存储入度为0的点
    if(bfs())
        for(int i=0;i<n;i++)
            cout<<ans[i]<<' ';
    else
        cout<<-1;

//  for(int i=1;i<=n;i++)cout<<inedge[i]<<' '; 
    
}
~~~

### 邻接表写法

~~~C++
#include<iostream>
#include<vector>
using namespace std;
const int N=1e5+10;
vector<int>ans;
int st[N];
int top;
int inedge[N];

int n;
typedef struct ArcNode
{
    int adjvex;
    ArcNode *next;
}ArcNode;

typedef struct vexNode
{
    int val;
    ArcNode *first;//头结点
}verlist[N];
typedef struct graph
{
    verlist vertices;//顶点集
    int numvex,numedge;
   
    
}graph;
void add(graph *g,int a,int b)
{
    ArcNode *n1=new ArcNode();
    n1->adjvex=b;
    n1->next=g->vertices[a].first;
    g->vertices[a].first=n1;
    
}
int bfs(graph *g)
{
    int cnt=0;
    while(top)
    {
        int t=st[top--];//这里就是对队列中的元素处理
        cnt++;
        ans.push_back(t);
        for(ArcNode *i=g->vertices[t].first;i!=nullptr;i=i->next)
        {
            inedge[i->adjvex]--;//因为在这个循环中把所有出边都删除了
            if(inedge[i->adjvex]==0)
            {
                st[++top]=i->adjvex;
                
            }
        }
        
    }
    if(cnt<n)return 0;
    else
    return 1;
}
int main()
{
    graph g;

    cin>>n;
    for(int i=1;i<=n;i++)g.vertices[i].first=nullptr;//一定要初始化
    int x;
    cin>>x;
   
    while(x--)
    {
        int a;
        int b;
        cin>>a>>b;
     
            add(&g,a,b); 
    }
    for(int i=1;i<=n;i++)
    {
      for(ArcNode *h=g.vertices[i].first;h!=nullptr;h=h->next)
      {
          inedge[h->adjvex]++;
      }
    }
    // for(int i=1;i<=n;i++)
    //     if(inedge[i]==0)
    //         st[++top]=i;
    // if(bfs(&g))
    //     for(auto c: ans)
    //         cout<<c<<' ';
    // else
    //     cout<<-1;
        cout<<inedge[2];
 
    
}

~~~

**注意点：初始化问题 nullptr 一定！！**

**删除边问题**



### 逆拓扑排序（使用dfs）

### 对于逆序 考虑dfs（递归栈）

#### 整体

~~~c++

    #include<iostream>
    #include<vector>
    using namespace std;
    const int N=1e5+10;
    vector<int>ans;
    bool flag[N];
    int n;
    typedef struct ArcNode
    {
        int adjvex;
        ArcNode *next;
    }ArcNode;
    
    typedef struct vexNode
    {
        int val;
        ArcNode *first;//头结点
    }verlist[N];
    typedef struct graph
    {
        verlist vertices;//顶点集
        int numvex,numedge;
       
        
    }graph;
    void add(graph *g,int a,int b)
    {
        ArcNode *n1=new ArcNode();
        n1->adjvex=b;
        n1->next=g->vertices[a].first;
        g->vertices[a].first=n1;
        
    }
    
      void dfs(graph *g,int v)//起点
    {
        for(ArcNode *i=g->vertices[v].first;i!=nullptr;i=i->next)
        {
            if(!flag[i->adjvex])
            {
              flag[i->adjvex]=1;
              dfs(g,i->adjvex);  
              
            }
            
        }
        cout<<v<<' ';
        
    }
    
    
    
    void dfstravel(graph *g)
    {
        for(int i=1;i<=n;i++)
        flag[i]=0;
        //初始化
        for(int i=1;i<=n;i++)//从入度为零的点开始
        {
            if(!flag[i])
            {
            
                dfs(g,i);
            }
            
        }
        
    }
  
    int main()
    {
        graph g;
    
        cin>>n;
        for(int i=1;i<=n;i++)g.vertices[i].first=nullptr;//一定要初始化
        int x;
        cin>>x;
       
        while(x--)
        {
            int a;
            int b;
            cin>>a>>b;
         
            add(&g,a,b); 
        }
        dfstravel(&g);
        
            
      
        
    }

~~~

#### 核心代码

~~~C++
 
      void dfs(graph *g,int v)//起点
    {
        for(ArcNode *i=g->vertices[v].first;i!=nullptr;i=i->next)
        {
            if(!flag[i->adjvex])
            {
              flag[i->adjvex]=1;
              dfs(g,i->adjvex);  
              
            }
            
        }
        cout<<v<<' ';
        
    }
    
    
    
    void dfstravel(graph *g)
    {
        for(int i=1;i<=n;i++)
        flag[i]=0;
        //初始化
        for(int i=1;i<=n;i++)//从入度为零的点开始
        {
            if(!flag[i])
            {
            
                dfs(g,i);
            }
            
        }
        
    }

~~~

![image-20241013170231676](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241013170231676.png)

# 关键路径





# 八、最小生成树

**连通图概念：从一个顶点可以到达任意一个顶点（都有路径）**

生成树：表示所有顶点均由边连接在一起，但**不存在回路**的图

## 1.prim算法

![image-20241011211526962](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211526962.png)

![image-20241011211542709](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211542709.png)

![image-20241011211551109](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211551109.png)

---



## prim实现操作

![image-20241011211950682](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211950682.png)

![image-20241011212001654](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011212001654.png)

![image-20241011212008783](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011212008783.png)

![image-20241011212123191](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011212123191.png)

![image-20241011212129170](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011212129170.png)

---







​	



## 2. kruskal算法

![image-20241011211618541](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211618541.png)

![image-20241011211634355](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211634355.png)

## kruskal实现操作（并查集）



![image-20241011212138688](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011212138688.png)

![image-20241011212205046](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011212205046.png)

![image-20241011212208675](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011212208675.png)

![image-20241011212211415](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011212211415.png)



## ==sum==

![image-20241011211648769](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241011211648769.png)



# 有向无环图 的表达式求值

![image-20241015164413069](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015164413069.png)



![image-20241015164423599](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015164423599.png)

![image-20241015164431523](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015164431523.png)

![image-20241015164437958](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015164437958.png)



# ==-------《查找》--------==



**查找长度的概念：对比关键字的次数！**

## 查找的基本概念



![image-20241016211125959](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016211125959.png)

---



![](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016211217831.png)

## 查找算法的效率分析

![image-20241016211256652](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016211256652.png)

## 平均查找长度公式：

![image-20241016211347984](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016211347984.png)

**注意：ASL的数量级反映了这个查找算法的时间复杂度！**



# 1^o^   顺序查找

![image-20241017192820102](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017192820102.png)

**带哨兵与不带哨兵 仅有微妙的区别 重点在于 查找成功和查找失败的情况**

ASL= （每个点查找次数 乘上查找概率 ）之和

**通过 有序 来优化算法**

![image-20241017193115000](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017193115000.png)

![image-20241017193548148](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017193548148.png)





# 2^o^   折半查找（二分）

## 构造二分查找判定树



![image-20241017193951847](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017193951847.png)

---



![image-20241017193935293](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017193935293.png)

## 折半查找判定树的树高h：



![image-20241017195049820](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017195049820.png)

![image-20241017195110393](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017195110393.png)

---

## 时间复杂度

![image-20241017195225185](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017195225185.png)

---







## 查找成功与查找失败

**二分查找判定树  是个二叉排序树 + 二叉平衡树** 

**所以对于一个结点数为n的空链域就有n+1个！**



## sum

![image-20241017194037958](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017194037958.png)

**不对称的分为左/右多的两种情况**

![image-20241017210430792](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017210430792.png)



---



# 3^o^   分块查找

![image-20241017195431850](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017195431850.png)

## 可用折半/顺序查找 查找 索引表



![](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017200134171.png)

## 二分查找逻辑

![image-20241017200314181](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017200314181.png)

**查找 4次？ 还是 5次？**



![image-20241017200318195](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017200318195.png)

**查找失败的情况较为复杂 重点在折半查找的查找成功和失败的情况上！！**

**可以用邻接表（拉链法）来动态存储 增删 方便（链表的优点！）**

![image-20241017200550250](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241017200550250.png)





# 九、二叉排序树（二叉搜索树）

## 二叉搜索树的定义

![image-20241015164542843](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015164542843.png)

## 查找



![image-20241015164709213](C:/Users/33813/AppData/Roaming/Typora/typora-user-images/image-20241015164709213.png)

##  插入

## ![image-20241015164737288](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015164737288.png)

## 构造



![image-20241015164756645](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015164756645.png)

## 删除分三种情况

### 1.结点是叶子结点 

**直接删除**

### 2.结点只有一边的子树



![image-20241015164836591](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015164836591.png)

### 3.结点两边都有子树

#### 又分为两种做法 ： 处理 后继和前驱 

![image-20241015165111380](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015165111380.png)

**根据二叉排序树的特性进行的措施！**

![image-20241015165124001](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015165124001.png)

## 查找效率分析

###  查找成功

![image-20241015165339468](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015165339468.png)

**最好情况：二叉树的最小高度为log2^n+1  平均查找长度为O (log2^n+1)**

**最坏情况：每个结点有且仅有一个分支 树高h=结点数n  退化为链表 ,平均查找长度为 o(n)**

**原因就是构造时的问题**

**解决方法：构造时构造==平衡二叉树！==**

### 查找失败

![image-20241015165750084](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241015165750084.png)

# 十、平衡二叉树



# 十一、红黑树



# 十二、B树



# 十三、B+树





# ==十四、堆==



## up和down逻辑



~~~c++
void up(int u)
{
    while(u/2>0&&h[u]<h[u/2])//指涉不为空
    {
        swap(h[u],h[u/2]);
        u/=2;//步进
    }
}
void down(int u)
{
    int t=u;//当前结点cur
    
    //比较三个值（前提是指涉不为空）
    if(u*2<=Size&&h[u*2]<h[t])t=u*2;
    if(u*2+1<=Size&&h[u*2+1]<h[t])t=u*2+1;
    //两个if都要判断
    
    if(t!=u)//如果确实要改变
    {
        swap(h[t],h[u]);
        down(t);//直到down到满足条件
    }
}
~~~

**堆是完全二叉树，下标是不会变化的，变化的仅有数据**

## 建堆

~~~C++
 cin>>n; 
    Size=n;
    for(int i=1;i<=Size;i++)cin>>h[i];//传入时都是离散的每一个点
    //!
    for(int i=n/2;i;i--)down(i);//从最后一个父节点开始建堆(建小根堆)
~~~



## 操作

### 1.插入一个数

~~~c++
void insert(int x)
{
    h[++Size]=x;
    up(Size);
    
}
~~~



### 2.求堆顶

`h[1]`

### 3.删除堆顶

~~~c++
void del()
{
    h[1]=h[Size--];
    down(1);
}
~~~



### 4.删除任意一个元素

~~~c++
void supDel(int k)//下标
{
    h[k]=h[Size--];
    //!
    up(k);
    down(k);
}
~~~



### 5.修改任意一个元素

~~~C++
void change(int k,int x)
{
    h[k]=x;
    //!
    up(k);
    down(k);
}
~~~





# 十五、哈希表(散列查找)

# 一、 拉链法



[树的相关知识](#五、树)

![image-20241016195939589](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016195939589.png)

**==特别的==：注意题目 如果位置上都没有数的话 就无需判断，也就是查找长度是 ==0== ！**

**冲突越多 查找效率越低**

![image-20241016202801877](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016202801877.png)

## 装填因子



---



![image-20241016202753965](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016202753965.png)

## 1.除留余数法

### 使用数组模拟

~~~C++
#include<iostream>
#include<cstring>
using namespace std;
const int N=100003;//第一个比长度大的质数（可以相等--> 尽可能接近）
int e[N],idx,h[N],ne[N];
void add(int x)
{
  int hash=(x%N+N)%N;
  e[idx]=x;
  ne[idx]=h[hash];
  h[hash]=idx++;


}
int find(int x)
{
  int hash=(x%N+N)%N;
  for(int i=h[hash];i!=-1;i=ne[i])
  {
    if(e[i]==x)
      return 1;
  }
  return 0;
}
int main()
{
  memset(h,-1,sizeof h); //初始化为-1
  int n;
  cin>>n;
  while(n--)
  {
    int x;
    cin>>x;
    add(x);
  }
  int x;
  cin>>x;
  cout<<find(x);
  

  return 0;
}
~~~

![image-20241016202329672](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016202329672.png)

![image-20241016203135175](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016203135175.png)

**但是使用mod 素数法也不一定是最优的 如果如上是连续的就不是最优的了 （具体题目具体分析！**）

此邻接表也可用于==建图== ！！ 

## Create Graph

==**h 存的都是下标指针一类的！！**==

~~~C++
#include<iostream>
#include<cstring>
using namespace std;
const int N=1e5+10;
int e[N],ne[N],h[N],w[N];
int idx;
void add(int a,int b,int weight)// a->b
{
  ne[idx]=h[a];
  h[a]=idx;
  e[idx]=b;
  w[idx++]=weight;

}
int main()
{
  memset(h,-1,sizeof h);//都要先初始化为-1；

  return 0;
}
~~~



### 使用拉链法

~~~C++
#include<iostream>
using namespace std;
const int N=10003;

typedef struct ArcNode  //?????
{
    int adjvex;//结点值
    ArcNode *next;//链表
}ArcNode;

typedef struct VNode
{
  int val;
  ArcNode *first;//h[]

}vexlist[N];
typedef struct graph
{
  vexlist vextices;//顶点set
  int numvex,numedge;//no-usage
}graph;
//下面的只是别名  上面的是它本名！！！
void add(int x,graph *g)
{
  int hash=(x%N+N)%N;
  ArcNode *newNode=new ArcNode();
  newNode->adjvex=x;
  newNode->next=g->vextices[hash].first;
  g->vextices[hash].first=newNode;


}
int find_is_exist(int x,graph *g)
{
  int hash=(x%N+N)%N;
  for(ArcNode *i=g->vextices[hash].first;i!=nullptr;i=i->next)
  {
      if(i->adjvex==x)
        return 1；
  }
  return 0;
}
--------------------------------
void init(graph *g)
{
  for(int i=0;i<N;i++) 
    g->vextices[i].first=nullptr;
}
--------------------------------// -->初始化很重要<--
int main()
{
  graph p;
  init(&p);
  int n;
  cin>>n;
  while(n--)
  {
    int x;
    cin>>x;
    add(x,&p);
  }
  int q;
  cin>>q;
  while(q--)
  {
    int x;
    cin>>x;
    cout<<find_is_exist(x,&p)<<endl;
  }
  return 0;
}
~~~





## 2.直接定址法

![image-20241016203346967](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016203346967.png)

## 3. 平方取中法

![image-20241016203400792](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016203400792.png)

## 4.数字分析法

## ![image-20241016203427159](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016203427159.png)



**key：就是尽可能的减小冲突，也有可能完全避免冲突的（具体问题具体分析！！！**



![image-20241016203421863](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016203421863.png)

# 二、开放寻址法

<font size=8>==**! 注意：  m 表示散列表表长度**==</font>



## 1.线性探测法（最重要！！）

![image-20241016203813404](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016203813404.png)

![image-20241016203817042](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016203817042.png)

### 查找

![image-20241016203854808](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016203854808.png)

缺点：没有区别度的查找！

#### 查找失败



**注意空位置也是要找的！**



![image-20241016203949619](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016203949619.png)

**当遇到空位置判断为空就停止**

**但是！** 

**这样就引出的一个问题！**

### 删除の问题

![image-20241016204115894](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016204115894.png)

**标记“逻辑删除”！**

![image-20241016204144636](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016204144636.png)

### 查找效率分析（ASL）

![image-20241016204210097](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016204210097.png)

### 缺点

![img](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/%7B2FE42FCB-10B0-4D5A-8718-B194A7B0CCEC%7D)

![image-20241016204343928](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016204343928.png)

**导致遇到逻辑删除的位置还是要一直查询！**

## 2.平方探测法

**一开始都由于mod13余6造成冲突！** 

![image-20241016210602587](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016210602587.png)



---

![image-20241016210706302](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016210706302.png)

> 要想查找到所有位置是有要求的！！

## 3.伪随机探测法

![image-20241016210815543](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016210815543.png)

![image-20241016210823874](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016210823874.png)

## 4.再散列法（准备多个散列表）

![image-20241016210835076](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241016210835076.png)

# 十六、排序

![image-20240926191434980](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240926191434980.png)

> 对于递归 画树更好理解！
>
> 稳定 插帽龟 and  *统计鸡

## 算法的稳定性

![image-20240927221330046](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240927221330046.png)



## 1.归并排序

~~~c++
#include<iostream>
using namespace std;
const int N=1e5+10;
int a[N];
int res[N];
void merge(int q[],int l,int r)
{
    if(l==r)//只有一个点到时候返回
    return ;
    int mid=l+r>>1;
    merge(q,l,mid);
    merge(q,mid+1,r);
    
    int i=l,j=mid+1;
    int k=0;
    while(i<=mid&&j<=r)
    {
        if(q[i]<q[j]) res[k++]=q[i++];
        else res[k++]=q[j++];
        
    }
    while(i<=mid)res[k++]=q[i++];
    while(j<=r)res[k++]=q[j++];
    //!!!
    for(int i=l,j=0;i<=r;i++,j++)
    {
        q[i]=res[j];
    }
    
    
}
int main()
{
    int n;
    cin>>n;
    for(int i=0;i<n;i++)cin>>a[i];
    merge(a,0,n-1);
    for(int i=0;i<n;i++)cout<<a[i]<<' ';
    
    return 0;
}
~~~

## 2.快速排序

~~~C++
#include<iostream>
using namespace std;
const int N=1e5+10;
int a[N];
void quick(int a[],int l ,int r)
{
    if(l==r)
    return ;
    
    int x=a[l+r>>1];
    int i=l-1,j=r+1;
    while(i<j)
    {
        //注意这个while 不能就一个 不然会嵌入下行的 除非while下面跟着语句
        
        while(a[++i]<x);
        while(a[--j]>x);//不能等
        //!
        if(i<j)swap(a[i],a[j]);
    }
    quick(a,l,j);//不能mid 相遇在i/j 而不一定是mid
    quick(a,j+1,r);
}
int main()
{
    int n;
    cin>>n;
    for(int i=0;i<n;i++)cin>>a[i];
    quick(a,0,n-1);
    for(int i=0;i<n;i++)cout<<a[i]<<' ';
    return 0;
}
~~~



## 3.选择排序

~~~c++
#include<iostream>
using namespace std;
const int N=1e5+10;
int a[N];
int main()
{
    int n;
    cin>>n;
    for(int i=0;i<n;i++)cin>>a[i];
    int min;
    for(int i=0;i<n-1;i++)
        for(int j=i+1;j<n;j++)
        {
            if(a[j]<a[i])swap(a[i],a[j]);
        }
        
    
    for(int i=0;i<n;i++)cout<<a[i]<<" ";
    
    return 0;
}
~~~

### 性能分析

![image-20240927221540776](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240927221540776.png)

## 4.冒泡排序

~~~C++
#include<iostream>
using namespace std;
int main()
{
    int n;
    cin>>n;
    int a[10];
    for(int i=0;i<n;i++)cin>>a[i];
        
    for(int i=0;i<n-1;i++)
    {
        //每一趟都设置为0
        bool flag=0;//如果有交换就设为true
        for(int j=n-1;j>i;j--)
        {
            if(a[j]<a[j-1])
            {
                flag=1;
                swap(a[j],a[j-1]);
            }
        }
        if(flag==0)
        break;
    }
    
    for(int i=0;i<n;i++)cout<<a[i]<<" ";
    
    return 0;
}
~~~



## 5.堆排序

~~~c++
#include<iostream>
using namespace std;
const int N=1e5+10;
//需要什么
int h[N];
int Size;
int n,m;
void up(int u)
{
    while(u/2>0&&h[u]<h[u/2])//指涉不为空
    {
        swap(h[u],h[u/2]);
        u/=2;//步进
    }
}
void down(int u)
{
    int t=u;//当前结点cur
    
    //比较三个值
    if(u*2<=Size&&h[u*2]<h[t])t=u*2;
    if(u*2+1<=Size&&h[u*2+1]<h[t])t=u*2+1;
    
    if(t!=u)
    {
        swap(h[t],h[u]);
        down(t);//直到down到满足条件
    }
}

int main()
{
    cin>>n>>m; 
    Size=n;
    for(int i=1;i<=n;i++)cin>>h[i];//传入时都是离散的每一个点
    //!
    for(int i=n/2;i;i--)down(i);//从最后一个父节点开始建堆
   
    
    while(m--)
    {
        cout<<h[1]<<" ";
        h[1]=h[Size--];//覆盖
        down(1);
        
    }
    
    return 0;
}
~~~



## 6.基数排序



## 7.直插排序 (移位赋值操作)

~~~C++
#include<iostream>
using namespace std;
const int N=1010;
int a[N];
int main()
{
    int n;
    cin>>n;
    //a[0] 哨兵结点
    for(int i=1;i<=n;i++)cin>>a[i];
    if(n==1)
    {
        cout<<a[1];
        return 0;
    }
    int j;
    for(int i=2;i<=n;i++)//每次在遍历时都保证了前面是有序的了
    {
        if(a[i]<a[i-1])
        {
            a[0]=a[i];//复制当前元素到哨兵结点
            //判断条件不需要j>0 因为a[0]本身，到本身一定会停下来
            for(j=i-1;a[0]<a[j];j--) a[j+1]=a[j];//右移空间,因为会覆盖所以要用哨兵存起来
            
            //直到满足条件j就会停下来
            a[j+1]=a[0];
        }
    }
    for(int i=1;i<=n;i++)cout<<a[i]<<" ";
    return 0;
}
~~~

### 二分优化（a bit）

~~~C++
#include<iostream>
using namespace std;
const int N=1010;
int a[N];
int main()
{
    int n;
    cin>>n;
    
    for(int i=1;i<=n;i++)cin>>a[i];
    if(n==1)
    {
        cout<<a[1];
        return 0;
    }
    int j;
    int l,r;
    for(int i=2;i<=n;i++)//每次在遍历时都保证了前面是有序的了
    {
       if(a[i]<a[i-1])//一旦发现不满足的就二分查找能插入的位置
       {
           a[0]=a[i];
         l=1,r=i-1;
           while(l<r)
           {
               int mid=l+r>>1;
               if(a[mid]>a[0])//二分逻辑注意
                r=mid-1;
               else 
               l=mid+1;
           }//如果找不到
          if(a[l]>a[0])//也就是都比之前小的话
            l=0;
            
            //统一后移让出位置
              for(j=i-1;j>=l+1;j--)
              a[j+1]=a[j];
               
              a[j+1]=a[0];
           
       }
  
     
      
       
    }
    for(int i=1;i<=n;i++)cout<<a[i]<<" ";
    return 0;
}
~~~



## 8.希尔（shell）排序

~~~C++
#include<iostream>
using namespace std;
const int N=1e5+10;
int a[N];
int main()
{
    int n;
    cin>>n;
    for(int i=1;i<=n;i++)cin>>a[i];
    int j;
    for(int d=n/2;d>=1;d/=2)
    {
        for(int i=d+1;i<=n;i++)
        {
            if(a[i]<a[i-d])//一旦发现子集中有一个大于a[0]
            {
                a[0]=a[i];//暂存这个值
                //插入排序步骤
                for(j=i-d;j>0&&a[j]>a[0];j-=d)//枚举这个子集
                a[j+d]=a[j];
                a[j+d]=a[0];
                
            }
        }
    }


    for(int i=1;i<=n;i++)cout<<a[i]<<' ';
    return 0;
}
~~~





