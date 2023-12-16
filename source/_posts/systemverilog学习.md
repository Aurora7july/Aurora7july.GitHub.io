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
