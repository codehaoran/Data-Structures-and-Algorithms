# 目录

- [数据结构与算法前言](#数据结构与算法前言)
- [栈结构(Stack)](#栈结构(Stack))
- [队列结构(Queue)](#队列结构(Queue))
- [单向链表](#单向链表)
- [双向链表](#双向链表)
- [集合结构](#集合结构)
- [字典](#字典)



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

## 栈结构的代码实现

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

## 栈的练习：

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

## 代码封装实现

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

# 单向链表

## 链表的简介

链表和数组一样，可以用于**存储一系列的元素**，但是链表和数组的**实现机制完全不同**。链表的每个元素由一个存储**元素本身的节点**和一个**指向下一个元素的引用**（有的语言称为指针或连接）组成。类似于火车头，火车头会连接一个节点，车厢（节点）载着乘客（数据），通过节点连接另一节车厢。



![image-20221026145648527](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221026145648527.png)

**链表的优势：**

- 链表中的元素在内存中**不必是连续的空间**，可以充分利用计算机的内存，实现灵活的**内存动态管理**
- 链表不必在创建时就**确定大小**，并且大小可以**无限地延伸**下去
- 链表在**插入和删除**数据时，**时间复杂度**可以达到O(1)，相对数组效率高很多

**链表的缺点：**

- 链表访问任何一个位置的元素时，都需要**从头开始访问**（无法跳过第一个元素访问任何一个元素）
- 无法通过下标值直接访问元素，需要从头开始一个个访问，直到找到对应的元素
- 虽然可以轻松地到达**下一个节点**，但是回到**前一个节点**是很难的

## **链表中的常见操作：**

- append（data）：向链表尾部添加一个新的项
- insert（position，data）：向链表的特定位置插入一个新的项，返回值为Boolean
- get（position）：获取对应位置的元素
- indexOf（data）：返回元素在链表中的索引。如果链表中没有该元素就返回-1
- update（position，data）：修改某个位置的元素，返回值为Boolean
- removeAt（position）：从链表的特定位置移除一项，返回值为被移除的数据
- remove（data）：从链表中移除一项，返回值为Boolean
- isEmpty（）：如果链表中不包含任何元素，返回trun，如果链表长度大于0则返回false
- size（）：返回链表包含的元素个数，与数组的length属性类似
- toString（）：由于链表项使用了Node类，就需要重写继承自JavaScript对象默认的toString方法，让其只输出元素的值

## 封装单向链表

### 封装类

```js
// 节点类
class Node {
    constructor(data) {
        // 数据
        this.data = data
        // 指向下一个节点
        this.next = null
    }
}
// 封装链表类
class LinkedList {
    constructor() {
        // 链表的头
        this.head = null
        // 记录链表的长度
        this.length = 0
    }
}
```

### 1.append(data)

向链表尾部追加数据可能有两种情况：

- 链表本身为空，添加的数据是唯一节点，需要把head指向节点

- 链表不为空，需要在链表最后面追加节点，并让链表最后一个节点指向此节点

  **代码实现**

```js
append(data) {
    // 1.创建新的节点
    let newNode = new Node(data)
    // 2.判断添加的是否是第一个节点
    if (!this.length) {

        this.head = newNode
    } else {
        // 2.2不是第一个节点
        // 查出最后一个节点
        let current = this.head
        while (current.next) {
            current = current.next
        }
        // 在最后的节点的next上添加节点
        current.next = newNode
    }
    // 节点长度加一
    this.length += 1
}
```

**测试**

```js
// 测试
const list = new LinkedList()
list.append('tom-1')
list.append('jack-2')
list.append('city-3')
console.log(list);
```

![image-20221026161940743](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221026161940743.png)

### 2.insert（position，data）

![image-20221027103825934](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221027103825934.png)

**插入一条数据有三种可能发生情况**

1. **position大于链表长度或者为负数**
   - return false
2. **position = 0**
   - 插在head后面
   - ![image-20221027103836935](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221027103836935.png)
3. **position > 0**
   - previous和current分别指向需要插入位置前一个节点和要插入的节点
   - newNode的next指向current ，previous的next指向newNode
   - ![image-20221027103921335](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221027103921335.png)

```js
// 指定位置插入数据
insert(position, data) {
    // 1.对position进行越界判断
    if (position < 0 || position > this.length) return false

    // 2.根据data创建Node
    let newNode = new Node(data)

    // 3.插入newNode
    // 插入数据有两种情况
    // 第一种是position是0，插在head后
    if (position === 0) {
        newNode.next = this.head
        this.head = newNode
    } else {
        // 第二种情况是position>0
        let index = 0
        let current = this.head
        let preNode = null // 存放要插入位置的上一个
        while (current) {
            preNode = current
            current = current.next
            index++
            if (index === position) {
                newNode.next = current
                preNode.next = newNode
                break
            }
        }
    }
    // 4.length+1
    this.length += 1
    return true
}
```

**测试**

```js
// 测试
const list = new LinkedList()
list.append('tom-1')
list.append('jack-2')
list.append('city-3')
list.insert(2, 'test')
console.log(list);
```

![image-20221027140307277](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221027140307277.png)

### 3.get（position）

```js
// 获取对应位置的元素
get(position) {
    // 1.越界判断
    if(position < 0 || position > this.length - 1) return null
    // 2.根据position获取对应的数据
    let current = this.head
    let index = 0
    while (current) {
        if (index === position) {
            return current.data
        }
        current = current.next
        index++
    }
}
```

**测试**

```js
// 测试
const list = new LinkedList()
list.append('tom-1')
list.append('jack-2')
list.append('city-3')
console.log(list.get(1)); // 结果：jack-2
```

### 4.indexOf（data）

```js
// 返回数据在链表中的索引，如果没有，则返回-1
indexOf(data) {
    // 定义变量
    let index = 0
    let current = this.head
    // 开始查找
    while (current) {
        // 每次循环判断data是否相等
        if (data === current.data) {
            return index
        }
        // 不相等就current等于本身的next，准备下次循环使用
        current = current.next
        // 没循环一次 下标要+1
        index += 1
    }
    // 循环完毕，没有找到相等的data
    return -1
}
```

**测试**

```js
// 测试
const list = new LinkedList()
list.append('tom-1')
list.append('jack-2')
list.append('city-3')
list.indexOf('tom-1')
console.log(list.indexOf(1)); // 结果：-1
console.log(list.indexOf('tom-1')); // 结果： 0
console.log(list.indexOf('city-3')); // 结果： 2
```

### 5.update（position，data）

```js
// 修改某个位置的元素
update(position, newData) {
    // 1.越界判断
    if (position < 0 || position > this.length - 1) return false
    // 2.根据position坐标获取要修改的数据
    let current = this.head
    let index = 0
    while (current) {
        // 2.1坐标相同，修改数据
        if (index === position) {
            current.data = newData
            return true
        }
        // 2.2不相同，为下次循环做数据准备
        current = current.next
        index += 1
    }
}
```

**测试**

```js
// 测试
const list = new LinkedList()
list.append('tom-1')
list.append('jack-2')
list.append('city-3')
console.log(list);
```

![image-20221027145713088](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221027145713088.png)

### 6.removeAt（position）

```js
// 删除链表中指定位置的数据
removeAt(position) {
    // 1.越界判断
    if (position < 0 || position > this.length - 1) return null
    // 2.声明需要的变量
    let index = 0
    let current = this.head
    let preNode = null // 当前节点的上一个
    // 3.有两种情况，一种是position等于0,
    if (position === 0) {
        current = this.head
        this.head = this.head.next
    } else {
        // 第二种情况是position不等于0
        while (current) {
            // 坐标相同
            if (index === position) {
                // 上一个坐标的next等于当前坐标的next，即跳过了当前节点的data
                preNode.next = current.next
                break
            }
            // 记录当前节点的上一个
            preNode = current
            current = current.next
            index += 1
        }
    }
    // 4.链表长度更新
    this.length -= 1
    return current.data
}

```

**测试**

```js
// 测试
const list = new LinkedList()
list.append('tom-1')
list.append('jack-2')
list.append('city-3')
console.log(list);
```

![image-20221027153714807](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221027153714807.png)

### 7.remove（data）

```js
remove(data) {
    // 1.通过数据获取坐标，使用封装过的indexOf方法
    let index = this.indexOf(data)
    // 2.通过坐标删除链表中的数据，使用已经封装过的removeAt方法
    return !!this.removeAt(index) // !! 转换成布尔型
}
```

**测试**

```js
// 测试
const list = new LinkedList()
list.append('tom-1')
list.append('jack-2')
list.append('city-3')
console.log(list.remove('jack-2'));
```

![image-20221027155537253](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221027155537253.png)

### 8.sEmpty（）

```js
isEmpty() {
    return !!this.length
}
```

### 9.size（）

```js
size() {
    return this.length
}
```

### 10.toString（）

**实现流程：**

- 主要是获取每一个元素
- 从head开始，遍历每一个节点，取出其中的data，拼接成字符串
- 最终将字符串返回

​	**代码实现：**

```js
// 转换成字符串
toString() {
    // 1.定义变量
    let current = this.head
    let res = ''
    // 2.循环每一个节点
    while (current) {
        res += current.data + ' '
        current = current.next
    }
    return res
}
// 测试
const list = new LinkedList()
list.append('tom-1')
list.append('jack-2')
list.append('city-3')
console.log(list.toString()); // tom-1 jack-2 city-3 
```

### 整体代码

```js
// 节点类
class Node {
    constructor(data) {
        // 数据
        this.data = data
        // 指向下一个节点
        this.next = null
    }
}
// 封装链表类
class LinkedList {
    constructor() {
        // 链表的头
        this.head = null
        // 记录链表的长度
        this.length = 0
    }
    // 末尾添加一个节点
    append(data) {
        // 1.创建新的节点
        let newNode = new Node(data)
        // 2.判断添加的是否是第一个节点
        if (!this.length) {
            this.head = newNode
        } else {
            // 2.2不是第一个节点
            // 查出最后一个节点
            let current = this.head
            while (current.next) {
                current = current.next
            }
            // 在最后的节点的next上添加节点
            current.next = newNode
        }
        // 节点长度加一
        this.length += 1
    }
    // 转换成字符串
    toString() {
        // 1.定义变量
        let current = this.head
        let res = ''
        // 2.循环每一个节点
        while (current) {
            res += current.data + ' '
            current = current.next
        }
        return res
    }
    // 指定位置插入数据
    inster(position, data) {
        // 1.对position进行越界判断
        if (position < 0 || position > this.length) return false

        // 2.根据data创建Node
        let newNode = new Node(data)

        // 3.插入newNode
        // 插入数据有两种情况
        // 第一种是position是0，插在head后
        if (position === 0) {
            newNode.next = this.head
            this.head = newNode
        } else {
            // 第二种情况是position>0
            let index = 0
            let current = this.head
            let preNode = null // 存放要插入位置的上一个
            while (current) {
                preNode = current
                current = current.next
                index++
                if (index === position) {
                    newNode.next = current
                    preNode.next = newNode
                    break
                }
            }
        }
        // 4.length+1
        this.length += 1
        return true
    }
    // 获取对应位置的元素
    get(position) {
        // 1.越界判断
        if (position < 0 || position > this.length - 1) return null
        // 2.根据position获取对应的数据
        let current = this.head
        let index = 0
        while (current) {
            if (index === position) {
                return current.data
            }
            current = current.next
            index++
        }
    }
    // 返回数据在链表中的索引，如果没有，则返回-1
    indexOf(data) {
        // 定义变量
        let index = 0
        let current = this.head
        // 开始查找
        while (current) {
            // 每次循环判断data是否相等
            if (data === current.data) {
                return index
            }
            // 不相等就current等于本身的next，准备下次循环使用
            current = current.next
            // 没循环一次 下标要+1
            index += 1
        }
        // 循环完毕，没有找到相等的data
        return -1
    }
    // 修改某个位置的元素
    update(position, newData) {
        // 1.越界判断
        if (position < 0 || position > this.length - 1) return false
        // 2.根据position坐标获取要修改的数据
        let current = this.head
        let index = 0
        while (current) {
            // 2.1坐标相同，修改数据
            if (index === position) {
                current.data = newData
                return true
            }
            // 2.2不相同，为下次循环做数据准备
            current = current.next
            index += 1
        }
    }
    // 删除链表中指定位置的数据
    removeAt(position) {
        // 1.越界判断
        if (position < 0 || position > this.length - 1) return null
        // 2.声明需要的变量
        let index = 0
        let current = this.head
        let preNode = null // 当前节点的上一个
        // 3.有两种情况，一种是position等于0,
        if (position === 0) {
            current = this.head
            this.head = this.head.next
        } else {
            // 第二种情况是position不等于0
            while (current) {
                // 坐标相同
                if (index === position) {
                    // 上一个坐标的next等于当前坐标的next，即跳过了当前节点的data
                    preNode.next = current.next
                    break
                }
                // 记录当前节点的上一个
                preNode = current
                current = current.next
                index += 1
            }
        }
        // 4.链表长度更新
        this.length -= 1
        return current.data
    }

    // 从链表中移除指定值
    remove(data) {
        // 1.通过数据获取坐标，使用封装过的indexOf方法
        let index = this.indexOf(data)
        // 2.通过坐标删除链表中的数据，使用已经封装过的removeAt方法
        return !!this.removeAt(index)

    }
    // 判断链表有没有数据
    isEmpty() {
        return !!this.length
    }
    // 返回链表的长度
    size() {
        return this.length
    }
}
```

# 双向链表

## 双向链表简介

链表有多种不同的类型，本节介绍双向链表。双向链表和普通链表的区别在于，在链表中， 一个节点只有链向下一个节点的链接；而在双向链表中，链接是双向的：一个链向下一个元素， 另一个链向前一个元素

**双向链表的缺点：**

- 每次在**插入或删除**某个节点时，都需要处理四个引用，而不是两个，实现起来会困难些；
- 相对于单向链表，所占**内存空间更大**一些；
- 但是，相对于双向链表的便利性而言，这些缺点微不足道。

**双向链表的结构：**

![image-20221027193049052](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221027193049052.png)

![image-20221027193350257](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221027193350257.png)

- 双向链表不仅有**head**指针指向第一个节点，而且有**tail**指针指向最后一个节点；
- 每一个节点由三部分组成：**item**储存数据、**prev**指向前一个节点、**next**指向后一个节点；
- 双向链表的第一个节点的prev指向**null**；
- 双向链表的最后一个节点的next指向**null**；

## **双向链表常见的操作（方法）：**

- append（data）：向链表尾部添加一个新的项；
- inset（position，data）：向链表的特定位置插入一个新的项；
- get（position）：获取对应位置的元素；
- indexOf（data）：返回元素在链表中的索引，如果链表中没有元素就返回-1；
- update（position，data）：修改某个位置的元素；
- removeAt（position）：从链表的特定位置移除一项；
- remover(data)：从链表中移除指定数据
- isEmpty（）：如果链表中不包含任何元素，返回trun，如果链表长度大于0则返回false；
- size（）：返回链表包含的元素个数，与数组的length属性类似；

- toString（data）：输出链表中字符串的值，参数: 1：正向，-1：反向
- forwardString（）：返回正向遍历节点字符串形式；
- backwordString（）：返回反向遍历的节点的字符串形式；

## 封装双向链表

### 封装类

```js
// 节点类
class Node {
    constructor(data) {
        this.data = data
        this.prev = null
        this.next = null
    }
}
// 封装双向链表类
class DoubleLinkList {
    constructor() {
        // 属性
        this.head = null
        this.tail = null
        this.length = 0
    }
}
```

### 1.append(data)

**向尾部添加新节点分为两种情况：**

1. 链表中还没有节点(0节点)
   - 只需要将head和tail都指向新节点
2. 链表中已存在节点
   - 先将新节点的prev指向tail(最后一个节点)
   - 再将tail(最后一个节点)的next指向新节点
   - 最后将最后一个节点指向新节点
   - ![image-20221028144200320](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221028144200320.png)
   - ![](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221028144200320.png)

**代码实现**

```js
// 尾部添加一个节点
append(data) {
    // 1.创建节点
    const newNode = new Node(data)
    // 2.判断添加的是否是第一个节点
    if (!this.length) {
        // 是第一个节点
        this.head = newNode
        this.tail = newNode
    } else {
        // 先将新节点的prev指向tail(最后一个节点)
        newNode.prev = this.tail
        // 再将tail(最后一个节点)的next指向新节点
        this.tail.next = newNode
        // 将最后一个节点设置成新节点
        this.tail = newNode
    }
    // 3.长度+1
    this.length += 1
}
```

**测试代码**

```js
const dbList = new DoubleLinkList()
dbList.append('aaa')
dbList.append('bbb')
dbList.append('ccc')
console.log(dbList);
```

![image-20221028144554363](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221028144554363.png)

### 2.insert(position, data)

**插入一个新节点有多种情况：**

1. 插入的位置为0

   - 分两种情况，一是链表是空，只需要把 head 和 tail 都指向这个新节点

   - 二是链表不为空，把head.prev指向newNode，再将newNode设置为head，当前head.next指向记录的老head

     ![image-20221028165527826](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221028165527826.png)

2. 插入的位置是最后一个(position === length)

   - 新节点的prev指向tail，tail.next指向新节点，再把tail重新指向新节点

     ![image-20221028165208013](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221028165208013.png)

3. 插入的位置大于0 且 小于 length

   - 循环找到要插入的位置
     1. current.prev.next = newNode，将newNode设置为当前节点的位置
     2. newNode.prev = current.prev ， 新节点的prev等于当前节点的prev
     3. current.prev = newNode，newNode.next = current，这是互相连接

**代码实现**

```js
// 指定位置插入一个节点
insert(position, data) {
    // 1.越界判断
    if (position < 0 || position > this.length) return false

    // 2.根据data创建新节点
    const newNode = new Node(data)

    // 3.找到位置并插入
    let current = this.head
    let index = 0
    let prevCurrent = null // 用来记录当前循环的节点的prev
    // 3.1如果插入的时候链表是一个空链表
    if (this.length === 0) {
        this.head = newNode
        this.tail = newNode
        // 3.2如果插入的位置是0
    } else if (position === 0) {
        // 将当前第一个节点的prev指向新节点
        current.prev = newNode
        // 将新节点设置成第一个节点
        this.head = newNode
        // 新节点的next指向记录下来的current
        this.head.next = current
        // 3.3如果插入的位置最后一个（链表的长度）
    } else if (position === this.length) {
        newNode.prev = this.tail
        this.tail.next = newNode
        this.tail = newNode
        // 3.4 插入的位置不是头也不是尾
    } else {
        while (current) {
            if (index === position) {
                current.prev.next = newNode
                newNode.prev = current.prev 
                current.prev = newNode
                newNode.next = current
                break
            }
            index += 1
            current = current.next
        }
    }
    // 4.长度 +1
    this.length += 1
    return newNode
}
```

**代码测试：**

```js
const dbList = new DoubleLinkList()
dbList.insert(0, 'aaa')
dbList.insert(0, 'root')
dbList.insert(2, 'bbb')
dbList.insert(1, 'root_son')
console.log(dbList);
```

![image-20221028170708962](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221028170708962.png)

### 3.get(data)

**代码实现**

```js
// 获取对应位置的元素
get(position) {
    if (position < 0 || position > this.length) return null
    let current = this.head
    let index = 0
    while (current) {
        if (index === position) {
            return current
        }
        index += 1
        current = current.next
    }
    return null
}
```

如果考虑到性能，当节点过多，从head开始循环貌似不是最优的办法，如果节点很多，我们要找的节点又靠后呢？那将浪费很多性能，解决办法就是判断position的位置距离head和tail哪个近，就从那边循环

- position < this.length / 2，从head开始遍历
- position > this.length / 2，从tail开始遍历

**优化后的代码：**

```js
// 获取对应位置的元素
get(position) {
    if (position < 0 || position > this.length) return null
    if (position < this.length / 2) {
        let index = 0
        let current = this.head
        while (current) {
            if (index === position) {
                return current
            }
            index += 1
            current = current.next
        }
    }else {
        let current = this.tail
        let index = this.length - 1
        while (current) {
            if (index === position) {
                return current
            }
            index -= 1
            current = current.prev
        }
    }
    return null
}
```

**测试代码**

```js
const dbList = new DoubleLinkList()
dbList.insert(0, 'aaa')
dbList.insert(0, 'root')
dbList.insert(2, 'bbb')
dbList.insert(1, 'root_son')
console.log(dbList);
console.log(dbList.get(3));
```

![image-20221029131115921](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221029131115921.png)

### 4.indexOf(data)

```js
// 返回元素在链表中的索引
indexOf(data) {
    let index = 0
    let current = this.head
    while (current) {
        if (current.data === data) {
            return index
        }
        current = current.next
        index += 1
    }
    return -1
}
```

### 5.update(position, data)

**实现代码**

```js
// 修改某个位置的元素
update(position, data) {
    // 越界判断
    if (position < 0 || position > this.length - 1) return false
    // 判断position位置距离head和tail哪个近
    if (position < this.length / 2) {
        let index = 0
        let current = this.head
        while (current) {
            if (index === position) {
                current.data = data
                return true
            }
            index += 1
            current = current.next
        }
    } else {
        let index = this.length - 1
        let current = this.tail
        while (current) {
            if (index === position) {
                current.data = data
                return true
            }
            index -= 1
            current = current.prev
        }
    }
}
```

**测试代码**

```js
const dbList = new DoubleLinkList()
dbList.insert(0, 'root')
dbList.insert(1, 'root_son')
dbList.insert(2, 'aaa')
dbList.insert(3, 'bbb')
console.log(dbList.update(0, 'root-update')); 
console.log(dbList.update(3, 'bbb-update')); 
console.log(dbList);
```

![image-20221029141437871](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221029141437871.png)

### 6.removeAt(position)

**删除一个节点有四种情况：**

1. 只有一个节点的时候，需要把head、tail指向null
2. 删除第一个节点，head指向this.head.next，再把新head的prev指向null
3. 删除最后一个节点，tail指向this.tail.prev，再把新tail的next指向null
4. 删除中间的节点，current.prev.next指向current.next，current.next.prev = current.prev。互相指向，跳过current

**实现代码**

```js
// 从链表的特定位置移除一项
removeAt(position) {
    // 越界判断
    if (position < 0 || position > this.length - 1) return false
    // 四种情况：1.length===1。 2.移除的是第一个，3.移除的是最后一个，4.非第一个和最后一个
    // 如果length===1
    if (this.length === 1) {
        this.head = null
        this.tail = null
        //移除的是第一个
    } else if (position === 0) {
        this.head = this.head.next
        this.head.prev = null
        // 移除的是最后一个
    } else if (position === this.length - 1) {
        this.tail = this.tail.prev
        this.tail.next = null
    } else {
        // 移除的是中间的
        let index = 0
        let current = this.head
        while (current) {
            if(index === position) {
                current.next.prev = current.prev
                current.prev.next = current.next
            }
            index += 1
            current = current.next
        }
    }
    // 长度改变 -1
    this.length -= 1
    return true
}
```

**测试代码**

```js
const dbList = new DoubleLinkList()
dbList.insert(0, 'AAA')
dbList.insert(1, 'BBB')
dbList.insert(2, 'CCC')
dbList.insert(3, 'DDD')
dbList.removeAt(1)
console.log(dbList);
```

![image-20221029150445120](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221029150445120.png)

### 7.remove(data) 

```js
// remover 从链表中移除指定数据
remove(data) {
    return this.removeAt(this.indexOf(data))
}
```



### 8.isEmpty()

```js
// 链表中包不包含任何元素
isEmpty() {
    return !!this.length
}
```

### 9.size()

```js
// 返回链表包含的元素个数
size() {
    return this.length
}
```

### 10.toString()

```js
// 输出链表中字符串的值，参数: 1：正向，-1：反向
toString(data) {
    if(data === 1) return this.forwardString()
    if(data === -1) return this.backwordString()
}
```

### 11.forwardString()

```js
// 返回正向遍历节点字符串形式
forwardString() {
    let res = ''
    let current = this.head
    while (current) {
        res += current.data + ' '
        current = current.next
    }
    return res
}
```

### 12.backwordString()

```js
// 返回反向遍历的节点的字符串形式
backwordString() {
    let res = ''
    let current = this.tail
    while (current) {
        res += current.data + ' '
        current = current.prev
    }
    return res
}
```

### 整体代码

```js
// 节点类
class Node {
    constructor(data) {
        this.data = data
        this.prev = null
        this.next = null
    }
}
// 封装双向链表类
class DoubleLinkList {
    constructor() {
        // 属性
        this.head = null
        this.tail = null
        this.length = 0
    }
    // 尾部添加一个节点
    append(data) {
        // 1.创建节点
        const newNode = new Node(data)
        // 2.判断添加的是否是第一个节点
        if (!this.length) {
            // 是第一个节点
            this.head = newNode
            this.tail = newNode
        } else {
            // 先将新节点的prev指向tail(最后一个节点)
            newNode.prev = this.tail
            // 再将tail(最后一个节点)的next指向新节点
            this.tail.next = newNode
            // 将最后一个节点设置成新节点
            this.tail = newNode
        }
        // 3.长度+1
        this.length += 1
    }
    // 返回正向遍历节点字符串形式
    forwardString() {
        let res = ''
        let current = this.head
        while (current) {
            res += current.data + ' '
            current = current.next
        }
        return res
    }
    // 返回反向遍历的节点的字符串形式
    backwordString() {
        let res = ''
        let current = this.tail
        while (current) {
            res += current.data + ' '
            current = current.prev
        }
        return res
    }
    // 指定位置插入一个节点
    insert(position, data) {
        // 1.越界判断
        if (position < 0 || position > this.length) return false

        // 2.根据data创建新节点
        const newNode = new Node(data)

        // 3.找到位置并插入
        let current = this.head
        let index = 0
        let prevCurrent = null // 用来记录当前循环的节点的prev
        // 3.1如果插入的时候链表是一个空链表
        if (this.length === 0) {
            this.head = newNode
            this.tail = newNode
            // 3.2如果插入的位置是0
        } else if (position === 0) {
            // 将当前第一个节点的prev指向新节点
            current.prev = newNode
            // 将新节点设置成第一个节点
            this.head = newNode
            // 新节点的next指向记录下来的current
            this.head.next = current
            // 3.3如果插入的位置最后一个（链表的长度）
        } else if (position === this.length) {
            newNode.prev = this.tail
            this.tail.next = newNode
            this.tail = newNode
            // 3.4 插入的位置不是头也不是尾
        } else {
            while (current) {
                if (index === position) {
                    current.prev.next = newNode
                    newNode.prev = current.prev
                    current.prev = newNode
                    newNode.next = current
                    break
                }
                index += 1
                current = current.next
            }
        }
        // 4.长度 +1
        this.length += 1
        return newNode
    }
    // 获取对应位置的元素
    get(position) {
        if (position < 0 || position > this.length) return null
        if (position < this.length / 2) {
            let index = 0
            let current = this.head
            while (current) {
                if (index === position) {
                    return current
                }
                index += 1
                current = current.next
            }
        } else {
            let current = this.tail
            let index = this.length - 1
            while (current) {
                if (index === position) {
                    return current
                }
                index -= 1
                current = current.prev
            }
        }
        return null
    }
    // 返回元素在链表中的索引
    indexOf(data) {
        let index = 0
        let current = this.head
        while (current) {
            if (current.data === data) {
                return index
            }
            current = current.next
            index += 1
        }
        return -1
    }
    // 修改某个位置的元素
    update(position, data) {
        // 越界判断
        if (position < 0 || position > this.length - 1) return false
        // 判断position位置距离head和tail哪个近
        if (position < this.length / 2) {
            let index = 0
            let current = this.head
            while (current) {
                if (index === position) {
                    current.data = data
                    return true
                }
                index += 1
                current = current.next
            }
        } else {
            let index = this.length - 1
            let current = this.tail
            while (current) {
                if (index === position) {
                    current.data = data
                    return true
                }
                index -= 1
                current = current.prev
            }
        }
    }
    // 从链表的特定位置移除一项
    removeAt(position) {
        // 越界判断
        if (position < 0 || position > this.length - 1) return false
        // 四种情况：1.length===1。 2.移除的是第一个，3.移除的是最后一个，4.非第一个和最后一个
        // 如果length===1
        if (this.length === 1) {
            this.head = null
            this.tail = null
            //移除的是第一个
        } else if (position === 0) {
            this.head = this.head.next
            this.head.prev = null
            // 移除的是最后一个
        } else if (position === this.length - 1) {
            this.tail = this.tail.prev
            this.tail.next = null
        } else {
            // 移除的是中间的
            let index = 0
            let current = this.head
            while (current) {
                if(index === position) {
                    current.next.prev = current.prev
                    current.prev.next = current.next
                }
                index += 1
                current = current.next
            }
        }
        // 长度改变 -1
        this.length -= 1
        return true
    }
    // 链表中包不包含任何元素
    isEmpty() {
        return !!this.length
    }
    // 返回链表包含的元素个数
    size() {
        return this.length
    }
    // 输出链表中字符串的值，参数: 1：正向，-1：反向
    toString(data) {
        if(data === 1) return this.forwardString()
        if(data === -1) return this.backwordString()
    }
}
```

# 集合结构

集合通常是由一组无序的、不能重复的元素构成

- 和数学中的集合名次比较相似，但是数学中的集合范围更大一些，也允许集合中的元素重复
- 在计算机中，集合通常表示的结构中元素是不允许重复的

也可以把集合看成一种特殊的数组

- 特殊之处就在于里面的元素没有顺序，也不能重复
- 没有顺序意味着不能通过下标值进行访问，不能重复意味着相同的对象在集合中只会存在一份

在2015年6月份发布的ES6中包含了Set类，可以直接使用它，但是为了明确内部的实现机制，我们还是自己来封装一下这个Set类

## **集合中常见的操作方法：**

- add(value)：向集合添加一个新的项
- remove(value)：从集合移除一个值
- has(value)：如果值在集合中，返回true，否则返回false
- clear()：清空集合中的项
- size()：返回集合所包含元素的数量，与数组length相似
- values()：返回一个包含集合中所有值的数组

## 封装集合

### 创建集合类

```js
// 封装集合类
class Set {
    constructor() {
        // 使用一个对象保存集合的元素
        this.items = {}
    }
}
```

### 1.add(value)

```js
// 向集合添加一个新的项 
add(value) {
    // 判断集合中是否含有此元素
    if (this.has(value)) return false
    // 将元素添加到集合中
    this.items[value] = value

    return true
}
```

### 2.remove(value)

```js
// 删除一个元素
remove(value) {
    // 判断是否含有该元素
    if (!this.has(value)) return false
    // 将元素从集合中删除
    delete this.items[value]
    return true
}
```

### 3.has(value)

```js
// 判断集合中是否包含此元素
has(value) {
    return this.items.hasOwnProperty(value)
}
```

### 4.clear()

```js
// 清空集合
clear() {
    this.items = {}
}
```

### 5.size()

```js
// 集合长度
size() {
    // Object.keys() 将对象中所以的key转变成数组
    return Object.keys(this.items).length
}
```

### 6.values()

```js
// 返回一个包含集合中所有值的数组
values() {
    return Object.keys(this.items)
}
```

## 集合间操作

就是集合与集合之间的操作

- 并集：对于给定的两个集合，返回一个包含两个集合中**所有**元素的集合
- 交集：对于给定的两个集合，返回一个包含两个集合中**共有**元素的集合
- 差集：对于给定的两个集合，返回一个包含**所有存在于第一个集合且不存在于第二个集合**的元素的新集合
- 子集：验证一个给定集合是否是另一集合的子集

![image-20221029202539688](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221029202539688.png)

### 并集实现

就是两个集合合并成一个新的集合

并集：

- 并集其实对应的就是数学中并集的概念

- 集合A和B的并集，表示为A U *B* ，定义如下

  ![image-20221029210006757](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221029210006757.png)

- 意思是*X*(元素)存在于A中，或*x*存在于B中

代码解析：

- 首先需要创建一个新的集合，代表两个集合的交集
- 遍历集合1中所有的值，并且添加到新集合中
- 遍历集合2中所有的值，并且添加到新集合中
- 将最终的新集合返回

**代码实现**

```js
// 并集
union(otherSet) {
    // this:集合对象A
    // otherSet:集合对象B

    // 1.创建一个新集合
    const unionSet = new Set()

    // 2.将A集合所以元素添加到辛几何中
    this.values().forEach(val => {
        unionSet.add(val)
    });

    // 3.取出otherSet的values，判断是否加入新集合
    let values = otherSet.values()
    values.forEach(val => {
        // 这里不用判断新集合是否包含val，因为add方法已经做判断
        unionSet.add(val)
    })
    // 4.将并集结果返回
    return unionSet
}
```

**测试**

```js
const setA = new Set()
setA.add(1)
setA.add(2)
setA.add(3)
const setB = new Set()
setB.add('a')
setB.add('b')
setB.add('c')
console.log(setA.union(setB));
```

![image-20221029212042227](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221029212042227.png)

### 交集实现

交集就是两个集合中重复的元素

交集：

- 交集其实对应的就是数学中交集的概念
- 集合A和B的交集，表示为A ∩ *B*，定义如下

​							![image-20221030095510306](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221030095510306.png)

- 意思是x(元素)存在于A中，且X存在于B中

代码解析：

- 创建一个新集合
- 遍历集合1中所有的元素，判断该元素是否在集合2中
- 如果在集合2中，将该元素加入到新集合中
- 将最终的新集合返回

**代码实现**

```js
// 交集
intersection(otherSet) {
    // this:集合对象A
    // otherSet:集合对象B

    // 1.创建一个新集合
    const newSet = new Set()

    // 2.遍历集合A
    this.values().forEach(val => {
        // 3.判断元素是否存在于集合B，如果存在，将该元素加入到新集合
        if (otherSet.has(val)) {
            newSet.add(val)
        }
    })
    // 4.最终返回新集合
    return newSet
}
```

**测试**

```js
const setA = new Set()
setA.add(1)
setA.add(2)
setA.add(3)
const setB = new Set()
setB.add('a')
setB.add('b')
setB.add('c')
setB.add(3)
console.log(setA.intersection(setB));
```

![image-20221030105355431](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221030105355431.png)

### 差集实现

集合A中的元素集合B没有包含，将没有包含的元素加入到新集合

差集

- 差集其实对应的就是数学中差集的概念
- 集合A和B的差集，表示为A -*B*，定义如下

![image-20221030105506641](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221030105506641.png)

- 意思是x(元素)存在于A中，且x不存在B中

代码解析

- 创建一个新的集合
- 遍历集合1中所有的元素，判断元素是否在集合2中
- 不存在集合2中，将该元素添加到新集合中
- 将新集合返回

**代码实现**

```js
// 差集
differenceSet(otherSet) {
    // this:集合对象A
    // otherSet:集合对象B

    // 1.创建一个新集合
    const newSet = new Set()

    // 2.遍历集合A,判断元素是否在集合B中
    this.values().forEach(val => {
        if (!otherSet.has(val)) {
            newSet.add(val)
        }
    })
    // 3.返回新集合
    return newSet
}
```

**代码测试**

```js
const setA = new Set()
setA.add(1)
setA.add(2)
setA.add(3)
const setB = new Set()
setB.add('a')
setB.add('b')
setB.add('c')
setB.add(3)
console.log(setA.differenceSet(setB));
```

![image-20221030171658010](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221030171658010.png)

### 子集实现

子集：

- 子集其实对应的就是数学中子集的概念
- 集合A是B的子集（或集合B包含了A），表示为A⊆B，定义如下

![image-20221030111441219](https://haoran-img.oss-cn-hangzhou.aliyuncs.com/typora_img/image-20221030111441219.png)

- 意思是集合A中的每一个X（元素），也需要存在于B中

代码解析：

- 遍历集合1中所有的元素，判断元素是否在集合2中
- 如果集合1中的每一个元素集合2都存在，那么集合1就是集合2的子集

**代码实现**

```js
// 子集
subSet(otherSet) {
    // this:集合对象A
    // otherSet:集合对象B
    // 1.循环集合A，查看集合B中是否含有集合A的元素
    for (let i = 0; i < this.values().length; i++) {
        const val = this.values()[i];
        if (!otherSet.has(val)) {
            // 2.如果有一个元素集合B没有，那么不是子集，返回false
            return false
        }
    }
    // 通过循环说明集合A中的元素都在集合B里包含，返回true
    return true
}
```

**代码测试**

```js
const setA = new Set()
setA.add(1)
setA.add(2)
setA.add(3)
const setB = new Set()
setB.add('a')
setB.add('b')
setB.add('c')
setB.add(3)
setB.add(2)
setB.add(1)
console.log(setA.subSet(setB)); // true
```

# 字典结构

### 一. 认识字典

#### 字典的介绍

- 生活中的字典
  - 中文字典我们可以根据拼音去查找汉字, 并且找到汉字对应的词以及解释.
  - 英文字典也是类似, 根据英文字母找到对应的单词, 再查看其翻译和应用场景.
  - 很多编程语言中都有字典的概念
- 字典有什么特点呢?
  - 字典的主要特点是一一对应的关系.
  - 比如保存一个人的信息, 在合适的情况下取出这些信息.
  - 使用数组的方式: [18, "Coderwhy", 1.88]. 可以通过下标值取出信息.
  - 使用字典的方式: {"age" : 18, "name" : "Coderwhy", "height": 1.88}. 可以通过key取出value
- 字典的映射关系:
  - 有些编程语言中称这种映射关系为字典, 因为它确实和生活中的字典比较相似. (比如Swift中Dictionary, Python中的dict)
  - 有些编程语言中称这种映射关系为Map, 注意Map在这里不要翻译成地图, 而是翻译成映射. (比如Java中就有HashMap&TreeMap等)
- 字典和数组:
  - 字典和数组对比的话, 字典可以非常方便的通过key来搜索对应的value, key可以包含特殊含义, 也更容易被人们记住.
- 字典和对象:
  - 很多编程语言(比如Java)中对字典和对象区分比较明显, 对象通常是一种在编译期就确定下来的结构, 不可以动态的添加或者删除属性. 而字典通常会使用类似于哈希表的数据结构去实现一种可以动态的添加数据的结构.
  - 但是在JavaScript中, 似乎对象本身就是一种字典. 所有在早期的JavaScript中, 没有字典这种数据类型, 因为你完全可以使用对象去代替.
  - 但是这里我们还是按照其他语言经常使用字典的方式去封装一个字典类型, 方便我们按照其他语言的方式去使用字典. (虽然本质上它内部还是用了一个对象, 后面学习完哈希表我会简单谈一下对象和哈希表的关系)

#### 创建字典类

- 我们向之前封装集合一样, 封装一个字典的构造函数

  

  ```javascript
  // 创建字典的构造函数
  function Dictionay() {
      // 字典属性
      this.items = {}
      
      // 字典操作方法
  }
  ```

- 代码解析:

  - 非常简单, 创建一个Dictionary的构造函数, 用于我们字典的封装.
  - 在字典中, 我们使用了一个items属性, 该属性是一个Object对象.
  - 也就是我们的字典是基于Object封装的, 这个不难理解: 就像我们之前封装Stack和Queue是基于数组的一样.
  - 后面我们在添加字典相关的操作

### 二. 操作字典

> 我们之前封装的数据结构, 都有封装各种操作, 字典也是一样

#### 常见的操作

- 字典常见的操作
  - `set(key,value)`：向字典中添加新元素。
  - `remove(key)`：通过使用键值来从字典中移除键值对应的数据值。
  - `has(key)`：如果某个键值存在于这个字典中，则返回`true`，反之则返回`false`。
  - `get(key)`：通过键值查找特定的数值并返回。
  - `clear()`：将这个字典中的所有元素全部删除。
  - `size()`：返回字典所包含元素的数量。与数组的`length`属性类似。
  - `keys()`：将字典所包含的所有键名以数组形式返回。
  - `values()`：将字典所包含的所有数值以数组形式返回。

#### 操作的实现

- 我们将这些方法放在一起实现

  

  ```javascript
  // 创建字典的构造函数
  function Dictionay() {
      // 字典属性
      this.items = {}
  
      // 字典操作方法
      // 在字典中添加键值对
      Dictionay.prototype.set = function (key, value) {
          this.items[key] = value
      }
  
      // 判断字典中是否有某个key
      Dictionay.prototype.has = function (key) {
          return this.items.hasOwnProperty(key)
      }
  
      // 从字典中移除元素
      Dictionay.prototype.remove = function (key) {
          // 1.判断字典中是否有这个key
          if (!this.has(key)) return false
  
          // 2.从字典中删除key
          delete this.items[key]
          return true
      }
  
      // 根据key去获取value
      Dictionay.prototype.get = function (key) {
          return this.has(key) ? this.items[key] : undefined
      }
  
      // 获取所有的keys
      Dictionay.prototype.keys = function () {
          return Object.keys(this.items)
      }
  
      // 获取所有的value
      Dictionay.prototype.values = function () {
          return Object.values(this.items)
      }
  
      // size方法
      Dictionay.prototype.size = function () {
          return this.keys().length
      }
  
      // clear方法
      Dictionay.prototype.clear = function () {
          this.items = {}
      }
  }
  ```

- 代码解析:

  - 代码比较简单, 和之前实现的Set也比较类似, 不再深度解析.

#### 字典的使用

- 我们来使用和测试一下字典类:

  

  ```javascript
  // 创建字典对象
  var dict = new Dictionay()
  
  // 在字典中添加元素
  dict.set("age", 18)
  dict.set("name", "Coderwhy")
  dict.set("height", 1.88)
  dict.set("address", "广州市")
  
  // 获取字典的信息
  alert(dict.keys()) // age,name,height,address
  alert(dict.values()) // 18,Coderwhy,1.88,广州市
  alert(dict.size()) // 4
  alert(dict.get("name")) // Coderwhy
  
  // 字典的删除方法
  dict.remove("height")
  alert(dict.keys())// age,name,address
  
  // 清空字典
  dict.clear()
  ```

