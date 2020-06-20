# 一

**1.** 顺序表的删除

编程实现把顺序表中从i个元素开始的k个元素删除（数据类型为整型）。

输入格式：第一行输入元素个数n，第二行输入n个数，空格分隔，第三行输入i和k；

输出格式：如果成功删除，则第一行输出Success!第二行输出删除后还剩下的顺序表中的元素；如果删除不成功，第一行输出Failure!第二行输出原顺序表元素。

输入样例：

8
1 4 6 8 9 2 11 15
3 4

输出：

Success!
1 4 11 15

代码:

```cpp
#include "iostream"

using namespace std;

int deletek(int lis[], int n, int i, int k) {
    if (i < 0 || k < 0 || i > n || i+k > n) {
        return 0;
    }
    for (int l = i - 1; l + k <= n; l++) {
        lis[l] = lis[l + k];
    }
    n -= k;
    return 1;
}

int main(int argc, char const *argv[]) {
    int n, i, k;
    cin >> n;
    int lis[n];
    for (int l = 0; l < n; l++) {
        cin >> lis[l];
    }
    cin >> i >> k;

    if (deletek(lis, n, i, k)) {
        cout << "Success!" << endl;
        for (int l = 0; l < n - k; l++) {
            cout << lis[l] << " ";
        }
        cout << endl;
    }else{
        cout << "Failure!" << endl;
        for (int l = 0; l < n; l++) {
            cout << lis[l] << " ";
        }
        cout << endl;
    }

    return 0;
}



```

**2.** 顺序表的插入

【问题描述】实现在顺序存储的有序表中插入一个元素（数据类型为整型）,使表仍然有序。

【输入形式】第一行输入原线性表元素个数，第二行输入有序表中的元素，元素间空格分开，第三行输入要插入的元素值 。

【输出形式】输出插入后的有序序列。
【样例输入】

7

3 5 6 8 11 30 66

22

【样例输出】

3 5 6 8 11 22 30 66

```c
#include "iostream"

using namespace std;

int main(int argc, char const *argv[]) {
    int n, ele;
    cin >> n;
    int lis[n+1];
    for (int l = 0; l < n; l++) {
        cin >> lis[l];
    }
    cin >> ele;

    for (int i = n-1; i >= -1; i--) {
        if (lis[i] > ele) {
            lis[i + 1] = lis[i];
        } else {
            lis[i + 1] = ele;
            break;
        }
    }

    for (int i = 0; i < n+1; i++) {
        cout << lis[i] << " ";
    }

    return 0;
}
```

**3.** 将0元素前移

【问题描述】已知具有n个数组元素的一维数组A,请写一个算法，将该数组中所有值为0的元素都依次移到数组的前端，其他元素依次输出。
【输入形式】第一个数为输入数字的个数，其后为数组的数字
【输出形式】输出相应的数组
【样例输入】5 1 2 3 4 0
【样例输出】0 1 2 3 4

# 二

**1.** 创建链表

【问题描述】提交与自己学号相邻的两位同学的学号与一门考试成绩，编程建立由这三组数据结点组成的简单链表。
【输入形式】三组同学的学号后三位，成绩
【输出形式】链表各节点的数据
【样例输入】201，98  202，94 203，89
【样例输出】】[num=201,score=98]

​            [num=202,score=94]

​            [num=203,score=89]
【样例说明】输入三组数据，创建一个单链表

```c
#include <iostream>

using namespace std;

typedef struct node {
    int num;
    int score;
    struct node *next;
} node;

int main(int argc, char const *argv[]) {
    node *p1 = (node *)malloc(sizeof(node));
    node *p2 = (node *)malloc(sizeof(node));
    node *p3 = (node *)malloc(sizeof(node));

    //201，98  202，94  203，89
    scanf("%d,%d", &p1->num, &p1->score);
    scanf("%d,%d", &p2->num, &p2->score);
    scanf("%d,%d", &p3->num, &p3->score);

    p1->next = p3;
    p2->next = p2;
    p3->next = NULL;

    cout <<"[num="<<p1->num<<",score="<<p1->score<<"]\n";
    cout <<"[num="<<p2->num<<",score="<<p2->score<<"]\n";
    cout <<"[num="<<p3->num<<",score="<<p3->score<<"]\n";

    return 0;
}
```

**2.** 线性链表的结点移动

【问题描述】
已知非空线性链表第1个链结点指针为list，链结点构造为
struct node{
  datatype data;
  node *link;
};
请写一算法，将该链表中数据域值最大的那个点移到链表的最后面。（假设链表中数据域值最大的链结点惟一）（注意：要求先写出算法的解题思路，然后再写出算法）
【输入形式】
输入为一个整数序列，整数之间以空格隔开，序列以回车结尾。
【输出形式】
输出为移动后的整数序列，整数之间以空格隔开，序列以回车结尾。
【样例输入】
3 12 4 9 5 1
【样例输出】
3 4 9 5 1 12
【样例说明】
将序列中最大的数字12移动到序列最后。
【评分标准】
本题必须采用链表来实现移动操作，其他方法不得分。

