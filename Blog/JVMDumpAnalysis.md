---
Title: 针对JVM大core分析
---

# 场景

使用jmap工具将Java服务堆栈保存至文件，接着使用Mat工具分析堆栈信息是处理Java程序内存泄漏问题的一种思路。现实场景中，通过jmap工具dump后的堆栈文件可能较大(10G, 40G, 甚至更多)，个人电脑往往没有足够的内存进行处理。

一种可行的方案是使用mat工具，在服务器中生成索引结果，然后拷贝至本地进行分析。

# 保存堆栈信息

# 

