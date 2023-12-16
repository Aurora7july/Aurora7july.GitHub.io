---
title: Verilog学习
date: 2023-09-19 15:18:51
tags: 
    - 学习 
    - 代码
mathjax: ture
cover: /img/Verilog学习.jpg
categories: 学习
---
**Verilog学习**

## verilog HDL 层次化设计
### 模块和端口
1. 模块=模块名定义+端口描述+内部功能逻辑
2. 逻辑功能描述：变量声明、数据流描述语句、门级实例化描述语句、行为描述语句、任务与函数。
3. 关键词：`module`定义模块名字；`input`、`output`指定端口方向；`endmodule`结束模块描述。
4. 模块定义格式：
   ```
   module 模块名
   端口定义
   ......
   unmodule
   ```
5. 端口定义：有两种格式
   - 普通风格
      ```
      module 模块名
      input [位宽-1: 0] 端口名1，端口名2  
      output [位宽-1: 0] 端口3 
      inout [位宽-1: 0]端口4
      ```
   - ANSI C风格
      ```
      module 模块名
      ( input [位宽-1: 0] 端口名1，端口名2  
        output [位宽-1: 0] 端口3 
        inout [位宽-1: 0]端口4
        );
      ```
6. 实例化：不允许嵌套，模块之间只能通过实例化
   
## 层次化设计思想
- 自顶向下  
  类似于根据一张图纸造物
- 自底向上  
  类似于根据材料造物，可以是已知也可以是未知的
  
## Testbench概念
用于测试设计的电路的功能是否正常

## verilog HDL基本语法
### 词法约定         
1. 空白符：空格`\b`，制表`\t`和换行
2. 注释：单行`//`，多行`*/.../*`(不允许嵌套)
3. 操作符：单目操作符`~`，双目操作符`+`，三目操作符`?`
4. 标识符：
   - 第一个字符是字母或下划线
   - 区分大小写
   - 转义`\`
   - 空白符结束
5. 关键字：均为小写
### 数据类型
-- 线网：除`tri`和`reg`所有网线类型不能存储数据值
-- 变量：抽象的数据存储单元
1. 逻辑值与常量
- 基本值：0/1真假，x未知，z高阻(不分大小写)
- 整数：二进制、十进制、十六进制、八进制  
         格式：`[位宽]'[进制][数值]`  
         负数：加负号
- 实数：十进制和科学计数法(可用e或E表示)
2. 逻辑强度：supply最强，highz最弱
- 线网类型：`wire`和`tri`最常见  
   格式：`wire [7:0] datain, dataoutt`(*两个8位的wire数据)【这是举例】
- 变量类型：`reg`类型、`integer`型、`real`型、`time`型
- 向量：位宽大于1
- 数组：数组中的每一个元素可以是标量也可以是向量
- 参数：`defparam语句`(同样不可嵌套)  
3. 表达式
- 操作数
- 算术操作符：单双目操作数。单目`+ -`表正负，双目`* / + -`运算符号
- 逻辑操作符：逻辑与`&&`，逻辑或`||`，逻辑非`!`
- 关系操作符：`>` `<` `>=` `<=`
- 相等操作符：逻辑相等`==`，逻辑不等`!=`，逻辑全等`===`，逻辑非全等`!==`
- 按位操作符：反`~`，与`&`，或`|`，异或`^`，同或`^~, ~^`
- 缩减操作符：缩减与`&`，缩减与非`-&`，缩减或`|`，缩减或非`~|`，缩减异或`^`，缩减同或`~^, ^~`
- 位移操作：右移`>>`，左移`<<`，算术左移`<<<`，算术右移`>>>`
- 拼接操作符：格式`{操作1，操作2，操作3，...，操作n}`
- 条件操作符：根据条件表达式的值从两个表达式中选择一个表达式作为输出结果，格式`条件表达式? 真表达式 ： 假表达式`

## Verilog HDL行为描述
### Verilog HDL基本描述形式
1. 数据流描述方法
   ```
   assing [延迟] wire类型 = 表达式
   ```
2. 行为描述方式
   两种语句：initial和always
   ```
   always @(事件控制列表) begin
   ···
   end
   或
   intial begin
   ···
   end
   ```
3. 层次化描述方式
   ```
   模块名 实例名
   ```

### 结构化过程语句
**initial和always语句不能相互嵌套使用**
1. initial语句  
   从仿真的0时刻开始，只执行一次。
   ```
   reg a, b, c; //initial中只有一条赋值语句
   initial
      a = 1'b0; 
   //若含多条赋值语句，需要begin end
   initial begin
      b = 1'b0;
      c = 1'b0;
   end
   ```
