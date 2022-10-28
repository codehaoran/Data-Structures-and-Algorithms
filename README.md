# 目录

- [数据结构与算法前言](#数据结构与算法前言)
- [栈结构(Stack)](#栈结构(Stack))
- [队列结构(Queue)](#队列结构(Queue))
- [单向链表](#单向链表)
- [双向链表](#双向链表)



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

**链表中的常见操作：**

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

**双向链表常见的操作（方法）：**

- append（data）：向链表尾部添加一个新的项；
- inset（position，data）：向链表的特定位置插入一个新的项；
- get（data）：获取对应位置的元素；
- indexOf（data）：返回元素在链表中的索引，如果链表中没有元素就返回-1；
- update（position，data）：修改某个位置的元素；
- removeAt（position）：从链表的特定位置移除一项；
- isEmpty（）：如果链表中不包含任何元素，返回trun，如果链表长度大于0则返回false；
- size（）：返回链表包含的元素个数，与数组的length属性类似；
- toString（）：由于链表项使用了Node类，就需要重写继承自JavaScript对象默认的toString方法，让其只输出元素的值；
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

### 2.**insert**(position, data)

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

### 4.indexOf(data)

### 5.update(position, data)

### 6.removeAt(position)

### 7.isEmpty()

### 8.size()

### 9.toString()

### 10.forwardString()

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

### 11.backwordString()

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