```c
#include <stdio.h>
#include <stdlib.h>
typedef int datatype;
typedef struct node {
    datatype data;
    struct node *next;
} node;

int main(int argc, char const *argv[]) {
    node *pHead = (node *)malloc(sizeof(node));
    node *curr = pHead;
    node *last;
    while (1) {
        scanf("%d", &curr->data);
        char c = getchar();
        if (c == '\n') break;
        node *p = (node *)malloc(sizeof(node));
        curr->next = p;
        p->next = NULL;
        curr = p;
    }

    last = curr;

    curr = pHead;
    node *maxNode = pHead;
    while (curr != NULL) {  //找到最大节点
        if (maxNode->data < curr->data) maxNode = curr;
        curr = curr->next;
    }

    node *maxPrev = pHead;
    if (maxPrev != maxNode) {
        while (maxPrev->next != maxNode) {  //找到最大的节点的前驱节点
            maxPrev = maxPrev->next;
        }
        if (maxNode->next != NULL) {
            maxPrev->next = maxNode->next;
            maxNode->next = NULL;
            last->next = maxNode;
        }
        curr = pHead;
    } else {
        pHead = pHead->next;
        last->next = maxNode;
        maxNode->next = NULL;

        curr = pHead;
    }
    curr = pHead;
    while (curr != NULL) {
        printf("%d ", curr->data);
        curr = curr->next;
    }
    printf("\n");
}


```

**3.** 输出单链表倒数第K个结点值

【问题描述】输入一个单向链表，输出该链表中倒数第k个结点，链表的最后一个结点是倒数第1个节点。


【输入形式】输入第一位为K值，其后接一串以空格分隔的整型值。
【输出形式】输出为倒数第K个结点的值，若无，则输出Not Found

【样例输入】3 13 45 54 32 1 4 98 2
【样例输出】4
【样例说明】K值为3，则输出链表倒数第3个结点的值，为4；数据输入间以空格隔开
【评分标准】本题要综合输出正确性及使用的数据结构。需由输入数据构建单链表。不使用链表的将不得分。

```c
#include <iostream>
#include <stdlib.h>
typedef int datatype;
typedef struct node {
    datatype data;
    struct node *next;
} node;

using namespace std;

int main(int argc, char const *argv[]) {
    node *pHead = (node *)malloc(sizeof(node));
    pHead->next = NULL;
    node *curr = pHead;
    int k;
    char c;
    
    cin >> k;
    
    while (1) {
    	node *p = (node *)malloc(sizeof(node));
       	scanf("%d",&p->data);
       	p->next = pHead->next;
       	pHead->next = p;
       	c = getchar();
       	if(c==EOF) break;
    }
	
	curr = pHead->next;
	int count = 1;
	while(1){
		if(k == count){
			printf("%d",curr->data);
			break;
		}
		if(curr->next == NULL){
			printf("Not Found");
			break;
		}
		curr = curr->next;
		count++;
	}
}
```

# 三

**1.** 十进制整数转换为八进制数

【问题描述】对于输入的任意一个非负十进制整数，打印输出与其等值的八进制数
【输入形式】非负十进制整数
【输出形式】相应十进制整数转换后的八进制正整数，若输入不符合要求，提示错误，重新输入
【样例输入】5548
【样例输出】12654
【样例说明】先判断输入是否符合非负正整数要求
【评分标准】

```
#include <iostream>
#include <stack>
using namespace std;

int main(int argc, char const* argv[]) {
    int num;
    stack<int> st;

    cin >> num;
    if (num == 0) {
        cout << 0 << '\n';
    } else {
        while (num) {
            st.push(num % 8);
            num = num / 8;
        }
        while (!st.empty()) {
            cout << st.top();
            st.pop();
        }
    }
    cout<<endl;
    // cout<<oct<<num<<endl;

    return 0;
}
```

**2.** 圆括号是否正确配对

【问题描述】



设计一个算法判别一个算术表达式的圆括号是否正确配对

【输入形式】

一个任意字符串表达式

【输出形式】

若配对，则输出圆括号的对数；否则输出no



【样例输入】(a+b)/(c+d)@

【样例输出】 2

【样例说明】共有两对括号，输出2

【评分标准】

```
#include <iostream>
#include <stack>
using namespace std;

int countBrackets(char *str);

int main(int argc, char const *argv[]) {
    char ch[2048];
    gets(ch);
    int result = countBrackets(ch);
    if(result!=0){
        cout<<result<<endl;
    }else{
        cout<<"no"<<endl;
    }

    return 0;
}

int countBrackets(char *str) {
    int ret = 0;
    stack<char> st;
    char *ch = str;
    while (*ch != '@') {
        switch (*ch) {
            case '(':
                st.push('(');
                break;
            case ')':
                if (st.top() == '(') {
                    st.pop();
                    ret++;
                } else {
                    st.push(')');
                }
                break;
            case '[':
                st.push('[');
                break;
            case ']':
                if (st.top() == '[') {
                    st.pop();
                    ret++;
                } else {
                    st.push(']');
                }
                break;
            case '{':
                st.push('{');
                break;
            case '}':
                if (st.top() == '{') {
                    st.pop();
                    ret++;
                } else {
                    st.push('}');
                }
                break;
            default:
                break;
        }
        ch++;
    }

    return st.empty()&&ret!=0?ret : 0;
}
```

