---
title: Python每日练习
date: 2023-11-01 14:34:59
tags: 
    - 学习 
    - 代码
mathjax: ture
cover: /img/Python.jpg
categories: 学习
---
# 2023.11.1练习
## 问题1：
编写一个程序，要求用户输入一个正整数，然后计算该整数的阶乘并输出结果。阶乘是指将一个整数与小于它的所有正整数相乘的结果。例如，5的阶乘是5 * 4 * 3 * 2 * 1 = 120。

## 要求：
* 提示用户输入一个正整数。
* 检查用户输入是否是正整数，如果不是，显示错误消息并要求重新输入。
* 计算输入整数的阶乘。
* 输出计算结果。
```
#提示用户输入
num = input("请阁下输入一个正整数：") 

#判断用户输入是否是正整数
if num.isdigit(): 
   num = int(num)
   if num > 0:
      print(f"{num}是一个正整数")
   else:
      print(f"{num}不是正整数，请阁下重新输入")
else:
   print(f"{num}不是正整数，请阁下重新输入") 

#计算整数的阶乘
result = 1
for i in range(1, num+1):
    result *= i
print(f"{num}的阶乘为:{result}")

```

## 问题2：
 编写一个Python程序，要求用户输入一个字符串，然后判断这个字符串是否是回文字符串。回文字符串是指正着读和倒着读都一样的字符串，例如 "level"、"radar" 和 "madam" 都是回文字符串。

## 要求：
* 提示用户输入一个字符串。
* 忽略字符串中的空格，标点符号和大小写（将所有字符转换为小写）。
* 判断输入的字符串是否是回文字符串。
* 输出相应的结果，指出是否是回文字符串。
```
import re

#提示用户输入
user_input = input("请阁下输入一个字符串：")

#移除空格，标点和大小写
user_input = user_input.replace(" ", "") #移除空格
user_input = re.sub(r'[^\w\s]','',user_input) #移除符号标点
user_input = user_input.lower() #转换为小写

#判断输入的字符是否是回文字符串
fan_input = user_input[::-1] #创建反向字符串
if fan_input == user_input: #判断是否是回文字符串
    print(f"恭喜阁下，{user_input}是回文字符串！")
else:
    print(f"很抱歉，{user_input}并不是回文字符串")
```

# 2023.11.5练习
## 问题1：
写一个Python程序，找出一个列表中的所有奇数，并将它们存储在一个新的列表中。

## 要求：
* 创建一个函数，该函数接受一个整数列表作为参数。
* 函数应该返回一个新的列表，其中包含原列表中的所有奇数。
* 不要使用内置的filter函数或列表解析来完成任务。
```
def find_odd_numbers(input_list): #定义奇数函数
   odd_numbers = [] #形成一个列表
   input_list = input_list.split(",") #对列表进行切片
   input_list = [int(num.strip()) for num in input_list] #检查奇数
   input_list = [int(num_str.strip()) for num_str in input_list]  # 更改变量名

   for num in input_list: #遍历列表
      if num % 2 != 0:
         odd_numbers.append(num)
         
   return odd_numbers

user_input = input("请阁下输入一串列表(用，隔开): ")
result = find_odd_numbers(user_input)
print("奇数列表：", result)
```

## 问题2：
编写一个Python程序，计算斐波那契数列的第n个数字，其中n是非负整数。  
斐波那契数列的定义如下：  
1.第0个和第1个数字分别为0和1。  
2.从第2个数字开始，每个数字都是前两个数字之和

## 要求：
* 创建一个函数，接受一个非负整数n作为参数。
* 函数应该返回斐波那契数列的第n个数字。
* 请使用递归方式来解决这个问题。
```
#定义斐波那契数列的函数
def fibonacci(n):
   if n <= 0:
      return 0
   elif n == 1:
      return 1
   else:
      return fibonacci(n-1) + fibonacci(n-2)

#提示用户输入
user_input = input("请阁下输入一个非负整数")

#测试用户输入的是否是一个非负整数
try:
   user_input = int(user_input)
   if user_input < 0:
    print("让你打非负整数你不听,你XX!")
   else:
    result =  fibonacci(user_input)
except ValueError:
    print("输入什么玩意儿，让你输入一个非负整数")

```

# 2023.11.6练习
## 问题1：
猜数字游戏
## 要求：
编写一个Python程序，实现一个简单的猜数字游戏。程序随机生成一个1到100之间的整数，然后要求玩家猜这个数字，直到玩家猜中为止。程序需要提供反馈，告诉玩家他们的猜测是太高还是太低。最后，当玩家猜中数字时，显示猜测次数和祝贺消息。
```
import random
def guess_num():
   real_num = random.randint(1,100)
   attempts = 0

   while True:
      user_num = int(input("请猜测一下目标数字为(在1-100间选择)："))
      attempts += 1

      if user_num < real_num:
         print("结果与猜测不符，有点小，请再试一次")
      elif user_num > real_num:
         print("结果与猜测不符，有点大，请再试一次")
      else:
         print(f"恭喜阁下猜中了！目标数字为{real_num}，与阁下猜测的{user_num}完全一致！您真是一个小天才！")
         break

guess_num()
```

