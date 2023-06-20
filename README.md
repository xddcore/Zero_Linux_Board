<!--
 * @Author: Chengsen Dong 1034029664@qq.com
 * @Date: 2023-06-09 21:19:34
 * @LastEditors: Chengsen Dong 1034029664@qq.com
 * @LastEditTime: 2023-06-20 15:11:23
 * @FilePath: /Zero_Linux_Board/README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
# Zero_Linux_Board
A Linux Board (F1C200S, RP2040 Inside)

>在写此篇README之前，xdd同学抱着生怕各位看官复现过程中出问题的心态，于是这篇较为详细的README便产生了。

## 介绍
本项目是xddcore同学在2023年6月2日启动的一个Linux开发板项目。本项目旨在纪念学生时代的结束(从初二至今9年的电子编程折腾生涯)。同时，设计一块板子来满足一些需要Linux生态但是又不需要很强性能的场景。

## 特性
1. **紧凑的设计**。PCB尺寸`49mm*49mm*1.6mm`，带壳尺寸`59mm*59mm*24mm`。
2. **差不多性能**。内置全志F1C200S(`ARM9@400Mhz+`)和RP2040(`双Cortex M0+处理器核心，最高133MHz`)。
3. **方便的开发方式**。仅一个Type-C接口可完成对F1C200S和RP2040的开发。另外还可通过F1C200S直接对RP2040进行编程。
4. **充分的外设**。`USB Hub(USB2.0*2)`，`2.4 GHz WIFI`，`3W扬声器`，`锂电池充放电管理`，`MPU6050`等。
5. **扩展板支持**。RP2040GPIO全引出(除2个ADC引脚外)，F1C200S部分核心外设引出。在后期将支持`ISP屏幕/墨水屏➕摄像头➕麦克风一体化扩展板`。
6. **透明探索版**。外壳主体采用12块2mm透明亚克力拼装而成。

## 1. 复现指南

### 1.1 硬件

#### 1.1.1 核心板PCB
1. PCB尺寸:`49mm*49mm`，板厚1.6mm
2. PCB层数:`4层`
3. 电源线宽度`10mil`，信号线宽度`6mil`
4. **WIFI天线50Ω阻抗匹配**: 下单时选用嘉立创`JLC0461H-7628`层压结构，经过计算，天线走线宽度为`13.75mil`。
5. 最小孔径/外径选择: 下单时选用嘉立创`0.25mm(外径0.35/0.4)`
6. 大量封装采用0402，手焊推荐开钢网(节省成本可开小钢片)

#### 1.1.2 扩展板PCB

(待补充)

#### 1.1.3 其他硬件
1. 4 \*（M2螺丝+M2防滑螺母）。螺丝长度**需大于**`30mm`。
2. 锂电池尺寸**需小于**`50mm*50mm*8mm`，锂电池接口为`XH2.54`。
3. F1C200S散热片尺寸**需小于**`10mm*10mm*12mm`。







---
## 开发时间线记录(以下为流水账纪念，各位看官可以跳过)

2023/06/02:项目启动

2023/06/03:项目思维导图绘制完成
![正面](/img/Xmind.png)


2023/06/08:PCB绘制&渲染完成    
![正面](/img/Front_only_board.jpg)
![背面](/img/Back_only_board.jpg)

**与1英镑硬币的大小对比**
![正面](/img/Front_board_coin.jpg)
![背面](/img/Back_board_coin.jpg)

2023/06/09:PCB&SMT生产开始    
![背面](/img/PCB_SMT.jpeg)

2023/06/10:透明探索版外壳绘制&渲染完成  

> Note: 什么是透明探索版外壳? 用于收藏陈列的全封闭透明亚克力外壳。

![透明探索版正面1](/img/Front_Board_Explore_Shell_1.jpg)
![透明探索版正面2](/img/Front_Board_Explore_Shell_2.jpg)
![透明探索版正面3](/img/Front_Board_Explore_Shell_3.jpg)

![透明探索版背面1](/img/Back_Board_Explore_Shell_1.jpg)
![透明探索版背面2](/img/Back_Board_Explore_Shell_2.jpg)
![透明探索版背面3](/img/Back_Board_Explore_Shell_3.jpg)

2023/6/11: 提出关于外壳款式的构想

>平衡美观和实用，预计推出三种外壳形式（得益于n\*2mm亚克力外壳方案带来Z轴方向的积木特性）：    
1.**透明探索款**：收藏陈列。全封闭外壳，避免进灰，搭配上蓝色阻焊层&1u沉金&JLC高清丝印，主打一个精致和帅。    
2.**基础款**：一般开发应用。Type-C&TF Card接口，内部含电池槽&扬声器槽，主控散热片支持&顶板散热孔。    
3.**工程款**：火力全开开发应用，在**基础款外壳**的基础上，增加USB-A*2，4个按钮触发杆（分别是F1C200S复位按钮，F1C200S用户按钮，RP2040 Boot按钮，RP2040复位按钮），50P FPC扩展板固定孔（50P包含电源，RP2040的所有GPIO，F1C200S的部分核心外设IO）将赋予更多可能性（比如点个屏（B站小电视），点个摄像头（跑一下NCNN），etc…）。    

总之，生命不息，折腾不止！🐛

2023/06/11： 完成基础款外壳绘制

![基础版正面1](/img/Front_Board_Basic_Shell_1.jpeg)
![基础版正面2](/img/Front_Board_Basic_Shell_2.jpg)
![基础版正面3](/img/Front_Board_Basic_Shell_3.jpg)

2023/06/12： 利用autocad将3D dwg文件转为适用于生产的2D dwg文件
步骤:    
1. Ctrl+a:全选    

2. 依次输入命令 
m    
0,0,0   
0,0,1e99   

3. Ctrl+a:全选

4. 依次输入命令 
m    
0,0,1e99   
0,0,0  

![基础版DWG](/img/dwg_2d.jpeg)

2023/06/18: SMT&外壳加工完成
![基础版DWG](/img/PCB_Front.JPG)
![基础版DWG](/img/PCB_Back.JPG)

2023/06/21: 所有设备发往英国

