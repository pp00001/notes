# Description
notes.


# More

- [gitee](https://gitee.com/bovenson)
- [cnblogs](https://www.cnblogs.com/bovenson)

# TODO

- [x] ~~`Python`中`set`原理及效率~~

- [x] ~~切片操作的效率(对比遍历)~~

- [x] 内置函数`sum`的效率

  ```python
  s = [1, 2, 3] * 1000000
  print(time.clock())
  sum(s)
  print(time.clock())
  print(time.clock())
  res = 0
  for i in s:
      res += i
  print(time.clock())
  
  # output
  0.032466
  0.046174
  0.046191
  0.220772
  ```

- [x] ~~`all() / any()`~~

- [x] `set() == set()`

  ```shell
  >>> set([1, 2]) == set([1, 2])
  True
  >>> s1 = set([1, 2])
  >>> s2 = set([1, 2])
  >>> s1 == s2
  True
  >>> s1.add(3)
  >>> s1 == s2
  False
  >>> l1 = [1, 2]
  >>> l2 = [1, 2]
  >>> l1 == l2
  True
  >>> l1.append(3)
  >>> l1 == l2
  False
  ```

- [x] 整理MVC笔记

- [x] 整理函数式编程笔记

- [ ] Java

  - [x] Java函数式编程

- [x] ~~JVM~~

  - [x] ~~垃圾回收~~

- [x] SpringMVC

- [ ] 剑指Offer

  - [x] 数组
  - [x] 字符串
  - [x] 链表
  - [x] 树
  - [x] 栈和队列
  - [x] 查找排序
    - [x] 二分
    - [x] 快排
    - [x] 旋转数组的最小数字
  - [x] 回溯
  - [ ] 动规
  - [ ] 贪心

- [ ] C++

  - [ ] 基础
    - [ ] 面向对象
    - [ ] 模板与范型编程
    - [ ] 抛出异常
    - [x] new & malloc
    - [ ] 堆 & 栈
    - [ ] struct & class
      - [ ] sizeof(...struct)
    - [ ] 指针 & 引用
    - [ ] 友元
    - [ ] move
    - [ ] `* & &&`
    - [x] `push_back emplace_back`
  - [ ] 特性
    - [x] STL
      - [x] 算法
      - [x] 容器
        - [x] stack
      - [x] 迭代器
      - [x] 堆

- [ ] 操作系统

  - [x] 引论
  - [ ] 进程管理
    - [ ] 经典进程同步问题，使用记录型信号量、AND信号量、管程解决
  - [ ] 处理机调度
  - [ ] 存储器管理
  - [ ] 虚拟存储器
  - [ ] 输入输出系统
  - [ ] 文件管理
  - [ ] 磁盘存储器的管理
  - [x] 内核
  - [ ] 计算机物理结构
    - [ ] CPU

- [x] CMake

- [x] thrift

- [ ] 算法

  - [ ] 经典
    - [ ] 查找
      - [x] 二分
    - [ ] 排序
      - [ ] 归并
      - [x] **快排**
      - [x] **堆排序**
  - [x] 回溯
  - [x] 动规
  - [ ] 贪心 

- [ ] 数据结构

  - [ ] 树
    - [ ] **平衡二叉树**
    - [x] **堆**

- [ ] 网络
  - [ ] TCP/IP
  - [ ] HTTP

- [ ] 架构

  - [ ] protocolBuffer

- [ ] Linux
  - [x] grep
  - [ ] sort
  - [ ] wc
  - [ ] uniq
  - [ ] cut
  - [x] sed
  - [x] awk

# BOOK

- [ ] 并行程序设计导论
- [ ] 计算广告

# Task

- 20181011
  - [x] 堆
    - [x] 构建
    - [x] 插入
    - [x] 删除
    - [x] 排序

- 20181013
  - [ ] 平衡二叉搜索树
    - [ ] 构建
    - [ ] 插入
    - [ ] 删除