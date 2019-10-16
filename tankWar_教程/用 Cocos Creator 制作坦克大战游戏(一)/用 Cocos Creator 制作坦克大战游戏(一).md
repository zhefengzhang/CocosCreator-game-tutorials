# 用 Cocos Creator 制作坦克大战游戏（一）



## *前言*

欢迎大家到[CocosCreator](https://discuss.cocos2d-x.org/)论坛发帖，将你在开发过程中遇到的任何问题发出来与大家一起讨论。本篇文章不教学任何代码的编辑，而是带领大家学习制作TiledMap资源，因为这是制作坦克大战游戏的关键。开始学习教程之前，请准备好开发环境。

如果你在我们的教程中遇到麻烦，请学习一下文档：

- 准备开发环境
  - [Cocos Creator 2.1.2](http://cocos2d-x.org/filedown/CocosCreator_v2.1.2_win)
  - [Tiled Map Editor 0.10.2](https://github.com/Jno1995/TiledMapEditor)
- [文档](https://docs.cocos.com/creator/manual/en/)
  - [TiledMap Component Reference](https://docs.cocos.com/creator/manual/en/components/tiledmap.html?h=tiledmap)

------



## *我们开始吧！*

目前CocosCreator最新版本只支持1.0.0版本及以下版本的TiledMap资源。

### 1、了解并使用TiledMapEditor

当你下载并解压我提供的TiledMapEditor安装包之后，请找到`tiled.exe`应用程序，双击它。这时候在windows系统下会出现如下界面：

![1568103250049](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568103250049.png)

选择菜单File出现如下菜单选项：

![1568103350497](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568103350497.png)

选择New...出现如下窗口：

![1568103544022](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568103544022.png)

我们解读一下该界面的各个属性的作用：

* Map
  * Orientation 
    * ![1568103811813](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568103811813.png)
    * Orthogonal:（90度角地图）可以用于RPG游戏地图，也可考虑用于类似超级玛丽一样的横版过关游戏
    * Isometric：（45度角）可用于RPG游戏地图，也可以考虑战棋类游戏 
    * Isometric（Staggered）：（45度交错）地图呈现为四边形，边界位置使用1/2的三角形地图块呈现
  * Tile layer format
    * ![1568104166126](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568104166126.png)
    * 图层保存格式：XML、Base64（无压缩、gzip、zlib）、CSV 
  * Tile render order
    * ![1568104441230](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568104441230.png)
    * 地图坐标方向：默认是Right Down（右 下）也就是说左上角为顶点向右为X轴，向下为Y轴 
* Map size
  * ![1568104592244](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568104592244.png)
  * 地图大小，也就是创建的地图中拥有 Width * Height 个地图块 
* Tile size
  * ![1568104613897](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568104613897.png)
  * 块大小，此处对应的是像素点，也就是每个图块所占的宽高 

了解每个属性的作用之后，点击`OK`创建TMX地图资源。按住`Ctrl + S`保存资源，这时候我们将它命名为`tankWarMap0`。

我们继续为地图添加图块资源：

点击Tilesets进入图集管理窗口

![1568105273056](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568105273056.png)

点击New Tileset，出现如下窗口

![1568106338745](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568106338745.png)

* Name：
  * 图集名称
* Type：
  * Based  on Tileset Image
    * 基于图集本身尺寸的模式
  * Collection of Images
    * 可以导入任意图片
* Source：
  * 图集路径
* Use transparent color：
  * 将图集上的透明区域替换成指定颜色
* Tile width / Tile height：
  * 图块大小
* Margin：
  * 图块边缘像素填充
* Spacing：
  * 图块间隔像素填充

一切确定之后，点击`OK`,导入图集。

![1568107080376](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568107080376.png)

每一个图块，都有它对应的Tile ID，这对于判断图块的类型非常有用：

![1568108838000](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568108838000.png)

接着，我们得为地图添加Tile Layer和Object Layer。首先我们找到Tile Layers区域：

![1568107440350](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568107440350.png)

添加如下图所示的Tile Layer和Object Layer（这里要注意每个Layer的上下层级关系，建议与下图保持一致）：

![1568107563592](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568107563592.png)

为什么这里要注意上下层级关系呢？因为当TiledMap资源导入到CocosCreator编辑器中，并加入到场景中时，它的层级结构会出现颠倒：

![1568108084038](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568108084038.png)

并且在CocosCreator的UI系统中，下层节点会掩盖上层节点，所以我们需要注意这一点，避免出现问题。

选择如下图所示的区域，之后在layer画布中点击鼠标左键不放，然后拖动一段距离，之后松开。这样就完成了第一次的地图绘制：

![1568109324979](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568109324979.png)

最终，我的完成品是这样的：

![1568109516700](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568109516700.png)

![1568109550756](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568109550756.png)

关于TiledMapEditor的基础操作基本介绍完了，其它的可以自行探索。

---



### 2、在CocosCreator中使用TiledMap资源

本节将指导大家导入TiledMap资源到CocosCreator中，以及熟悉CocosCreator的CCTiledMap组件。

#### 2.1、导入TileMap资源到CocosCreator中

找到已经保存在本地的TileMap资源：

![1568111157524](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568111157524.png)

全选它们，然后拖入CocosCreator编辑器的assets/res/maps目录下：

![1568111496212](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568111496212.png)

这样就成功导入资源了。

#### 2.2、让TiledMap资源在场景中显示

两种方式可以让TiledMap资源在场景中显示：

* 添加TiledMap组件，并将TiledMap资源的.tmx资源拖入到Tmx Asset属性框中：
  * ![1568113927803](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568113927803.png)
* 将TiledMap资源中的.tmx资源拖入到场景中：

以上两种方法最后都能正确加载并显示TiledMap资源，效果如下：

![1568114022613](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568114022613.png)

最后，我们需要将Canvas的尺寸调整为和TiledMap组件的尺寸一致，这样能够让游戏看起来更美观。

![1568114187166](https://github.com/Jno1995/CocosCreator-game-tutorials/blob/master/tankWar_%E6%95%99%E7%A8%8B/%E7%94%A8%20Cocos%20Creator%20%E5%88%B6%E4%BD%9C%E5%9D%A6%E5%85%8B%E5%A4%A7%E6%88%98%E6%B8%B8%E6%88%8F(%E4%B8%80)/images/1568114187166.png)

---

### 3、结尾

本篇教程是对坦克大战游戏教程的热身教程。当你熟练掌握TiledMapEditor之后，也就能够制作出很多有趣的地图了。

展示一下完整demo的效果图：

![](F:\TestDemo\GIF.gif)

---

谢谢大家，下面是完整项目的链接，请你使用CocosCreator2.1.2版本打开。

[Complete Demo](https://github.com/Jno1995/Tank-War)

