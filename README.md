# 数据结构与算法前言

## 什么是数据结构与算法？

数据结构就是在计算机中，存储和组织数据的方式。

例如：图书管理，要实现两个相关操作：

- 操作一：新书怎么插入？
- 操作二：怎么找到某本指定的书？

方法1：随便放

- 操作一：哪里有空放哪里，一步到位！
- 操作二：找某一本书，把人累死

方法2：按照书名和拼音字母顺序排放

- 操作一：新进一本《阿Q正传》按照字母顺序找到位置，插入
- 操作二：二分查找法

方法3：把书架划分成几块区域按照类别存放，类别中按照字母顺序

- 操作一：先定类别，二分查找确定位置，移除空位
- 操作二：先定类别，再二分查找

## 常见的数据结构

- **数组**（Array）
- **栈**（Stack）
- **链表**（Linked List）
- **图**（Graph）
- **散列表**（Hash）
- **队列**（Queue）
- **树**（Tree）
- **堆**（Heap）

> 注意:数据结构和语言无关,常见的编程语言都有直接或者间接的使用上述常见的数据结构

## 什么是算法？

算法（Algorithm）的定义

- 一个有限指令集，每条指令的描述不依赖于语言；
- 接收一些输入（有些情况下不需要输入）；
- 产生输入；
- 一定在有限步骤之后终止；

算法通俗理解：

- Algorithm这个单词本意就是解决问题的办法/步骤逻辑
- 数据结构的实现，离不开算法

# 栈结构(Stack)

**认识栈结构**

栈也是一种非常常见的数据结构，并且在程序中的应用非常广泛，栈的特点是**先进后出，后进先出**

**栈结构示意图**

![image-20221025210353987](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221025210353987.png)

**面试题目：**

有六个元素6,5,4,3,2,1 的顺序进栈，问下列哪一个不是合法的出栈序列？

- A：5 4 3 6 1 2
- B：4 5 3 2 1 6
- C：3 4 6 5 2 1
- D：2 3 4 1 5 6

> 注意：不是一次性全部进栈，而是进栈途中可以出栈，有进有出

解析：

- A答案：65进栈，5出栈，4进栈出栈，3进栈出栈，6出栈，21进栈，1出栈，2出栈
- B答案：654进栈，4出栈，5出栈，3进栈出栈，2进栈出栈，1进栈出栈，6出栈
- C答案：6543进栈，3出栈，4出栈，之后应该5出栈而不是6，错误；
- D答案：65432进栈，2出栈，3出栈，4出栈，1进栈出栈，5出栈，6出栈。

**栈常见的操作：**

- push（element）：添加一个新元素到栈顶位置；
- pop（）：移除栈顶的元素，同时返回被移除的元素；
- peek（）：返回栈顶的元素，不对栈做任何修改（该方法不会移除栈顶的元素，仅仅返回它）；
- isEmpty（）：如果栈里没有任何元素就返回true，否则返回false；
- size（）：返回栈里的元素个数。这个方法和数组的length属性类似；
- toString（）：将栈结构的内容以字符串的形式返回。

**栈结构的代码实现**

```js
class Stack {
    constructor() {
        // 栈中的属性
        this.items = []
    }
    // 栈的相关操作
    push(el) {
        //添加一个新元素到栈顶位置
        this.items.push(el)
    }
    pop() {
        // 移除栈顶的元素，同时返回被移除的元素
        return this.items.pop()
    }
    peek() {
        // 仅返回栈顶的元素
        return this.items[this.items.length - 1] 
    }
    isEmpty() {
        // 如果栈里没有任何元素就返回true，否则返回false
        return this.isEmpty.length === 0
    }
    size() {
        // 返回栈里的元素个数
        return this.items.length
    }
    toString() {
        // 将栈结构的内容以字符串的形式返回 
        // 20 10 8 7 6 5 4 1
        let res = ''
        for (let i = 0; i < this.items.length; i++) {
            res += this.items[i] + ' '
        }
        return res
    }
}
const stack = new Stack()
stack.push(10)
stack.push(5)
stack.push(3)
stack.push(1)
console.log(stack.items);
```

![image-20221025214415917](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221025214415917.png)

**栈的练习：**

将十进制转换成二进制

```js
// 函数：十进制转二进制
function dec2bin(decNumber) {
    // 1.定义一个栈对象
    const stack = new Stack()

    // 2.循环操作
    while (decNumber > 0) {
        // 2.1.获取余数
        stack.push(decNumber % 2)
        // 2.2获取整除后的结果，作为下一次使用
        decNumber = Math.floor(decNumber / 2)
    }
    // 3.从栈中取出0和1
    stack.items.reverse()
    return stack.toString()
}
console.log(dec2bin(100)) // 1 1 0 0 1 0 0 
```

# 队列结构(Queue)

队列也是一种受限的线性表，他的特点是**先进先出**

