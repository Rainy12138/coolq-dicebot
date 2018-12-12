# DiceRobot kills you 3000
Just a simple dicebot for coolq in development.  
只是一个简单的酷Q骰子机器人。  
![image](/dicebot_test.gif)   

# 特性
* 所有的骰子指令支持多行输入。  
* 使用硬件随机器，如果硬件随机器不可用，则改用mt19937随机器。  
* 支持coc7的奖惩骰。  
* 骰子指令的头部.r可以任意填充空格，例如```      .    r     1d20```也是有效的。  
* 算式也可以在各个组成部分之间插入空格，例如```.r 1d20  +  4d6  +3```也可以。  
* 可以识别整数、小数、百分数，例如```123```，```123.45```，```123.45%```都是有效的。（当然，骰子个数和面数不可能是小数。）  

#安装
点击[下载cpk](https://github.com/decterous/CoolQDicebot/releases/latest)前往下载本骰子机器人最新cpk。  
点击[获取酷Q](https://cqp.cc/)前往酷Q官网下载酷Q。    
点击[酷Q wiki](https://d.cqp.me/Pro/%E6%96%B0%E6%89%8B%E4%B8%8A%E8%B7%AF)前往酷Qwiki了解如何使用酷Q以及插件如何安装。  
注意：该骰子机器人不会回应私聊消息。  
感谢@niunuinui 在文档制作上的帮助。

# 使用示范
## help
发送```.help```获取没啥用的帮助信息。
> 测试：```.help```

> DiceBot：
> ``` 
> DiceBot by dynilath v1.4.2
> 访问项目主页http://github.com/dynilath/CoolQDicebot
> 获得使用说明以及了解更多内容。
> ```

## 最简单的骰子
让我们先骰一个d20试试。  
> 测试：```.rd20```

> DiceBot：``` * 测试  掷骰: d20 = 20```

你只需要在开头写上```.r```再加上骰子（例如```d20```、```4d6```）。  
骰子的基本格式为```XdY```，```X```表示骰子个数，```Y```表示骰子面数。当然，你在TRPG规则书里肯定已经看过无数次了。  

这个结构也可以用下面的文字表示：  
``` . r [骰子个数]d[骰子面数]```
发送这个消息，骰子机器人就能识别你的消息并回复一个骰子结果。  

## 骰子描述
在骰子指令后面加上一些文本，可以作为描述。  
> 测试：```.rd20攻击```

> DiceBot：``` * 测试 攻击 掷骰: d20 = 6```

## 更多的骰子
有时候你会需要骰几种不同的骰子，可以发送如下信息。  
> 测试：```.rd20+d6+2d4```

> DiceBot：``` * 测试  掷骰: d20 + d6 + 2d4 = 20```

## 骰子机器人到底在说什么？
骰子机器人发送的信息组成结构如下：  
``` * [你的QQ昵称/群名片] [骰子描述] 掷骰: [骰子指令] = [结果]```  
群名片就是你使用骰子所在的群中你的群名片，如果是讨论组则使用昵称。  
骰子描述即你输入的骰子（例如```d20```、```4d6```）。  
结果即最终计算得到的数值。

## 我想知道4d6的每个d6各是多少
有的时候你可能会想要知道4d6里面每个骰子各是多少，这个时候使用```.rs```代替之前的```.r```即可。  
> 测试：```.rs4d6```

> DiceBot：``` * 测试  掷骰: 4d6 = (1 + 1 + 4 + 2) = 8```

这个时候骰子机器人发送的信息组成结构为：  
``` * [你的QQ昵称/群名片] [骰子描述] 掷骰: [骰子指令] = [骰子详细] = [结果]```  

## 我想双/三/四骰取高/低
你可以在骰子指令后加上```k[数值]```或者```kl[数值]```来只取部分结果。  
其中```k[数值]```表示保留较高结果，```kl[数值]```表示较低结果。  
下面的例子是骰4d6并保留3个较高的结果（即扔掉较低的那个）。  
> 测试：```.rs4d6k3```

> DiceBot：``` * 测试  掷骰: 4d6k3 = (5 + 1 + (1) + 1) = 7```  

## 一个一个地输入太麻烦了！
骰子机器人支持一次输入多行，如下所示：
> 测试：
> ```
> .r 1d20 + 1d6-3+4+11 破邪斩+猛力攻击
> .r 5d4 * 150%
> ```

> DiceBot：
> ```
>  * 测试 破邪斩+猛力攻击 掷骰: 1d20 + 1d6 - 3 + 4 + 11 = 37
>  * 测试  掷骰: 5d4 * 150% = 21
> ```

可能下面的场景你会经常遇到：  
> 测试：
> ```
> .r4d6k3 力量
> .r4d6k3 敏捷
> .r4d6k3 体质
> .r4d6k3 智力
> .r4d6k3 感知
> .r4d6k3 魅力
> ```

> DiceBot：
> ```
>  * 测试 力量 掷骰: 4d6k3 = 10
>  * 测试 敏捷 掷骰: 4d6k3 = 15
>  * 测试 体质 掷骰: 4d6k3 = 14
>  * 测试 智力 掷骰: 4d6k3 = 12
>  * 测试 感知 掷骰: 4d6k3 = 9
>  * 测试 魅力 掷骰: 4d6k3 = 13
> ```

输出的顺序完全按照你的输入顺序，并且如果存在不符合规范的行，能够单独忽略。  
> 测试：
> ```
> .r4d6k3 力量
> 这行是来捣乱的
> .r4d6k3 敏捷
> ```

> DiceBot：
> ```
>  * 测试 力量 掷骰: 4d6k3 = 11
>  * 测试 敏捷 掷骰: 4d6k3 = 12
> ```  

## 我想能直接计算一部分后续加值

不用担心，骰子机器人是支持算式的。  
> 测试：```.rs(((4d6+3)/2+2d20)+4*1d6)*150%```

> DiceBot：``` * 测试  掷骰: (((4d6 + 3) / 2 + 2d20) + 4 * 1d6) * 150% = ((((2 + 1 + 5 + 4) + 3) / 2 + (11 + 12)) + 4 * (4)) * 150% = 69.75```  

当然，如果你的算式输入格式有问题，多余的部分会被识别成骰子描述。  
> 测试：```.rs4d6+(((4d6+3)/2+2d20)+4*1d6```

> DiceBot：``` * 测试 +(((4d6+3)/2+2d20)+4*1d6 掷骰: 4d6 = (6 + 3 + 2 + 4) = 15```  

## 我不想每次都改群名片
使用```.n```指令来指定一个仅在骰子机器人的回复文本中使用的名字。  
这段文本会代替之前所述的```[你的QQ昵称/群名片]```部分  
> 测试：```.n菜鸟PC```

> DiceBot：``` * 测试 的新名字是 菜鸟PC```  

在这之后使用骰子指令时，昵称部分会使用这个名字。  
> 测试：```.r4d6k3 力量```

> DiceBot：``` * 菜鸟PC 力量 掷骰: 4d6k3 = 7```  

除此之外，你也可以使用```.ns```来更改昵称，这个时候骰子机器人不会回复消息。  
> 测试：
> ```
> .ns 迷诱魔
> .r 1d20+20
> .ns 反pal魅魔
> .r 1d20+24破善斩
> ```

> DiceBot：
> ```
>  * 迷诱魔  掷骰: 1d20 + 20 = 37
>  * 反pal魅魔 破善斩 掷骰: 1d20 + 24 = 41
> ```  

这个昵称在每个群/讨论组之间是独立的，在A群的设置不会影响在B群的状态。  
昵称保存在数据库中，关闭开启不会取消已经设置的昵称。  
如果需要维护这部分内容，骰子机器人使用sqlite3数据库。在插件目录下可以找到.db文件。  

## 我是一个coc7版玩家
骰子机器人提供了coc定制的骰子。使用指令为```.c```。  
> 测试：```.c图书馆利用```  
> DiceBot：``` * 反pal魅魔 图书馆利用 掷骰: d100 = 11```  

除此之外，骰子机器人内置了coc7版的奖惩骰。 
使用```b[数值]```来产生奖励骰。
> 测试：```.cb2斗殴(65)```

> DiceBot：``` * 反pal魅魔 斗殴(65) 掷骰: d100b2 = [(10) + 9 + (9)] [0] = 90```  

使用```p[数值]```来产生惩罚骰。
> 测试：```.cp2闪避(50)```

> DiceBot：``` * 反pal魅魔 闪避(50) 掷骰: d100p2 = [(1) + 7 + (7)] [0] = 70``` 

可以自动计算奖惩相抵。
> 测试：```.cp5b5p2b3奖罚抵消```  
> DiceBot：``` * 反pal魅魔 奖罚抵消 掷骰: d100p5b5p2b3 = d100b1 = [0 + (1)] [7] = 7```  

## 手动骰子
手动骰子会产生一些会保存在数据库的骰子数据。  
你可以使用指令操作这些骰子。如同它们真的在那里。
可以使用的指令如下：

* 指令```.h``` ：产生手动骰子，后接骰子，这里不支持算式。
* 指令```.hr```：骰指定骰子，后接骰子序号。
* 指令```.hk```：消灭指定骰子，后接骰子序号。
* 指令```.hka```：清空手动骰子。

> 测试：
> ```
> .ns手动骰子测试
> .h4d6+2d8找几个骰子
> .hr4重骰第四个
> .hk5杀掉第五个
> .ha2d6增加两个
> .hka全杀掉
> .hr4
> .ha1d4
> ```

> DiceBot：
> ```
> * 手动骰子测试 找几个骰子 在桌上放了这些骰子: 4d6+2d8 当前状态: 3(6) + 6(6) + 4(6) + 4(6) + 5(8) + 4(8) = 26
>  * 手动骰子测试 重骰第四个 重骰桌上的第 4 个骰子 当前状态: 3(6) + 6(6) + 4(6) + 1(6) + 5(8) + 4(8) = 23
>  * 手动骰子测试 杀掉第五个 杀死桌上的第 5 个骰子 当前状态: 3(6) + 6(6) + 4(6) + 1(6) + 4(8) = 18
>  * 手动骰子测试 增加两个 在桌上增加了这些骰子: 2d6 当前状态: 3(6) + 6(6) + 4(6) + 1(6) + 4(8) + 2(6) + 2(6) = 22
>  * 手动骰子测试 全杀掉 杀掉了所有的骰子 当前状态: 没有骰子了
>  * 手动骰子测试  重骰桌上的第 4 个骰子 当前状态: 没有骰子了
>  * 手动骰子测试  在桌上增加了这些骰子: 1d4 当前状态: 2(4) = 2
> ```

# 其他的注意事项 

* 数字和骰子指令中是禁止空格的，例如```4d6```是不能写作```4 d 6```的，```100%```不能写作```1 0 0%```，这里被空格隔开的部分会被识别成指令中断，作为备注信息输出。  
* 没有任何计算时是不会输出的，例如```.r```，```.r  ```，```.r () ```都不会有输出结果，无论是否有备注信息。    
* 骰子能自动识别指令断点，例如输入``` .r 1d20 ++++```，机器人会将```++++```识别为骰子备注信息，并依此正常输出结果。这是为了增强骰子说明文本自由性。  
