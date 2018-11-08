# 首先解释一下什么是IO类游戏
目前游戏市场和游戏媒体公认最有前途的游戏类型就是IO类游戏，原型是[《Slither.io》](http://slither.io/)和[《Agar.io》](http://agar.io/)。
##特点
- **网络游戏。**io游戏的所有特性必须在能和其他玩家产生交互的情况下才会产生乐趣。单机的io游戏没有任何意义。

- **多人即时对战。**这里的“多人”通常指多于一百人，主流io游戏的单服务器在线人数常常超过万人。支撑这种数量级的同时在线就够困难了，再加上要处理即时对战，对程序员来说是相当大程度的挑战。

- **简单的成长系统。**在早期的io游戏中，成长到极限（理论上来说没有极限，实际上到达某个临界点后就极难再成长了）需要的时间不会超过半小时。成长有两种途径：一，获取资源；二，杀死对手。“获取资源”在很多游戏中是控制玩家成长速度，增加游戏时间的手段。而在所有的io游戏中，这个过程都极为简单而快速。

- **即开即玩。**死亡后马上复活。没有永久的成长系统，退出游戏后一切清零。

- **战力即束缚。**战力越强的单位移动速度会越慢，给了弱小单位理论上的发展空间。当然，实际情况会很复杂。有可能出现隐藏战力引诱对手，然后瞬间提升战力杀死对手的策略。

- **小地图。**在玩家之间创造不停歇的相互冲突。

IO类游戏是不可能直接抄袭的，因为可以抄的别人早就抄了个光光。但是可以在这个类型上面换一种玩法，比如跑酷 + IO。IO类型的游戏有一个运营特点，就是日活（每日用户活跃量）非常高，也就是辛辛苦苦导的量不怎么会浪费掉。

# 以上是游戏设计的知识普及，接下来介绍这个项目：
<img src="http://forum.cocos.com/uploads/default/original/2X/5/5bc223ed980222c03dbf2930784b128948dca606.png" width="690" height="411">

#[项目预览地址](https://wubuzi.github.io/slitherIO/)
玩法是单击移动，双击加速移动。

#[源码地址（是整个工程，可以用cocos creator直接打开）](https://github.com/WuBuzi/slitherIO)
还是处于开发阶段，**并且已经弃置**，我试了下，发现这样的游戏对技术要求才是最最高的，因为前端本身就是一个问题，市面上火爆的IO类游戏基本都是用unity做的，我这个是用creator做的，所以我弃置了。因为在手机的网页上面玩家多起来真的跑不动。（主要原因我没怎么用心做，because<img src="http://forum.cocos.com/uploads/default/original/2X/6/608f433c600c19ec063f1c7d2dd479fcbef3f5e5.png" width="201" height="97">被这本书祸害比较重）


###不说这些了，来研究研究技术吧。
这样的游戏前端实现就是那个样子，然后就做同步，同步的做法就是两种

* 服务器控制同步。所有同步逻辑放在服务器上面实现，优点是基本很难会有什么外挂。缺点是人多必炸，因为服务器做的事情太多，轻松超负荷，服务器性能不行的时候，玩家的数据都会出错，比如玩家冲了50块钱的元宝你把他钱扣了元宝没冲上试试。

* 客户端控制同步。同步逻辑实现放在客户端实现，优点是人多多到多少都是前端的性能问题，服务端只负责消息广播和消息转发，完全没有什么逻辑上的处理，人多少都不关服务器什么事情，客户端就算是一个屏幕有太多人，也只是卡，不会严重到冲50块元宝钱扣了元宝不见了。缺点是破解了客户端的代码，外挂就能模拟客户端的行为做事情，比如无限瞬移还是什么的。

##而我采用的方案就是第二种，客户端处理同步，思路就是玩家操控（点击屏幕的那些操作）的时候分发消息给其他客户端，自己地图产生食物的时候也会分发消息给其他客户端。
只是思路，具体实现还没实现，因为手贱，非要去用网易的那个新产品叫网易云信，折腾了半天才搞好账号登录和消息转发。要是直接用github上面的http免费服务器就没这档事情了。

_**目前项目可以单机跑，可以登录用设备ID登录账号，并且同步消息。然后就没有然后了，这种游戏单机是没法玩的，弃置。**_