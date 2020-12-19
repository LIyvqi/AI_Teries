# AI_Teries
这是一个自动下俄罗斯方块的小游戏  
作者：刘雨濠、李玉奇、张美涵、李宗显 机器学习小组  
本机环境：python3.7  pygame 1.9.6   
## 库安装：   
理论上来说，只有pygame是需要安装的   
pip install pygame==1.9.6   
如果安不上的话，可以试一下国内的豆瓣源   
pip install pygame -i https://pypi.douban.com/simple   
##  参考资料  
参考了已有的用pygame写的俄罗斯方块小游戏  
https://github.com/lovetianya/pygame-development/blob/master/els/run-this.py   
参考了第一次提出自动博弈的算法  
Fahey, Colin. Tetris ai, June 2003. URL http://www. colinfahey.com/tetris/tetris.html.  


## 文件说明   
font文件夹里面存的是字体，可以根据自己的需要换   
score.txt里面存的是每次的分数，主要是用来记录最高记录的  
The Game of Tetris in Machine Learning.pdf 是参考的关于俄罗斯方块的算法的综述  
程序说明.pdf是程序类、函数功能的说明  
俄罗斯方块.py是游戏的主要内容  
你可以clone下来这个仓库直接使用，按a进入或者退出AI模式   
mp4文件是程序运行效果的一个小例子  
## 程序说明  
代码的核心主要有三各类，分别是：  
Wall：实现程序的各个界面以及消除计分功能  
Brick：主要实现砖块的各个信息  
1、砖块的信息：名字、形态、颜色  
2、一行砖块填满的碰撞检测  
3、绘制当前方块和下一行方块  
4、方块的动作，左右移动和变形  
HouseWorker：控制器，来控制游戏不同状态的进程，包括开始游戏、暂停游戏、重新开始公能  
### Wall类的函数说明：  
draw_grids():画游戏背景方格  
draw_matrix():根据二维矩阵绘制已存在的格子  
remove_full_line():消除一行并计分  
show_text()：封装的写文字的函数  
draw_score():写分数  
showPause():暂停界面  
show_welcome():欢迎界面  
drawALL()封装的函数，用于绘制背景，分数，格子等  
drawNextBrick():绘制下一个方块  
getHeightScore():获取最高分  
writeHeightScore():写入最高分  
showAD():展示我组强烈的征婚内容
### Brick类的函数说明：  
SHAPES：所有方块的名字   
SHAPE_WITH_DIR：存储所有方块的所有形态  
shape：方块的名字  
center：方块的中心点  
dir：方块的形态  
color：方块的颜色  
__init__():构造函数，随机生成方块以及它的颜色、形态、中心点  
get_all_gridpos():根据中心坐标获取方块获取其它点的坐标  
conflict():碰撞检测，检测是否碰到边和底部  
rotate():方块变形  
left():方块左移  
right():方块右移  
draw():绘制当前方块  
drawNext():绘制下一个方块  
### HouseWorker类的函数说明：
start():开始游戏
pause():暂停游戏  
whenPause():暂停时运行的游戏程序  
whenNormal():正常运行时的游戏程序  
whenGameOver():结束运行时的游戏程序  
### RobotWorker 类函数及变量说明  
SHAPES: 所有方块的名字  
I、 J 等字母：记录字母对应方块的点集  
SHAPES_WITH_DIR: 简称与实际图形点集的对应  
center: 中心点坐标  
shape: 方块形状  
color: 方块颜色  
station: 当前状态 (方块的那种方式)  
matrix: 记录局面的矩阵  
get_all_gridpos(self, center,shape,dir): 返回此中心下该方块占据的位置  
conflict(self, center,matrix,shape,dir): 检验此方块位置是否合理，主要检测  
是否超出屏幕之外和占据的位置是否先前已被占据  
copyTheMatrix(self,screen_color_matrix): 复制原先的颜色矩阵  
getAllPossiblePos(self,thisShape = ’Z’): 获取所有可能的位置 (按照每一列，  
从上到下检测每一个位置，如果当前位置可以放置，而且下一个位置是不可  
以放置的，那么当前位置就是一个可能放置方块的位置。 for 循环每种形态)  
getLandingHeight(self,center): 获取中心点高度  
getErodedPieceCellsMetric(self,center,station): 获取消除的行数和自身贡献  
的方格数 (满一行之后，检测这一行的每一个坐标是否在方块的所有点的坐  
标矩阵之内。从下网上开始搜索，一但一行里面没有一个实心方格则跳出循  
环)  
getNewMatrix(self,center,station): 把可能的坐标位置放进去颜色矩阵，形  
成新的颜色矩阵  
getBoardRowTransitions(self,theNewmatrix): 获取行变换数  
getBoardColTransitions(self,theNewmatrix): 获取列变换数  
4getBoardBuriedHoles(self,theNewmatrix): 获取空洞数 (按照列开始检测，从  
上往下，碰到有实心方格把 colHoles 设为 0，继续往下，碰到空心方格则  
+1。每一列循环后加入到总的空洞数里)  
getBoardWells(self,theNewmatrix): 获取“井”的数量以及返回“井”数的  
连加数 (每一列从上往下开始检测，碰到空心方格而且两边是墙或者实心方  
格的时候，“井”深加 1，继续往下检测，再次碰到空心方格则“井”深加 1，  
若碰到实心方格则重新开始统计“井”深，并把当前“井”加入到总数)  
getPrioritySelection(self,point): 计算优先度函数  
evaluateFunction(self,point): 根据点的中心位置计算分数  