2. always语句  
   从仿真的0时刻开始，会重新执行命令
   ```
   reg a;
   initial a = 0;
   always #50 a =-a;
   //从0开始，每隔50个时间单位的反复操作
   ```

### 顺序块和并行块
1. 顺序块：按书写顺讯依次执行
2. 并行块：`fork`是同时开始
3. 块语句的其他特点
   - 嵌套块
   - 命名块

### 过程赋值语句
1. 阻塞赋值语句
   用`=`作为赋值符，按顺序执行
   ```
   reg a, b;
   initial begin
      a = 1'b0; 
      b = 1'b0;
      #10 a = 1'b1; //阻塞赋值语句对a赋新值，a变为1后才继续执行后面的命令
          b = a;
   end
   ```
2. 非阻塞赋值语句
   用`<=`作为赋值符，不会阻塞同一个块语句中的其他语句的执行
   ```
   reg a, b;
   initial begin
      a = 1'b0;
      b = 1'b0;
      #10 a <= 1'b1; //用非阻塞赋值语句赋值，赋值还未完成先完成后面的语句
          b <= a; //由于a的赋值未完成，所以b的值还是0
   end
   ```

### 条件语句
有三种情况，`if`表达式，`if-else`表达式，`if-else if`表达式。  
*注意*，这里容易弄混，一定要搞清楚。

### 多路分支语句
当分支特别多时，`if` `else`语句非常不好用，就可以使用`case`语句  
`case`语句的关键词：`case` `default` `endcase` 格式如下
```
case(表达式)
   分支表达式1: 语句1
   分支表达式2: 语句2
   ···
   default: 默认语句
   endcase
```

### 条件语句和多路分支语句的比较
`if...else`语句有优先级，而`case`语句没有，是并行的关系。

### 循环语句
1. while循环
   ```
   while(条件表达式)
      语句：
   ```
   当表示式为真时，则循环执行里面的雨具；如果为假，中止循环并跳出while。如果while中表达式的值为x或z时，当作假处理。
2. for循环
   ```
   for(循环变量初值;循环结束条件;循环变量增值)
   ```
   在for中，C语言有i++，而verilog没有，改成i=i+1
3. repeat循环
   ```
   repeat(循环次数表达式)
   ```
4. forever循环

### 时序控制
1. 延迟控制  
   分为常规和内嵌，两者区别为：常规是整个语句执行后，在推迟的时间后，赋值语句开始计算；内嵌是开始执行时刻就立即计算表达式右边的值，此值会一直保持至延迟结束。
* 常规延迟  
  ```# [延迟值] 语句```
* 内嵌延迟  
  ```语句 #[延迟值]```
2. 事件控制  
   发生某个事件(变量、线网信号或表达式的值发生变化)之后，整个逻辑发生变化
* 边沿敏感事件控制
  用边缘敏感符号`@`，格式为
  ```
  @ 事件
      语句;
  ```
  这里有个**关键字:posedge(上升沿跳变)/negedge(下降沿跳变)** 记住即可  
  如果出现了多个敏感事件，则用`or`或者`,`即可
* 电平敏感事件控制
  以信号值变化的边沿为标志的，即一定要达到指定信号的某个值的变化边沿才会触发执行，关键字为`wait`
  ```
  wait(事件) 语句;
  ```
  当事件为真时，后面的语句才会执行
* 时序控制语句在综合代码中的应用
  在进行电路综合时，延迟控制语句会被综合工具自动忽略，当作无延迟处理

## 组合逻辑建模
### 数字电路建模方式
电路与代码的一一对应关系

### 组合逻辑的门级描述
与门(and)、与非门(nand)、或门(or)、或非门(nor)、异或门(xor)、同或门(xnor)、缓冲器(buf)、非门(not)、三台缓冲器控制信号低电平有效(bufif0)、三台缓冲器控制信号高电平有效(bufif1)、三态非门控制信号低电平有效(notif0)、三态非门控制信号高电平有效(notif1)

### 组合逻辑的数据流描述
1. 连续赋值语句  
`assign[延迟]wire型变量=表达式;`


2. 数据流描述  
   利用数据流描述可以很方便的描述一个加法器等，用符号就可以了，比如`+` `*`等

### 组合逻辑的行为描述

### 组合逻辑建模实例
1. 比较器
2. 译码器和编码器