# 四

**1.** 队列元素逆置

【问题描述】

已知Q是一个非空队列，S是一个空栈。仅使用少量工作变量以及对队列和栈的基本操作，编写一个算法，将队列Q中的所有元素逆置。


【输入形式】

输入的第一行为队列元素个数，第二行为队列从首至尾的元素


【输出形式】

输出队列的逆置


【样例输入】

3

1 2 3


【样例输出】

3 2 1

```cpp
#include <iostream>
#include <queue>
#include <stack>

using namespace std;
int main(int argc, char const *argv[]) {
    int length, data;
    queue<int> que;
    stack<int> sta;
    cin >> length;
    for (size_t i = 0; i < length; i++) {
        cin >> data;
        que.push(data);
    }

    while (!que.empty()) {
        sta.push(que.front());
        que.pop();
    }

    while (!sta.empty()) {
        cout<< sta.top() << " ";
        sta.pop();
    }

    return 0;
}
```

**2.** 判断一个数列是否是栈的输出序列

【问题描述】给出一个堆栈的输入序列，试判断一个序列是否能够由这个堆栈输出。如果能，返回总的**出栈次数**，如果不能，返回0。序列的输入及输出都是从左往右。（输入输出序列皆为整数且没有重复的数字，如果一个数字在输入序列中没有出现，那么其在输出序列中也不会出现）
【输入形式】第一行为输入序列的长度，然后为输入序列的数字；第二行为输出序列的数字。输入数据以空格隔开。
【输出形式】如果是一个出栈序列，则返回总的**出栈次数**， 否则返回0
【样例输入】

5 1 2 3 4 5

1 2 3 4 5


【样例输出】5
【样例说明】第一行输入的第一个数字是序列的长度，1 2 3 4 5 输入序列，以空格隔开，输出的总的出栈次数。

```
#include <stdio.h>
#include <stdlib.h>

#define DataType int
#define MAXSIZE 1024

typedef struct {
    DataType data[MAXSIZE];
    int top;
} SeqStack;

SeqStack* Init_SeqStack() {  //栈初始化
    SeqStack* s;
    s = (SeqStack*)malloc(sizeof(SeqStack));
    if (!s) {
        printf("空间不足\n");
        return NULL;
    } else {
        s->top = -1;
        return s;
    }
}

int Empty_SeqStack(SeqStack* s) {  //判栈空
    if (s->top == -1)
        return 1;
    else
        return 0;
}

int Push_SeqStack(SeqStack* s, DataType x) {  //入栈
    if (s->top == MAXSIZE - 1)
        return 0;  //栈满不能入栈
    else {
        s->top++;
        s->data[s->top] = x;
        return 1;
    }
}

int Pop_SeqStack(SeqStack* s) {  //出栈
    if (Empty_SeqStack(s))
        return 0;  //栈空不能出栈
    else {
        s->top--;
        return 1;
    }
}

DataType Top_SeqStack(SeqStack* s) {  //取栈顶元素
    if (Empty_SeqStack(s))
        return 0;  //栈空
    else
        return s->data[s->top];
}

int Print_SeqStack(SeqStack* s) {
    int i;
    for (i = s->top; i >= 0; i--) printf("%3d", s->data[i]);
    printf("\n");
    return 0;
}
/**
 * SeqStack* Init_SeqStack()
 * int Empty_SeqStack(SeqStack* s)
 * int Push_SeqStack(SeqStack* s, DataType x)
 * int Pop_SeqStack(SeqStack* s, DataType* x)
 * DataType Top_SeqStack(SeqStack* s)
 * **/
int main() {
    SeqStack* S;
    S = Init_SeqStack();
    int length;
    scanf("%d", &length);

    DataType queueA[length], cursorA = 0;
    DataType queueB[length], cursorB = 0;

    for (cursorB = 0; cursorB < length; cursorB++) {
        DataType temp;
        scanf("%d", &queueB[cursorB]);
    }

    for (cursorA = 0; cursorA < length; cursorA++) {
        DataType temp;
        scanf("%d", &queueA[cursorA]);
    }

    cursorA = 0;
    cursorB = 0;

    for (size_t i = 0; i < length; i++) {
        Push_SeqStack(S, queueB[cursorB]);
        cursorB++;
        while (!Empty_SeqStack(S) && Top_SeqStack(S) == queueA[cursorA]) {
            Pop_SeqStack(S);
            cursorA++;
        }
    }

    if(Empty_SeqStack(S)){
        printf("%d",length);
    }else{
        printf("%d",0);
    }

    return 0;
}

```
