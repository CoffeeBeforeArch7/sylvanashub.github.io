---
layout: post
title:  "任务与函数_冒泡排序"
date:   2024-4-3 16:02:26 +0700
tags:
  - Verilog HDL
---

---

# 系统任务

## **一、仿真时间函数**

在Verilog HDL中有两种类型的时间系统函数：\$time和$realtime。用这两个时间系统函数可以**得到当前的仿真时刻**。该时刻是以模块的仿真时间尺度timescale为基准的。

不同之处：

- $time返回64位的整型时间(四舍五入)

- $realtime返回实型时间（根据时间精度来的）

## 二、**监控任务**

监控任务$monitor作用是**连续监控指定的参数**，只要参数表中的参数值发生变化，参数表就在当前仿真时刻结束时显示。往往是在一个initial块内进行调用。

## 格式说明：

由“%”和格式字符（t，b，d，o，h）组成。它的作用是将输出的数据转换成指定的格式输出。格式说明总是由“%”字符开始的

例：对D、Clk和Q的值进行监控

```verilog
$monitor (“At%t, D=%d, Clk=%d”, $time, D, Clk, “and Q is %d” , Q);

输出：
At 24, D=x, Clk=x and Q is 0;

At 25, D=x, Clk=x and Q is 1;

At 30, D=0, Clk=x and Q is 1;
```

\$monitor**off** 任务用于停止监控任务$monitor;

\$monitor**on** 任务用于启动监控任务$monitor

\$monitor往往在initial块中调用，只要不调用\$monitoroff，$monitor便不间断地对其所设定的信号进行监视。

---

## **三、仿真控制任务**

仿真控制任务用于使仿真进程停止。该类任务有两个：

```verilog
$finish（完成）
$stop（暂停）

例：initial #500 $stop；
```



## **四、随机函数random**

$random%60；区别于{$random}%60；前者输出的是有符号数，-59~+59

## **五、文件输出任务**

```verilog
$readmemb //读取二进制格式数
$readmemh //读取十六进制格式数
```

这两个系统任务用于从**文本文件**中读取数据并将数据**加载到存储器中。**

标准格式：$readmemb(“<路径/数据文件名>”，<存储器名>，<起始地址>，<结束地址>)；

举例说明：

```verilog

先定义一个有256个地址的字节存储器mem：
reg[7：0] mem[1：256]；

下面给出的系统任务以各自不同的方式装载数据到存储器mem中

initial $readmemh(“mem.data” ，mem)；//1-256
initial $readmemh("mem.data” ，mem，16)；//161-256
                  initial $readmemh(“mem.data”，mem，128，1)；//128-1
```

#### 练习：

1. 如何用监控任务显示当前仿真时间以及变量的值

2. 用系统随机函数产生【0-14】之间的无符号数

```verilog
1： $monitor($time, "a = %b,b = %b"， a,b);
2： a = {$random}%15;
```

---

# **编译预处理语句**

## 一、define语句

宏定义语句：用一个指定的标志符（即宏名）来代表一个字符串（即宏内容）

宏定义的作用：

- 以一个简单的名字代替一个长的字符串或复杂表达式

- 以一个有含义的名字代替没有含义的数字和符号

**注意：**宏定义不是Verilog HDL语句，不必在行末加分号！



**格式：**‵define 标志符（即宏名）字符串（即宏内容）

‵ define IN ina+inb+inc+ind

```verilog
‵define expression a + b + c + d

assign out = ‵expression + e;

assign out = a + b + c + d + e
```

## 二、 ‵ include语句

文件包含语句：一个源文件可将另一个源文件的全部内容包含进来。没有对文件进行连接，只是把对应文件的代码放这里，相当于files.f文件的指向作用

格式：‵ include “文件名”

#### 使用注意：

- 一个‵include语句只能指定一个被包含的文件；若要包含n个文件，需用n个‵include语句。

- ‵include语句可出现在源程序的任何地方。被包含的文件若与包含文件不在同一子目录下，必须指明其路径！

## 三、 ‵ timescale语句

时间尺度语句：用于定义跟在该命令后模块的时间单位和时间精度

**格式：**‵timescale <时间单位> / <时间精度>

- 时间单位——用于定义模块中仿真时间和延迟时间的基准单位；

- 时间精度——用来声明该模块的仿真时间和延迟时间的精确程度。

**注意：**时间精度值不能大于时间单位值

例：

```verilog
‵timescale 10ns / 1ns //时间单位为10ns，时间精度为1ns 
```