## 时序逻辑电路
### 时序逻辑建模概述
时序逻辑电路指的是在verilog HDL所描述的电路中，包含一个或多个存储单元。这些存储单元可以是边沿触发的寄存器，或者是电平触发的锁存器。由于引入了存储单元，时序逻辑电路具有了“记忆”功能，可以记录当前时刻之前的输入激励情况及电路状态。
### 寄存器和锁存器设计
1. 寄存器实例
   在`always`后面的敏感列表中加入边沿敏感的信号，即可设计出一个简单的寄存器。`posedge`是在时钟的上升沿触发并采集数据端口的值；`negedge`则在下降沿触发。

```
module dff
(
   input i_clk,
   input i_din,
   output reg o_dout
);

always@(posedge i_clk) //在always语句的敏感列表@()中加入边沿敏感的时钟信号i_clk
  o_dout <= i_din;

endmodule
```

2. 锁存器的设计实例
   用verilog描述一个的锁存器，该锁存器在控制信号i_en为高电平时开启，为低电平时锁存器当前值
```
module latch
(
   input i_en,
   input i_din,
   output reg o_dout
);

always@(i_den or i_en) //敏感列表中没有边沿触发的信号
  if(i_en)
    o_dout <= i_din;

endmodule 
```
### 寄存器和锁存器的推断
1. 寄存器的推断
* 寄存器是一种时序元件，用于存储数据，并且在时钟信号的上升沿或下降沿触发时更新数据。
* 寄存器在时钟边沿触发时，将其输入数据传递到输出，具有确定的时序行为。
* 在Verilog中，通常使用触发器（Flip-Flops）来实现寄存器。
```
//举例说明
module DFF (
    input wire D,    // 数据输入
    input wire CLK,  // 时钟信号
    output wire Q    // 数据输出
);

always @(posedge CLK) begin
    Q <= D;
end

endmodule
```
2. 锁存器的推断
* 锁存器是一种组合逻辑元件，它不需要时钟信号，而是根据输入信号的变化实时更新输出。
* 锁存器不是时序元件，通常应该避免在数字电路中使用锁存器，因为它们可能会导致不稳定的行为和时序问题。
* 锁存器可能会导致冒险条件，因此在设计中应该谨慎使用。
```
//举例说明
module SRLatch (
    input wire S,  // 设置输入
    input wire R,  // 复位输入
    output wire Q  // 数据输出
);

assign Q = S & ~R;

endmodule
```
### 存储器的设计与建模
1. ROM建模  
ROM是只读存储器
```
//变量z以数组的方式描述了一个ROM
//由于使用了inital语句，因此该代码只能适用于仿真，不能综合
module rom_sim
(
   input [2:0] i_sel,
   output [3:0] o_dat
);

   reg [3:0] rom [0:7]; //通过数组声明存储器变量

      inital begin //利用inital语句为ROM赋值
      rom[0] = 4'b1001;
      rom[1] = 4'b1011;
      rom[2] = 4'b0010;
      rom[3] = 4'b0011;
      rom[4] = 4'b1110;
      rom[5] = 4'b0000;
      rom[6] = 4'b0000;
      rom[7] = 4'b0000;
   end

   assign o_dat = rom[i_sel];
endmodule
```
2. RAM建模  
一个电平变化触发的16位宽RAM模型通常是基于时序逻辑的，使用触发器来存储数据。以下是一个简单的电平变化触发的16位宽RAM模型示例，使用2个16位触发器作为存储元件：
```
module LevelSensitiveRAM16 (
    input wire [3:0] address,       // 4位地址输入
    input wire [15:0] data_in,      // 16位数据输入
    input wire write_enable,       // 写使能信号
    input wire read_enable,        // 读使能信号
    output wire [15:0] data_out    // 16位数据输出
);

reg [15:0] memory [0:15];  // 16个16位触发器，模拟RAM的存储单元

always @(posedge write_enable or posedge read_enable) begin
    if (write_enable) begin
        // 写操作：将输入数据写入存储器指定地址
        memory[address] <= data_in;
    end
    if (read_enable) begin
        // 读操作：从存储器指定地址读取数据
        data_out <= memory[address];
    end
end

endmodule
```
### 同步有限状态机
同步有限状态机（Synchronous Finite State Machine，SFSM）是一种在特定时钟信号下运行的状态机，其中状态的转换和输出的更新都与时钟信号同步。SFSM 包括状态寄存器、组合逻辑块以及时钟信号。

