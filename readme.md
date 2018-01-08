# Assembly Snake



## 1. 说明

### 简介

1. 游戏区域随机产生 " 食物 "
2. w、s、a、d 控制蛇上下左右移动
3. 吃掉食物， 蛇会在尾端多一节身体;  蛇头碰到蛇身, 游戏结束
4. 游戏过程中有《老司机带带我》的BGM





### 使用方法

1. 使用masm 汇编 snake.asm, 生成 snake.obj
2. 使用链接器 链接 snake.obj, 生成 snake.exe
3. 在dosbox下 进入 snake.exe 的文件目录, 输入 snake,即可游戏

   上述命令如下:

* > masm snake
  >
  > [回车]
  >
  > [回车]
  >
  > [回车]
  >
  > link snake
  >
  > [回车]
  >
  > [回车]
  >
  > [回车]
  >
  > snake







## 2. 游戏实现

### 子程序



* **display_welcome** :    显示欢迎界面

  > 入口参数: 无
  >
  > 出口参数: 无
  >
  > 作用: 显示欢迎界面
  >
  > 实现方法: 将欢迎界面上的字符 以及样式定义到 数据段里,
  >
  > ​                 通过一个两层循环将其直接写入显存位置

*  **display_welcome_choose** : 在 欢迎 界面进行选择, 输入 3: easy 2 : middle 1: hard 
   > 入口参数:
   >
   > 出口参数:
   >
   > 作用:
   >
   > 实现方法:

* **init_menu** : 显示游戏界面

  > 入口参数:无
  >
  > 出口参数:无
  >
  > 实现方法: 与display_welcome 相同

* **ingame**: 

  >入口参数:
  >
  >出口参数:
  >
  >作用:
  >
  >实现方法:

* **wait_keyboard**:  检测、读取键盘事件, 设置 snake 的移动方向( 0: up, 1: down, 2: left, 3: right )

  >入口参数: snake_dir[0]
  >
  >出口参数: snake_dir[0]
  >
  >实现方法: 使用int 16h 的01h 和 00h中断来读取键盘事.
  >
  >​                 如果有wsad 按下, 则根据当前的方向来设置新的方向.
  >
  >​                 规则是, 新的方向与旧的方向必须垂直

  ​

* **go_snake**: 移动 snake 的每一节的 坐标
  >入口参数: snake_dir[0]
  >
  >出口参数:
  >
  >实现方法:

* **draw_snake** : 在 snake 的可移动区域内显示 snake
  >入口参数:
  >
  >出口参数:
  >
  >作用:
  >
  >实现方法:

* **clear_tail** : 在屏幕上清除旧位置上的蛇尾
  >入口参数:
  >
  >出口参数:
  >
  >作用:
  >
  >实现方法:

* **food_create** : 在snake 的可移动区域(13 * 43 ) 内随机放置一个食物: 设置食物的row & col
  >入口参数:
  >
  >出口参数:
  >
  >作用:
  >
  >实现方法:

* **locate**: 由字符, 在游戏区域内的行数列数得到该字符在屏幕上的显存偏移量
  >入口参数:
  >
  >出口参数:
  >
  >作用:
  >
  >实现方法:

* **score_increase**: 更新玩家得分
  >入口参数:
  >
  >出口参数:
  >
  >作用:
  >
  >实现方法:




### Q & A

1. Q: snake 是如何在程序中表示的?

​       A: 程序在数据段中 声明了一个 546 个 字( 两个字节 ) 的空间: s_locate, 用来表示snake的坐标.

​           程序中蛇的移动区域为 13 行, 42列 ( 13*42 = 546 ), 表示的坐标 从 0 ~ 13 * 84 - 2.  

​           如果某个坐标的值 为1 , 说明该坐标上为空, 蛇可以移动, 食物可以防止到该坐标上. 

​           若该坐标的值为偶数, 表示这个位置上是 snake 的一部分, 其值为下一个蛇身的坐标.

​           蛇 尾坐标上的值为 2048. 这样, 用一个单向链表就能表示 一个 snake.

​           在 数据段 用snake_head[0] 记录了snake 的起始坐标 

2. Q: 





