# J2ME
我很讨厌这门语言，虽然我现在还在用它开发者小游戏，每每提到这门语言大家都感觉使用它的人很低级，我也是这么想的。即使已经没有人使用这门语言了，但是我还是要将自己两年来对它的理解给大家共享出来，有理解不对的地方希望大家能提出。

## 背景
接触它是大二的时候，参加软件设计大赛，由于比较喜欢游戏，就用他开发了一个小游戏哈哈。结果还得了个二等奖。
当初参加软件设计大赛的时候已经有Android了，为什么不用Android开发游戏参赛呢，(⊙v⊙)嗯这个问题问得好，因为开发Android得有个Android的手机吧？可惜我没有，然后我就选择了它（J2me）开发。现在想想当初开发的游戏代码写的跟屎一样，乱七八糟的。即使现在还是那么的不堪入目。O(∩_∩)O哈哈~

## 应用
说到应用我发现除了我现在开发的IPTV游戏用到，还有一些机顶盒在使用，但是Android机顶盒要来了，这门技术真的要退出舞台了，我真的希望他能在别的领域还在用，这样我也能找个饭碗~~~~(>_<)~~~~ 陪伴自己两年的技术，必须好好吐槽一下，以上纯属吐槽！

## IPTV游戏开发
这就是我两年来干的工作，开发小游戏，适配全国的机顶盒，电信、广电，广电的盒子很难适配，早些年头的盒子就更能适配了），iptv游戏开发主要问题就是内存，最重要的问题也是内存，机顶盒的内存太小了，2M的内存，懂不懂就是OOM，还有jar包大小也要控制在2M内，

###内存控制
* 及时释放不在绘画的图片资源<br/>
* 尽量压缩jar大小，越小越好，（如果图片过多，建议使用图片服务器，从服务器读取图片）<br/>
* 对于大图，最好切成块状来加载，（分不同的步骤加载防止达到机顶盒的峰值导致OOM）

###闪屏处理
* canvas继承GameCanvas（建议使用）<br/>
* 自己new 一张图片来做双缓冲，（问题：new 出来的图片也会占用内存，容易OOM）

###游戏卡
* 优化代码，不在可视区域的图片不要绘制<br/>
* 代码中的计算量要少，本来机顶盒的运算性能又差，你每个坐标都要获取图片的宽高之类的来计算，（建议绘画之前就算好）<br/>
* 优化内存，<br/>
* 如果游戏中有很多小的图片，可以先new 一张图片，然后将小图都绘画在new出来的图片上，然后在将这张图片画上去，效果是一样的<br/>
* 低性能的盒子对于Sprite 的旋转的绘制特别慢，会卡到死得节奏<br/>
* 广电的盒子(很老的广电的盒子)不支持double类型，一说的不能用double，我就想吐槽了，不能用浮点数怎么开发好游戏，说多了都是泪啊，不过还好有大神写了一个工具类（MathFP）可以将整数先放大到亿倍在计算，计算后在相同的比例缩小，以至于相差不大（但是还是有相差的哦~~~~(>_<)~~~~ ）<br/>

###通信
* 有的盒子有个毛病，通信容易失败，我的处理是用递归算法去通信10次，直到通信成功后就返回，10次都不成功我就认定失败（哈哈）<br/>
* 如果遇到socket的通信，那就傻眼了，因为你不知道他什么时候给你返回结果啊，当你绘画的时候你一定要注意一定要等待他返回才去处理下面的逻辑，我的处理是使用 
```Java 
while(img!=null)
```
来卡死在这里等待结果返回才继续的（我觉得应该还有更好的额方法）

                                             今天先写到这。刚学会写README。哈哈








