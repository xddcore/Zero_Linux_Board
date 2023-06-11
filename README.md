<!--
 * @Author: Chengsen Dong 1034029664@qq.com
 * @Date: 2023-06-09 21:19:34
 * @LastEditors: Chengsen Dong 1034029664@qq.com
 * @LastEditTime: 2023-06-11 15:31:16
 * @FilePath: /Zero_Linux_Board/README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
# Zero_Linux_Board
A Linux Board(F1C200S, RP2040 Inside)

## 关于
本项目是xddcore同学在2023年6月2日启动的一个Linux开发板项目。

# 时间线记录

2023/06/02:项目启动

2023/06/03:项目思维导图绘制完成

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

>平衡美观和实用，预计推出三种外壳形式（得益于n*2mm亚克力外壳方案带来Z轴方向的积木特性）：    
1.透明探索款：收藏陈列。全封闭外壳，避免进灰，搭配上蓝色阻焊层&1u沉金&JLC高清丝印，主打一个精致和帅。    
2.基础款：一般开发应用。Type-C&TF Card接口，内部含电池槽&扬声器槽，主控散热片支持&顶板散热孔。    
3.工程款：火力全开开发应用，在基础款外壳的基础上，增加USB-A*2，4个按钮触发杆（分别是F1C200S复位按钮，F1C200S用户按钮，RP2040 Boot按钮，RP2040复位按钮），50P FPC扩展板固定孔（50P包含电源，RP2040的所有GPIO，F1C200S的部分核心外设IO）将赋予更多可能性（比如点个屏（B站小电视），点个摄像头（跑一下NCNN），etc…）。    

总之，生命不息，折腾不止！🐛