以下是一个简单的 2 状态同步有限状态机的示例，其状态转换和输出更新是同步的：
```
module SynchronousFSM (
    input wire clk,          // 时钟信号
    input wire rst,          // 复位信号
    output wire [1:0] state, // 2位状态输出
    output wire output       // 输出信号
);

reg [1:0] current_state;   // 当前状态寄存器

always @(posedge clk or posedge rst) begin
    if (rst) begin
        // 复位操作
        current_state <= 2'b00;  // 将状态初始化为00
    end else begin
        // 状态转换逻辑
        case (current_state)
            2'b00: current_state <= 2'b01;  // 从00转换到01
            2'b01: current_state <= 2'b10;  // 从01转换到10
            2'b10: current_state <= 2'b00;  // 从10转换到00
        endcase
    end
end

assign state = current_state;   // 输出当前状态

always @(posedge clk) begin
    // 输出逻辑
    case (current_state)
        2'b00: output <= 1'b0;  // 当前状态为00时输出0
        default: output <= 1'b1;  // 其他状态时输出1
    endcase
end

endmodule
```
### 时序逻辑建模实例
1. 计数器  
2. 串并/并串转换器
```
module p2s(clk,en,rsy,pin,sout)；
input clk,en,rst;
input [7:0] pin;
output sout;
output end; #并转串传输结束

reg[2:0] cnt;
reg[7:0] data;

always@(posedge clk or posedge rst)
  if(rst)
    sout <= 1'b0;
    cnt <= 3'b0;
  end
  else if(en) begin
    cnt <= cnt+1'b1;
    sout <= data[0];
  end

always@(posedge clk or posedge rst)
  if(rst)
    data <= 8'b0;
  else
    if(cnt==3'b0)
      data <= pin;
    else
      data <= {1'b0,data[7:1]};

always@(posedge clk or posedge rst)
  if(rst)
    end <= 1'b0;
  else
    end <= (cnt==3'b111);
endmodule
```
3. 时钟分频电路

### 练习题
5.4  
```
module 8bit(
   input wire clk,
   input wire rst,
   input wire [7:0] data_in,
   output wire [7:0] data_out
);

   reg [7:0] reg_data;

   always @(nesedge clk or posedge rst)begin
     if (rst) 
        reg_data <= 8'b0;
       else
        reg_data <= date_in;
        end
   end

   assign data_out = reg_data;

endmodule 
```
5.6
```
module 32_RAM(clk,wr,addr,rdata,wdata);
   input clk,wr;
   input [31:0] wdata;
   input [14:0] addr;
   output [31:0] rdata;

   reg [31:0] ram[32767:0]

   always@(posedge clk)
      if(wr)
         ramp[addr] <= wdata;
      else

   assign rdata =ram [addr];
endmodule
```
5.7
```
module 32_RAM(clk,wr,addr,data);
   input clk,wr;
   inout [31:0] wdata;
   inout [14:0] addr;

   reg [31:0] ram[32767:0]

   always@(posedge clk)
      if(wr)
         ramp[addr] <= wdata;
      else
         data ram[addr]
   assign rdata =ram [addr];
endmodule
```
5.11  
```
module fsm(clk,rst_n,sel.hready,write,burst,resp_ok)
   input clk,rst_n,sel,hready,write,burst,resp_ok;
   parameter Reset=3'b000;
   parmeter Idle=3'b001;
   parmeter Addr=3'b010;
   parmeter Write=3'b011;
   parmeter Read=3'b100;
   parmeter BurstWrite=3'b101;
   parmeter BurstRead=3'b110;
   parmeter Resp=3'b111;

   reg [2:0] next_state.current_state;
   always@(posedge clk or negedge rst_n)
      if(!rst_n)
         current_state <= Reset;
      else
         current_state <= next_state;

   always@(rst_n or sel or hready or wirte orburst or resp_ok)
      case(current_state)
         Reset: if(rst_n) next_state =Idle;
         Idle: if(sel&&hready) next_state = Addr;
         Addr: if(write&&burst) next_state = Burstread;
            else if(!write&&burst) next_state = burstread;
            else if(!write&&burst) next_state = Read;
            else next_state = Write;
            ......

endmodule
```
5.15

## 行为级仿真模型建模
### 概述
verilog提供的时序控制语句主要有3种：延迟控制语句，事件控制语句和条件等待语句。

### 仿真时间和时序控制
事件控制语句指利用语法@()进行描述，@后面的括号里包含需要的语句

### 仿真模型建模实例
1. 时钟发生器
2. 简单的仿真环境
