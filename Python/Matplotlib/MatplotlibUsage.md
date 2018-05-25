---
title: Matplotlib
tags:
	- Python
categories:
	- Python
---



# 简介

Matplotlib

- 数据可视化

# 安装

```shell
sudo pip3 install matplotlib
# or
sudo apt install python3-matplotlib
```

# 示例程序

```python
import numpy as np
import matplotlib.pyplot as plt


x = np.linspace(0, 10, 1000)    # 作图的变量自变量
y = np.sin(x) + 1               # 因变量y
z = np.cos(x**2) + 1            # 因变量z

plt.figure(figsize=(8, 4))      # 设置图像大小
plt.plot(x, y, label='$\sin x+1$', color='red', linewidth=2)    # 作图, 设置标签, 线条颜色, 线条大小
plt.plot(x, z, 'b--', label='$\cos x^2+1$')
plt.xlabel('Time(s) ')  # x轴名称
plt.ylabel('Volt')      # y轴名称
plt.ylim(0, 2.2)        # 显示的y轴范围
plt.legend()            # 显示图例
plt.show()              # 显示作图结果
```

**运行结果**

![](img/figure-01.png)