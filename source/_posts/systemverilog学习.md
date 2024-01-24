---
title: SystemVerilog学习
date: 2023-12-16 10:58:42
tags: 
    - 学习
    - 代码
mathjax: ture
cover: /img/systemverilog学习.jpg
categories: 学习
---

# 第I章 验证导论
## 基本测试平台的功能
测试平台的用途在于确定待测设计的正确性，包含以下步骤:  
1.产生激励  
2.把激励施加到DUT上  
3.捕捉响应  
4.检验正确性  
5.对照整个验证目标测算进展情况

# 第II章 数据类型
## 内建数据类型
两种基本类型：变量和线网，各自都可以有四种取值：1,0,Z,X
### 1.逻辑(logic)类型
SystemVerilog对经典的reg数据类型进行改进，使得它除了作为一个变量以外，还可以被连续赋值、门单元和模块所驱动，这种改进的数据类型被称为logic。  
任何使用线网的地方均可以使用logic，但要求logic不能有多个结构性的驱动
```
//logic类型使用实例
module logic(input logic);
  parameter CYCLE=20;
  logic q,q_1,d,clk,rst_1;
  inital begin
    clk=0;                           //过程赋值
    forever # (CYCLE/2) clk=~clk;
  end

  assign rst_1=~rst_h;               //连续赋值
  not n1(q_1,q);                     //q_1被门驱动
  my_dff d1(q,d,clk,rst_1);          //q被模块驱动
endmodule
```
### 2.双状态数据类型
最简单的双状态数据类型是bit，无符号。另外四种带符号的双状态数据类型是byte,shourtint,int和longint。

## 定宽数组
### 初始化和声明
必须声明上下界  
`int lo_hi[0:15];  //16个整数[0]...[15]`

声明并使用多维数组  
`int array[0:7][0:3];  //完整的声明`

### 常量数组
常量数组：一个单引号加大括号来初始化数组  
`int ascend[4]='{0,1,2,3};  //对4个元素进行初始化`

### for 和 foreach
- i被声明为for循环内的局部变量
- 在foreach循环中，只需要指定数组名并在其后面的方括号中给出索引变量，SV就会自动遍历数组中的元素。

### 复制和比较
- 比较仅限于等于或比较不等于
- 操作符?:一个袖珍的if语句

### 使用位下标和数组上标
```
inital begin
  bit [31:0] src[5] = '{5{5}};
  $display (src[0],,      // 'b101或'd5
            src[0][0],,   // 'b1
            src[0][2:1]);  // 'b10
end
```

### 合并数组
数组大小定义的格式必须是[msb:lsb]，而不是[size]，就是个数

## 动态数组
动态数组在声明时使用空的下标[ ].

## 队列
队列的声明时使用带有美元符号的下标:[$]。队列元素的编号从0到\$

## 关联数组
创建大容量数组可以用动态数组，创建超大容量用关联数组

## 链表

## 数组的方法