## 问题2：
查找最大元素
## 要求
编写一个Python函数，接受一个包含整数的列表作为参数，然后找到列表中的最大元素，并返回该最大元素的值。
```
def find_max_element(lst): # 初始化最大元素为列表的第一个元素
    max_element = lst[0]

    # 使用循环遍历列表中的每个元素
    for num in lst:
        # 如果当前元素比最大元素大，更新最大元素的值
        if num > max_element:
            max_element = num

    # 返回最大元素的值
    return max_element

# 示例使用
numbers = [12, 45, 62, 88, 34, 98, 75]
result = find_max_element(numbers)
print(f"列表中的最大元素是 {result}")
``` 

# 2023.11.12练习
## 问题1：简单的购物清单
## 要求：
1. 初始化一个空的购物清单。
2. 提示用户选择操作：添加商品、显示购物清单或退出。
3. 如果用户选择添加商品，程序应该提示用户输入商品名称和价格，然后将商品添加到购物清单。
4. 如果用户选择显示购物清单，程序应该输出当前购物清单中的所有商品及其总价格。
5. 如果用户选择退出，程序应该结束运行。
6. 在每次循环后，再次显示操作选项。
```
import random

def menu():
   print("欢迎使用购物清单程序!\n操作选项：\n1. 添加商品\n2. 显示购物清单\n3. 退出")

def add(shopping_list):
   name = input("请输入商品的名称：")
   price = input("请输入商品的价格：")
   shopping_list[name] = price
   print(f"{name}已添加至购物车 \n ")

def display(shopping_list):
   if not shopping_list:
      print("购物车竟然是空的！再忙，也记得买点什么犒劳下自己")
   else:
      print("当前购物清单：")
      for name, price in shopping_list.items():
         print(f" {name}: {price}")
      total = sum(shopping_list.values())
      print(f"总价格为：{total} \n")

def main():
    shopping_list = {}
    while True:
        menu()
        choice = input("请选择操作 (1/2/3): ")

        if choice == '1':
            add(shopping_list)
        elif choice == '2':
            display(shopping_list)
        elif choice == '3':
            print("退出也没有，摇一摇等下又见面了")
            break
        else:
            print("你在说什么？ \n")

if __name__ == "__main__":
    main()
```

# 2023.12.20练习
## 问题1：猜单词游戏
## 要求：
1. 使用一个包含多个单词的列表作为单词库。
2. 在游戏开始时，随机选择一个单词作为目标单词。
3. 显示一个由下划线组成的部分单词，初始时下划线的位置与目标单词相对应。
4. 允许玩家猜测字母，显示已经猜对的字母，并更新部分单词的显示。
5. 显示玩家已经猜过的字母列表。
6. 如果玩家在规定次数内猜对了整个单词，显示祝贺消息。如果猜错了6次，显示失败消息。

```
import random

# 创建词库
def choose_word():
    word_list = ["python", "programming", "challenge", "coding", "computer"]
    return random.choice(word_list)

# 显示部分单词
def display_partial_word(word, guessed_letters):
    partial_word = ""   # 初始化字符串为空
    for letter in word:   # 遍历目标单词的每个字符
        if letter in guessed_letters: # 如果字母已经在已猜过的字母列表中
            partial_word += letter # 将字母添加到部分单词中
        else:
            partial_word += "_"  # 否则，用下划线代替未猜对的字母
    return partial_word

# 游戏主循环
def main():
    target_word = choose_word()
    guessed_letters = []
    max_attempts = 6 #最大猜测次数
    attempts = 0 #初始值

    print("欢迎来到猜字母游戏!")
    print(display_partial_word(target_word, guessed_letters))

    while True:
        guess = input("猜一个字母: ").lower()

        if len(guess) != 1 or not guess.isalpha():
            print("请输入一个有效的字母。")
            continue

        if guess in guessed_letters:
            print("你已经猜过这个字母了。")
            continue

        guessed_letters.append(guess)

        if guess not in target_word:
            attempts += 1
            print(f"猜错了！还剩余 {max_attempts - attempts} 次机会。")

        partial_word = display_partial_word(target_word, guessed_letters)
        print(partial_word)

        if "_" not in partial_word:
            print("恭喜你，你猜对了！")
            break

        if attempts == max_attempts:
            print(f"很遗憾，你没有在规定次数内猜对。正确答案是: {target_word}")
            break

if __name__ == "__main__":
    main()

```