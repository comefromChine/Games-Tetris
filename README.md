# 俄罗斯方块游戏（SDL2+C++开发）

---

详细设计见我的知乎专栏 https://www.zhihu.com/people/caifei-yang/pins/posts

## 开发环境与依赖

 - IDE: Virtual Studio 2012
 - 依赖库: SDL2（下载地址: https://www.libsdl.org/download-2.0.php）
 - 开发语言: C++

## 实现效果图
![俄罗斯方块游戏实现效果图](C:\Users\yangcaifei\Desktop\res\2 - 副本.png)

## 公共引用文件描述
- res/目录下是程序中使用的资源文件，比如背景图片等；
- Defines.h文件中定义的是const values，比如游戏区域的位置等信息；
- Enums.h文件中定义的是enum const values，比如定义方向等；

## 类文件描述
1. Square类
定义一个类（Square）来表示我们的方块，由方块来构成我们的游戏块。这样一来，我们就能够很好地检测每个方块的碰撞，更重要的是，当我们的当前游戏块下落到游戏区域底部时，它就会成为方块的一部分，能够很好地被“删除”，并且上面的方块也能很好地向下移动。
2. GameBlock类
游戏块（GameBlock）由4个方块构成，我们只需要存储游戏块的中心、游戏块类型、4个方块以及方块纹理，就能够表示出游戏块。我们会根据游戏块的中心位置和类型来构造游戏块，在做旋转游戏块时，根据一个方块的中心来旋转游戏块。
3. Game类
游戏类Game负责游戏中游戏对象的管理，处理游戏逻辑部分，比如碰撞检测等。
当我们开始游戏时，我们将随机选择一个游戏块类型来作为焦点块，并再次随机选择一个游戏块类型作为下个块。每次我们焦点块改变时，我们需要选择另一个游戏块类型作为下一个游戏块。当焦点块不再移动时，我们需要将焦点块中的方块添加到已有方块的集合中（在游戏中我们使用vector来存储）。在游戏中我们还需要记录玩家的分数、游戏等级、下一个游戏块等信息，判断玩家玩游戏时是否Win or Fail？，更重要的是在游戏中做碰撞检测。
在做碰撞检测时我们需要检测游戏块是否与其它方块发生碰撞以及是否与游戏区域发生碰撞，当焦点块到达游戏区域的底部或者被方块给阻挡时，我们需要改变焦点块以及清除掉已完成的行，另外，我们的游戏块还能旋转，所以还需要检测游戏块旋转后是否与游戏区域、其它方块发生碰撞。
4. Window类
Window主要负责我们窗口的绘制、资源文件的加载、初始化我们的游戏对象（Game，Game类主要负责游戏中游戏对象的管理，处理游戏逻辑部分，比如碰撞检测等，暂时不用管）以及进入到窗口循环中来接收键盘事件、鼠标事件等。
在Window类中我们设计了Start方法，一旦调用该方法就会进入游戏循环，在循环中不断检测事件的发生、更新我们窗口中游戏资源的位置等信息以及将我们的游戏资源绘制到窗口中。