- 受限之处在于他只允许在表的**前端**（front）进行删除操作
- 而在表的**后端**（rear）进行插入操作

![image-20221026101345775](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221026101345775.png)

**队列的常见操作：**

- enqueue（element）：向队列尾部添加一个新的项；
- dequeue（）：移除队列的第一（即排在队列最前面的）项，并返回被移除的元素；
- front（）：返回队列中的第一个元素——最先被添加，也将是最先被移除的元素。队列不做任何变动（不移除元素，只返回元素信息与Stack类的peek方法非常类似）；
- isEmpty（）：如果队列中不包含任何元素，返回true，否则返回false；
- size（）：返回队列包含的元素个数，与数组的length属性类似；
- toString（）：将队列中的内容，转成字符串形式；

## **代码封装实现**

```js
// 封装队列类
class Queue {
    constructor() {
        // 属性
        this.items = []
    }
    // 相关操作
    enqueue(el) {
        // 向队列尾部添加一个新的项
        this.items.push(el)
    }
    dequeue() {
        // 移除队列的第一 并返回被移除的元素
        return this.items.shift()
    }
    front() {
        // 返回队列中最先被添加的元素,队列不做任何变动
        return this.items[0]
    }
    isEmpty() {
        // 如果队列中不包含任何元素，返回true，否则返回false
        return this.items.length === 0
    }
    size() {
        // 返回队列包含的元素个数
        return this.items.length
    }
    toString() {
        // 将队列中的内容，转成字符串形式
        let res = ''
        for (let i = 0; i < this.items.length; i++) {
            res += this.items[i] + ''
        }
        return res
    }
}
const queue = new Queue()
queue.enqueue('a')
queue.enqueue('b')
queue.enqueue('c')
console.log(queue);
```



![image-20221026103148041](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221026103148041.png)

## 队列应用

击鼓传花是一个常见的面试算法题，使用队列可以非常方便的实现最终的结果

游戏规则（修改过）：

- 几个朋友一起玩一个游戏，围成一圈，开始数数，数到某个数字的人自动淘汰
- 最后剩下的这个人会获得胜利，请问最后剩下的是原来在哪一个位置的人？

封装一个基于队列的函数：

- 参数：所有参与人的姓名，基于的数字
- 结果：最终剩下的那个人的姓名

**代码实现**

```js
// 面试题：击鼓传花
function passGame(nameList, num) {
    // 1.创建队列结构
    const queue = new Queue()
    // 2.将所有人依次加入到队列中
    for (let i = 0; i < nameList.length; i++) {
        queue.enqueue(nameList[i])
    }
    // 3.开始数数字
    while (queue.size() > 1) {
        // 不是num的时候，重新加入到队列的末尾
        // 是num的时候，从队列中删除
        // num数字之前的人重新放到队列末尾
        for (let i = 0; i < num - 1; i++) {
            queue.enqueue(queue.dequeue())
        }
        // num对应的人直接删除掉
        queue.dequeue()
    }
    // 4.获取剩下的人
    return queue.front()
}
console.log(passGame([1,2,3,4,5], 2)); // 3
```

## 优先级队列

优先级队列主要考虑的问题为：

- 每个元素不再只是一个数据，还包含数据的优先级
- 在添加数据过程中，根据优先级放入到正确位置

**优先级队列封装：**

```js
class QueueElement {
    constructor(element, priority) {
        this.element = element
        this.priority = priority
    }
}

class PriorityQueue {
    constructor() {
        // 属性
        this.items = []
    }
    enqueue(element, priority) {
        // 1.创建QueueElement对象
        let queueElement = new QueueElement(element, priority)

        // 判断队列是否为空
        if (!this.items.length) {
            this.items.push(queueElement)
        } else {
            // 判断优先级是不是最小的，如果是最小的，那么就没必要去比较了
            if (queueElement.priority >= this.items[this.items.length - 1].priority) {
                this.items.push(queueElement)
                return
            }
            // 比较优先级，插入
            for (let i = 0; i < this.items.length; i++) {
                if (queueElement.priority < this.items[i].priority) {
                    this.items.splice(i, 0, queueElement)
                    break
                }
            }
        }
    }
    // 删除优先级最高的并返回
    dequeue() {
        return this.items.shift()
    }
    // 返回优先级最高的
    front() {
        return this.items[0]
    }
    // 队列是否为空
    isEmpty() {
        return this.items.length === 0
    }
    // 队列长度
    size() {
        return this.items.length
    }
    // 返回队列的字符串形态
    toString() {
        let res = ''
        for (let i = 0; i < this.items.length; i++) {
            res += this.items[i].element + ' '
        }
        return res
    }
}

const qp = new PriorityQueue()

// enqueue
qp.enqueue('star', 10)
qp.enqueue('tom', 11)
qp.enqueue('jack', 2)
qp.enqueue('gg', 22)
console.log(qp);
```

![image-20221026141145143](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221026141145143.png)
