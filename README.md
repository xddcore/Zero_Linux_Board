<!--
 * @Author: Chengsen Dong 1034029664@qq.com
 * @Date: 2023-06-09 21:19:34
 * @LastEditors: Chengsen Dong 1034029664@qq.com
 * @LastEditTime: 2023-08-31 16:49:50
 * @FilePath: /Zero_Linux_Board/README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
![基础版正面1](/img/Front_Board_Basic_Shell_1.jpeg)
# Zero Linux Board - 一个Linux小电脑。

>如果你喜欢此项目，欢迎为本项目点一个Star🌟

**核心板视频介绍**：[【自制】圆梦Linux小电脑](https://www.bilibili.com/video/BV1nN411S7BC)

**开源仓库介绍**：[【自制|开源】小白也可以轻松复现的Linux小电脑](https://www.bilibili.com/video/BV17u411V7ws/)

**透明探索版便携式小电脑**:[【自制】技术宅up耗时两个月，自制掌上触屏小电脑【硬核】【透明探索版】](https://www.bilibili.com/video/BV16h4y1Q7jv/)

## 介绍
本项目是xddcore同学在2023年6月2日启动的一个Linux开发板项目。本项目旨在纪念学生时代的结束(从初二至今9年的电子编程折腾生涯)。同时，设计一块板子来满足一些需要Linux生态但是又不需要很强性能的场景。

## 特性
1. **紧凑的设计**。PCB尺寸`49mm*49mm*1.6mm`，带壳尺寸`59mm*59mm*27mm`。
2. **差不多性能**。内置全志F1C200S(`ARM9@400Mhz+`)和RP2040(`双Cortex M0+处理器核心，最高133MHz`)。
3. **方便的开发方式**。仅一个Type-C接口可完成对F1C200S和RP2040的开发。另外还可通过F1C200S直接对RP2040进行编程。
4. **充分的外设**。`USB Hub(USB2.0*2)`，`2.4 GHz WIFI`，`3W扬声器`，`锂电池充放电管理`，`MPU6050`等。
5. **扩展板支持**。RP2040GPIO全引出(除2个ADC引脚外)，F1C200S部分核心外设引出。在后期将支持`ISP屏幕/墨水屏➕摄像头➕麦克风一体化扩展板`。
6. **透明探索版**。外壳主体采用12块2mm透明亚克力拼装而成。


- [Zero Linux Board - 一个Linux小电脑。](#)
  * [介绍](#介绍)
  * [特性](#特性)
  * [关于量产拼单活动](#关于量产拼单活动)
  * [目录结构](#0-目录结构)
  * [复现指南](#1-复现指南)
    + [1.1 硬件](#11-硬件)
      - [1.1.1 核心板PCB](#111-核心板pcb)
      - [1.1.2 扩展板PCB](#112-扩展板pcb)
      - [1.1.3 外壳](#113-外壳)
      - [1.1.4 其他硬件](#114-其他硬件)
      - [1.1.5 Type-C连接方式](#115-type-c连接方式)
      - [1.1.6 Type-C拨码开关配置](#116-type-c拨码开关配置)
    + [1.2 软件](#12-软件)
      - [1.2.1 驱动支持情况:](#121-驱动支持情况)
      - [1.2.2 快速验证](#122-快速验证)
      - [1.2.3 U-Boot](#123-u-boot)
      - [1.2.4 Linux主线(5.10.186)](#124-linux主线510186)
      - [1.2.5 使用Buildroot创建一个简易的rootfs来调试内核](#125-使用buildroot创建一个简易的rootfs来调试内核)
      - [1.2.6 使用debian来作为rootfs(apt install很舒服)](#126-使用debian来作为rootfsapt-install很舒服)
      - [1.2.7 debian-番外篇](#127-debian-番外篇)
    + [1.3 驱动开发](#13-驱动开发)
      - [1.3.1 Linux音频](#131-linux音频)
      - [1.3.2 ESP8266EX WIFI驱动](#132-esp8266ex-wifi驱动)
      - [1.3.3 MPU6050驱动](#133-mpu6050驱动)
      - [1.3.4 2.8寸ISP电容触摸屏驱动➕LVGL](#134-28寸isp电容触摸屏驱动lvgl)
      - [1.3.5 树莓派RP2040 USB驱动](#135-树莓派rp2040-usb驱动)
      - [1.3.6 语音识别与交互驱动](#136-语音识别与交互驱动)
    + [1.4 玩法推荐](#14-玩法)
      - [1.4.1 显示系统信息](#141-在isp屏幕上显示系统信息)
      - [1.4.2 显示图片](#142-在isp屏幕上显示图片)
      - [1.4.3 视频播放](#143-在isp屏幕上视频播放)
      - [1.4.4 usb摄像头](#144-usb摄像头)
      - [1.4.5 本地音乐播放](#145-本地音乐播放)
      - [1.4.6 网易云音乐播放音乐播放](#146-网易云音乐播放音乐播放)
      - [1.4.7 6轴陀螺仪](#147-6轴陀螺仪)
      - [1.4.8 lvgl](#148-lvgl)
      - [1.4.9 rp2040编程](#149-rp2040编程)
      - [1.4.10 智能助手chatgpt-35](#1410-智能助手chatgpt-35)
      - [1.4.11 登陆月球模拟器](#1411-登陆月球模拟器)
      - [1.4.12 nes模拟器](#1412-nes模拟器)
      - [1.4.13 opennna2.0神经网络框架](#1413-opennna20神经网络框架)
      - [1.4.14 搭建个人博客(typecho)](#1414-搭建个人博客typecho)
      - [1.4.15 内网穿透(rathole)](#1415-内网穿透rathole)
  * [1.5 一些图片](#15-一些图片)

---
## 关于量产拼单活动
xddcore zero Linux开发板软硬件全开源，大家可以选择自行复现。为了响应大家的购买需求，特地开启量产拼单活动。**本次量产拼单旨在集合大家的生产需求来拼单生产。这将显著显著降低大家制作开发板的成本，节约制作时间，并避免自行焊接带来问题。**      

**活动记录**      
230806：已成功拼单45块`Zero Linux Board`核心板，并全部成功交付。     
230817: 第二批量产拼单活动筹备进行中。本次将会拼单掌上小电脑套件(含核心板)。        

**活动参与方式**     

添加QQ群481227232，并填写支付问卷。

---

## 0. 目录结构

1. Hardware: 所有硬件相关资料


## 1. 复现指南

### 1.1 硬件

#### 1.1.1 核心板PCB
1. PCB尺寸:`49mm*49mm`，板厚`1.6mm`。
2. PCB层数:`4层`。
3. 电源线宽度`10mil`，信号线宽度`6mil`。
4. **WIFI天线50Ω阻抗匹配**: 下单时选用嘉立创`JLC0461H-7628`层压结构，经过计算，天线走线宽度为`13.75mil`。
5. 最小孔径/外径选择: 下单时选用嘉立创`0.25mm(外径0.35/0.4)`。
6. 大量封装采用`0402`，手焊推荐开钢网(节省成本可开小钢片)。

**硬件迭代**
|  版本号   |说明  |
|  ----  |---- |
| V1.0  | 完成初步设计 |
| V1.1  | 优化布线，引出IO。**Bug预警:已知原有TP5400升压电路10uH 0402电感功率较小，升压时会导致电感烧毁，请替换为额定电流大于1.5A的功率电感(TP5400最高输出1.5A(Vbat=3.8v))。** |
| V1.1-量产版本  | 优化布线，修复Bug。已稳定生产。 |

#### 1.1.2 扩展板PCB

|  名称   | 进度  | 说明  |
|  ----  | ---- | ---- |
| MINIPC 扩展板  | 已成功发布| 2.8寸ISP电容触摸屏,摄像头，麦克风，自定义按钮，全彩LED |
| 桌面机器人扩展板  | 已绘制完成，等待测试 | [稚晖君ElectronBot桌面机器人的Linux版本](https://github.com/xddcore/ElectronBot-Linux)|

![MINI_PC.JPG](/img/MINI_PC.JPG)

#### 1.1.3 外壳

##### 亚克力外壳
平衡美观和实用，预计推出两种亚克力外壳形式（得益于n\*2mm亚克力外壳方案带来Z轴方向的积木特性）：    
1. **透明探索款**：收藏陈列。全封闭外壳，避免进灰，搭配上蓝色阻焊层&1u沉金&JLC高清丝印，主打一个精致和帅。    
2. **基础款**：一般开发应用。Type-C&TF Card接口，内部含电池槽&扬声器槽，主控散热片支持&顶板散热孔。    

> Note:如果把亚克力外壳的图纸(.dwg文件)发到淘宝进行生产，某些厂家图纸尺寸单位可能识别成mm，导致外壳大小仅有5.9mm\*5.9mm。这时候需要提醒厂家外壳图纸单位为cm，外壳实际尺寸为5.9cm\*5.9cm。

关于亚克力外壳组装的说明(**非常重要**):    
在首次亚克力外壳设计中，采用了12块2mm厚度的亚克力。经过实际组装测试，亚克力高度缺少`2.8mm`,为了成功的组装采用如下方法修补:    

>方法一: 使用4颗2.8mm高度的M2防滑螺母垫高处理(M2防滑螺母安装在由下往上数的**第4块**亚克力上方)。效果图如下:    
![Acrylic](/img/Acrylic_assemble_fixup1.jpeg)


>方法二: 在生产亚克力时，多生产一块3mm厚度的亚克力。最后共计生产**12块2mm厚度亚克力和1块3mm厚度亚克力**。    
**12块2mm厚度亚克力dwg生产文件**:[点我下载生产文件](https://github.com/xddcore/Zero_Linux_Board/blob/main/1.Hardware/1.1Zero_Linux_Board/SHELL_BASIC/Shell-basic_2D.dwg)     
**1块3mm厚度亚克力dwg生产文件**:[点我下载生产文件](https://github.com/xddcore/Zero_Linux_Board/blob/main/1.Hardware/1.1Zero_Linux_Board/SHELL_BASIC/Shell-basic_2D_3mm.dwg)




##### 3D打印外壳

1. MINI PC外壳:尺寸`90mm` \* `70mm` \* `34mm`。内置2.8寸ISP电容触摸屏，麦克风，iphone扬声器等，可玩性极高。

**MINI PC外壳螺丝要求:**
1. 2 \* M3螺丝长度**小于**`16.1mm`，**大于**`12.1mm`。**经实际测试，推荐`16mm`**
2. 2 \* M3螺丝长度**小于**`29.1mm`，**大于**`25.1mm`。**经实际测试，推荐`29mm`**
3. 2 \* M2螺丝长度**小于**`4mm`，**大于**`2mm`。**经实际测试，推荐`4mm`**


#### 1.1.4 其他硬件
1. 4 \*（M2螺丝+M2防滑螺母）。螺丝长度**需大于**`27mm`，M2防滑螺母厚度2.8mm。
2. 锂电池尺寸**需小于**`50mm*50mm*8mm`，锂电池接口为`XH2.54`。锂电池接口极性如下图:
>![battery](/img/battery.jpeg)
3. `F1C200S`和`ESP8266EX`散热片尺寸**需小于**`10mm*10mm*12mm`。

#### 1.1.5 Type-C连接方式
|  连接方式   | 功能  |
|  ----  | ---- |
| 正插  | 连接USB(具体取决于拨码开关配置) |
| 反插  | 连接F1C200S的串口0(USB-TTL)，用于输出串口终端 |

#### 1.1.6 Type-C拨码开关配置

|  功能(1-4Bit)   | 1 Bit  | 2 Bit   |  3 Bit   |  4 Bit   |
|  ----  | ---- | ---- | ---- | ---- |
| **F1C200S**的USB与`USB HUB`和`Type—C`断开连接  | OFF | OFF | OFF | OFF |
| **F1C200S**的USB与`USB HUB`的上行端口连接  | OFF | ON | OFF | ON |
| **F1C200S**的USB与`Type—C`连接  | ON | OFF | ON | OFF |

|  功能(5-8Bit)   | 5 Bit  | 6 Bit   |  7 Bit   |  8 Bit   |
|  ----  | ---- | ---- | ---- | ---- |
| **RP2040**的USB与`USB HUB`和`Type—C`断开连接  | OFF | OFF | OFF | OFF |
| **RP2040**的USB与`USB HUB`的下行端口连接  | OFF | ON | OFF | ON |
| **RP2040**的USB与`Type—C`连接  | ON | OFF | ON | OFF |

**如何跃过USB HUB进行通信**
操作:    
将F1C200s和RP2040的拨码开关都跳到连接Type-c，然后Type-c反面供电(连接F1C200s的串口)。此时F1c200s和RP2040直接连接。

### 1.2 软件

在软件章节开始前，想说明本项目的RAM&Flash资源情况如下:
|     | F1C200S  | RP2040  |
|  ----  | ---- | ---- |
| RAM  | 64MB | 264KB |
| Flash  | 取决于SD卡容量(典型值32GB) | 16MB(SPI Flash) |


#### 1.2.1 驱动支持情况:
|   驱动名称  | 支持情况  | 
|  ----  | ---- | 
| 状态指示LED  |  ✅ |
| WIFI网卡(ESP8266EX)  | ✅(WIFI速度下载806KB/s,上传729KB/s。以上结果由`speedtest`得出，仅供参考)  |
| SD卡(SDIO)  | ✅ |
| 视频硬解码  | ❌(开发中) |
| 音频codec  | ✅ |
| MPU6050(IIO Device)  | ✅ |
| 2.8寸ISP电容触摸屏  | ✅  |
| USB OTG/Host/Device   | ✅ |
| USB HUB(键盘，U盘,摄像头)  | ✅ |
| F1C200S与RP2040的UART CDC通信；控制RP2040进入DFU模式，并对RP2040编程  | ✅ |

#### 1.2.2 快速验证

为了方便大家快速验证本开源项目，我提供以下SD卡镜像文件，大家可以以类似树莓派的玩法来游玩本开源项目。
|   镜像名称  | 下载链接  | 
|  ----  | ---- | 
| xddcore_zero_debian_v5.10.186_230715.img.gz  |  [点我查看](https://github.com/xddcore/Zero_Linux_Board/releases/tag/Debian_v5.10.186_230715) |
| xddcore_zero_debian_v5.10.186_230810_Tiny.img(**最新**)  |  [点我查看](https://github.com/xddcore/Zero_Linux_Board/releases/tag/Debian_v5.10.186_230810) |

开发板工具包路径(相关软件会放置在里面)：
> /xddcore_toolbox

#### 1.2.3 U-Boot

1. 获取U-Boot源码
```
git clone https://github.com/xddcore/u-boot.git -b zero-v2023.07-rc4
```

2. 安装交叉编译工具链
```
sudo apt install gcc-arm-linux-gnueabi
```

3. 拉取配置文件
```
make xddcore_zero_defconfig
```
>[点我查看性能测试结果](#)     

**超频配置(CPU 408Mhz->720Mhz,DDR 156Mhz)** [点我查看超频配置](https://github.com/xddcore/Zero_Linux_Board/releases/tag/U-Boot_OverClock) 
```
make xddcore_zero_overclock_defconfig
```
4. 编译U-Boot
```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- -j4
```

5. 写入U-Boot至SD卡(假如为/dev/sdb)
> Note: SD卡在写入前请格式化为NTFS，数据无价，格式化前请做好数据备份。
```
sudo dd if=u-boot-sunxi-with-spl.bin of=/dev/sdb bs=1024 seek=8
```

6. 验证烧写结果,通过`gparted`软件查看。
```
sudo apt install gparted
```
7. 将SD卡插入Zero核心板背面的SD卡自弹插座中

8. 连接Type-C线缆(注意反面插入为USB-TTL功能)

9. 使用终端软件连接串口(波特率115200)
>xddcore同学在此使用的是Termius，大家可以选择自己喜欢的终端软件

![U-Boot](/img/uboot.jpeg)

在此，我们可以看到U-boot成功在我们的板子上跑起来了。

#### 1.2.4 Linux主线(5.10.186)
1. 获取Linux内核源码
>长期支持版本: 6.1.36(因为内核逐渐向设备树方向发展，API换了不少(也删了不少)，啥驱动都得自己折腾)
```
git clone https://github.com/xddcore/linux.git -b zero-v6.1.36
```
>长期支持版本: 5.10.186(驱动丰富)
```
git clone https://github.com/xddcore/linux.git -b zero-v5.10.186-codec
```
在此我们使用`v5.10.186内核`进行接下来的开发。

2. 拉取内核配置
```
make ARCH=arm xddcore_zero_defconfig 
```

3. 编译内核
```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- -j4
```

4.将arch/arm/boot/zImage和dtb移入SD卡的FAT16分区

#### 1.2.5 使用Buildroot创建一个简易的rootfs来调试内核

1. 拉取Buildroot源码
```
git clone https://github.com/xddcore/buildroot.git -b zero-v2023.05
```

2. 拉取配置
```
make xddcore_zero_defconfig 
```

3. 使busybox支持`depmod``

```
sudo make busybox-menuconfig
Linux Module Utilities-> 选中depmod模块
```

4. `ssh`支持
```
sudo make menuconfig
Networking applications->Openssh，dhcpcd选中

Networking applications->
wireguard tools, 
wireless-regdb,
wireless tools(install shared library), 
wpa_supplicant,
wpan-tools,
xinetd,
xl2tp选中
```
5. 编译
```
sudo make busybox

sudo make -j4
```

6. 将rootfs放入EXT4分区

7. 将sd卡插入Zero

8. 串口终端波特率115200，用户名root，密码123456.至此根文件系统收工。

**如果启动的时候，console有如下报错:**

>can't open /dev/console: Permission denied 权限不足，是因为移动rootfs的时候rootfs被虚拟机用户所属，

**解决方案**:把所有文件所有者切回root

```
chown root * -R
```



#### 1.2.6 使用debian来作为rootfs(apt install很舒服)
1. 安装工具
```
sudo apt install qemu-user-static -y
sudo apt install debootstrap -y
```

2. 构建rootfs
```
sudo debootstrap --foreign --verbose --arch=armel  buster rootfs 

#如果梯子不太好用，也可以试试华为云的镜像
sudo debootstrap --foreign --verbose --arch=armel  buster rootfs http://mirrors.huaweicloud.com/debian/
```

3. 挂载
>此步坑点 apple m1 pro的pd虚拟机不支持arm 32bit(qemu)，换x86/x64即可解决。
```
cd rootfs
sudo mount --bind /dev dev/
sudo mount --bind /sys sys/
sudo mount --bind /proc proc/
sudo mount --bind /dev/pts dev/pts/
cd ..
sudo cp /usr/bin/qemu-arm-static rootfs/usr/bin/
sudo chmod +x rootfs/usr/bin/qemu-arm-static
sudo LC_ALL=C LANGUAGE=C LANG=C chroot rootfs /debootstrap/debootstrap --second-stage --verbose
sudo LC_ALL=C LANGUAGE=C LANG=C chroot rootfs
```

4. 预先安装一些软件(实现Zero板子的自力更生)
```
#网络
apt-get install wpasupplicant #安装WIFI配置相关的组件
apt-get install net-tools     #安装网络基础组件、如使用ifconfig等
apt-get install udhcpc        #当wifi连接成功后，需要用这个组件去获取IP地址


## 其他组件
apt-get install wireless-tools 
apt install sudo vim openssh-server htop
apt install pciutils usbutils acpi
```

5. 配置账号
```
passwd root
123456
```

6. 修改主机名
```
HOSTNAME=xddcore_zero(替换为你自己的主机名)
echo $HOSTNAME > /etc/hostname
sed -i '/localhost/s/$/\t'"$HOSTNAME"'/g' /etc/hosts
```

7. 允许root用户通过ssh登陆(只有一个root用户，所以这步非常重要，不然root无法通过ssh登陆)
```
vim /etc/ssh/sshd_config

在里面添加

PermitRootLogin yes
```

8. 退出rootfs，打包rootfs
```
exit  #退出chroot
rm rootfs/usr/bin/qemu-arm-static

cd rootfs
sudo umount   dev/pts/
sudo umount   dev/
sudo umount   sys/
sudo umount   proc/
sudo umount   dev/pts/

#打包文件(此时pwd在rootfs里面)
tar cvf ../rootfs.tar .    
```

9. 将rootfs解压到sd卡的ext4(rootfs)中

10. **启动后，通过串口命令行手动配网**

11. 安装WiFi驱动
```
insmod esp8089-spi.ko
```

12. 启动wlan0无线网卡
```
ifconfig wlan0 up
```

13. 新建wpa_supplicant配置文件(只需要进行一次)
```
vim /etc/wpa_supplicant/wpa_supplicant.conf

假如我有一个ssid为GL-MT1300-52d的无密码Wi-Fi。
填入以下内容:
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=CN

network={
  ssid="GL-MT1300-52d"
  key_mgmt=NONE
}


有密码的WIFI
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=CN

network={
    ssid="MyWifiNetwork"
    psk="MyPassword"
    key_mgmt=WPA-PSK #WPA2-PSK
    pairwise=CCMP
    group=CCMP
}

```

14. 连接WIFI
```
wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf 
```

15. 使用dhcp获取ip地址
```
udhcpc -i wlan0
```

16. 此时，板子成功上网了，使用ssh连接，Enjoy it!

17. 如果修改配置文件后，需要重启服务
```
pkill wpa_supplicant

sudo systemctl restart wpa_supplicant
```


#### 1.2.7 debian-番外篇
1. SWAP分区
64MB内存对于一台Linux小电脑来说，非常小。为了防止内存溢出，此处在sd卡中建立swap分区。
**使用以下命令创建512MB Swap分区**
```
dd if=/dev/zero of=/swap1 bs=1M count=512

mkswap /swap1

swapon /swap1

#永久性Swap分区
vim /etc/fstab
在内添加:
/swap1 swap swap defaults 0 0
```

2. 开机自动配网
>每次都串口cmd手动一个个输入命令，累死个人
>注意:此步骤需要串口cmd先手动登陆root用户，成功登陆之后，会自动运行配网脚本。

0.创建`/xddcore_toolbox/`文件夹，将`esp8089-spi.ko`放入。




1.编辑`~/.bashrc`文件
```
vim ~/.bashrc
```
2.在`~/.bashrc`文件末尾写入如下内容。
```
insmod /xddcore_toolbox/esp8089-spi.ko
ifconfig wlan0 up
wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf
udhcpc -i wlan0
```

**这里大家肯定有一个疑问，有没有不用登陆root用户，也可以自动配网的方式呢？答案是肯定的，操作步骤如下:**

1.创建/etc/init.d/net.sh脚本
```
vim /etc/init.d/net.sh
```
2.文件中填入如下内容
```
#!/bin/bash
 
### BEGIN INIT INFO
# Provides:          skeleton
# Required-Start:    $remote_fs $syslog
# Required-Stop:     $remote_fs $syslog
# Should-Start:      $portmap
# Should-Stop:       $portmap
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: Example initscript
### END INIT INFO
 
insmod /xddcore_toolbox/esp8089-spi.ko
ifconfig wlan0 up
wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf
udhcpc -i wlan0
 
exit 0
```
2.给脚本设置可运行权限
```
chmod 777 net.sh
```

3.设置脚本自动启动
> Note: 数字越大越晚执行，99代表最后执行。符合我们的需求。
```
update-rc.d net.sh defaults 99
```

4.如果未来不需要的时候，去除自动运行
```
update-rc.d net.sh remove
```

#### 1.2.8 系统性能测试
1.安装sysbench
```
wget https://github.com/akopytov/sysbench/archive/refs/tags/1.0.20.tar.gz
tar -zxvf 1.0.20.tar.gz
```

2.编译安装
```
apt install libtool m4 automake pkg-config
cd sysbench-1.0.20/
./autogen.sh
# Add --with-pgsql to build with PostgreSQL support
./configure --without-mysql
make -j
make install
```

3.安装完成后，查看sysbench版本
```
sysbench --version
```

4.性能测试
```
sysbench cpu --cpu-max-prime=200 run
```

### 1.3 驱动开发

#### 1.3.1 Linux音频
1.在debian下，查看声卡
```
cat /proc/asound/cards
```

2. 安装alsa-utils
```
apt install alsa-utils
```

3. 设置默认声卡
```
vim /etc/asound.conf

添加如下内容:
defaults.ctl.card 1
defaults.pcm.card 1
defaults.timer.card 1
```

4. 安装音频/视频播放软件
```
apt install mplayer 
```

5. 启动运放(PE10拉高 NUM=138)
```
echo 138 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio138/direction
echo 1 > /sys/class/gpio/gpio138/value
echo 138 > /sys/class/gpio/unexport
```

6. 播放歌曲
```
mplayer /xddcore_toolbox/you.mp3 
```

7. 网易云音乐命令行版本
```
apt install mpg123
apt install python3-pip
pip3 install NetEase-MusicBox
#这一步需要比较长的时间，耐心等待
#运行
musicbox
```

#### 1.3.2 ESP8266EX WIFI驱动

以下驱动代码**在buildroot生成的rootfs中**调试开发。

**性能参数:**
>WIFI速度下载806KB/s,上传729KB/s。以上结果由`speedtest`得出，仅供参考
![wifi_speedtest](/img/wifi_speedtest.jpg)

>WIFI稳定性:
**路由器:**     
![WIFI_Stability_Router](/img/WIFI_Stability_Router.jpeg)
**手机热点:**
![WIFI_Stability_SOFTAP](/img/WIFI_Stability_SOFTAP.jpeg) 
用来测试的手机比较老了，等后面换一台再试试

1. 拉取代码
```
https://github.com/xddcore/ESP8089-SPI.git -b zero-esp8266ex
```

2. 编译代码
```
#KBUILD=换成自己下载的内核路径(我提供的内核:https://github.com/xddcore/linux/tree/zero-v5.10.186-codec)

make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- KBUILD=/home/parallels/xddcore/For_My_Board/linux
```

3. 此时在代码根目录下会生成`esp8089-spi.ko`文件，将驱动文件拷贝至sd卡的rootfs中。

4. SD卡插回开发板。

5. 在开发板的命令行下执行以下命令，加载驱动
```
insmod esp8089-spi.ko
```

此时应该会出现如下log:
![wifi_driver_insmod](/img/wifi_driver_insmod.png)

wlan0会自动启动


6. 编辑 /etc/wpa_supplicant.conf 替换为自己的SSID和密码。
```
vi /etc/wpa_supplicant.conf
```
![wifi_driver_conf](/img/wifi_driver_conf.png)

7. 使用`wpa_supplicant`连接WIFI
```
wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant.conf 
```

8. 此时你可以运行一些简单的wpa_cli来检查工作状态
```
wpa_cli -i wlan0 scan #扫描附近的WIFI

wpa_cli -i wlan0 scan_results #展示扫描结果

wpa_cli -i wlan0 status #查看网卡状态
```

9. 运行结果如下:
```
root@xddcore-zero:~# wpa_cli -i wlan0 scan #扫描附近的WIFI
OK
root@xddcore-zero:~# 
root@xddcore-zero:~# wpa_cli -i wlan0 scan_results #展示扫描结果
bssid / frequency / signal level / flags / ssid
34:8f:27:5e:13:a8       2432    -80     [WPA2-EAP+FT/EAP-CCMP][ESS]     ASK4 Wireless (802.1x)
34:8f:27:9e:13:a8       2432    -81     [WPA2-PSK-CCMP][ESS]    Glasgow West End Staff
94:83:c4:0f:35:2f       2457    -56     [ESS]   GL-MT1300-52d
34:8f:27:1e:13:a8       2432    -81     [ESS]   ASK4 Wireless
root@xddcore-zero:~# 
root@xddcore-zero:~# wpa_cli -i wlan0 status #查看网卡状态
bssid=94:83:c4:0f:35:2f
freq=2457
ssid=GL-MT1300-52d
id=0
mode=station
pairwise_cipher=NONE
group_cipher=NONE
key_mgmt=NONE
wpa_state=COMPLETED
ip_address=192.168.8.193
p2p_device_address=18:fe:34:cd:30:ca
address=18:fe:34:cd:30:ca
uuid=8f4984fd-97c3-52a9-ac66-48aefaaa4498
```
10. 对于ssh之类的应用来说，你可能需要一个IP地址
```
udhcpc -i wlan0
```

最后获取IP如下图:
![wifi_driver_ip](/img/wifi_driver_ip.jpeg)

11. 至此，网卡驱动折腾完毕

#### 1.3.3 MPU6050驱动

1. 安装IIO设备工具包
```
apt install libiio-utils
```

2. 测试MPU6050
```
#读取所有IIO设备信息
iio-info
```

```
#读取MPU6050信息
iio_readdev -b 256 -s 1 iio:device0
#应该会返回乱码，因为以二进制返回
```

3. 查看当前采样率
```
cat /sys/bus/iio/devices/iio:device0/sampling_frequency
```

4. 查看可以设置的采样率
```
cat /sys/bus/iio/devices/iio:device0/sampling_frequency_available
```

5. 设置采样率
```
echo 500 > /sys/bus/iio/devices/iio:device0/sampling_frequency
```

6. 通过命令行读取加速度和角速度数据
```
while true; do
  x_accel=$(awk '{print $1*0.000598}' /sys/bus/iio/devices/iio:device0/in_accel_x_raw)
  y_accel=$(awk '{print $1*0.000598}' /sys/bus/iio/devices/iio:device0/in_accel_y_raw)
  z_accel=$(awk '{print $1*0.000598}' /sys/bus/iio/devices/iio:device0/in_accel_z_raw)
  x_anglvel=$(awk '{print $1*0.001064724}' /sys/bus/iio/devices/iio:device0/in_anglvel_x_raw)
  y_anglvel=$(awk '{print $1*0.001064724}' /sys/bus/iio/devices/iio:device0/in_anglvel_y_raw)
  z_anglvel=$(awk '{print $1*0.001064724}' /sys/bus/iio/devices/iio:device0/in_anglvel_z_raw)

  echo "X: $x_accel m/s², Y: $y_accel m/s², Z: $z_accel m/s²"
  echo "X: $x_anglvel °/s, Y: $y_anglvel °/s, Z: $z_anglvel °/s"
  echo " "
  sleep 1
done
```

7. 通过互补滤波计算X轴和Y轴角度
>Note: Bash的数学运算效率不是很高，所以响应速度比较慢。以下代码仅作为测试。


```
#!/bin/bash

# 初始角度
angle_x=0
angle_y=0

# 滤波因子，可以根据实际情况进行调整
alpha=0.98

while true; do
  x_accel=$(awk '{print $1*0.000598}' /sys/bus/iio/devices/iio:device0/in_accel_x_raw)
  y_accel=$(awk '{print $1*0.000598}' /sys/bus/iio/devices/iio:device0/in_accel_y_raw)
  z_accel=$(awk '{print $1*0.000598}' /sys/bus/iio/devices/iio:device0/in_accel_z_raw)
  x_anglvel=$(awk '{print $1*0.001064724}' /sys/bus/iio/devices/iio:device0/in_anglvel_x_raw)
  y_anglvel=$(awk '{print $1*0.001064724}' /sys/bus/iio/devices/iio:device0/in_anglvel_y_raw)
  z_anglvel=$(awk '{print $1*0.001064724}' /sys/bus/iio/devices/iio:device0/in_anglvel_z_raw)

  # 根据角速度计算角度增量，考虑到陀螺仪给出的是角速度，我们需要乘以时间间隔
  angle_x=$(echo "$angle_x + $x_anglvel * 0.01" | bc)
  angle_y=$(echo "$angle_y + $y_anglvel * 0.01" | bc)

  # 根据加速度计算角度，需要将加速度转换为角度
  accel_angle_x=$(echo "a( $y_accel / sqrt( $x_accel*$x_accel + $z_accel*$z_accel ) ) * 180 / 3.14159265" | bc -l)
  accel_angle_y=$(echo "a( $x_accel / sqrt( $y_accel*$y_accel + $z_accel*$z_accel ) ) * 180 / 3.14159265" | bc -l)

  # 使用互补滤波计算角度
  angle_x=$(echo "$alpha * $angle_x + (1 - $alpha) * $accel_angle_x" | bc)
  angle_y=$(echo "$alpha * $angle_y + (1 - $alpha) * $accel_angle_y" | bc)

  echo "X: $x_accel m/s², Y: $y_accel m/s², Z: $z_accel m/s²"
  echo "X: $x_anglvel °/s, Y: $y_anglvel °/s, Z: $z_anglvel °/s"
  echo "Angle X: $angle_x °, Angle Y: $angle_y °"
  echo " "
  sleep 0.01
done
```

8. 利用c语言实现一个高效的互补滤波(以下代码写入`mpu6050.c`文件)
```
#include <stdio.h>
#include <math.h>
#include <unistd.h>
#include <time.h>

#define ALPHA 0.98
#define DT 0.001  // 1ms
#define PRINT_INTERVAL 0.1  // 100ms
#define GYRO_SCALE_FACTOR 0.001064724
#define ACCEL_SCALE_FACTOR 0.000598

double get_value(char *filename) {
    double value;
    FILE *fp = fopen(filename, "r");
    fscanf(fp, "%lf", &value);
    fclose(fp);
    return value;
}

int main() {
    double angle_x = 0;
    double angle_y = 0;
    int print_counter = 0;
    int print_interval_counts = PRINT_INTERVAL / DT;

    struct timespec delay = {0, DT * 1e9}; // Delay for nanosleep

    while (1) {
        double x_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_x_raw") * ACCEL_SCALE_FACTOR;
        double y_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_y_raw") * ACCEL_SCALE_FACTOR;
        double z_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_z_raw") * ACCEL_SCALE_FACTOR;
        double x_anglvel = get_value("/sys/bus/iio/devices/iio:device0/in_anglvel_x_raw") * GYRO_SCALE_FACTOR;
        double y_anglvel = get_value("/sys/bus/iio/devices/iio:device0/in_anglvel_y_raw") * GYRO_SCALE_FACTOR;
        double z_anglvel = get_value("/sys/bus/iio/devices/iio:device0/in_anglvel_z_raw") * GYRO_SCALE_FACTOR;

        angle_x += x_anglvel * DT;
        angle_y += y_anglvel * DT;

        double accel_angle_x = atan2(y_accel, sqrt(pow(x_accel, 2) + pow(z_accel, 2))) * 180 / M_PI;
        double accel_angle_y = atan2(x_accel, sqrt(pow(y_accel, 2) + pow(z_accel, 2))) * 180 / M_PI;

        angle_x = ALPHA * angle_x + (1 - ALPHA) * accel_angle_x;
        angle_y = ALPHA * angle_y + (1 - ALPHA) * accel_angle_y;

        if (++print_counter >= print_interval_counts) {
            printf("X: %lf m/s², Y: %lf m/s², Z: %lf m/s²\n", x_accel, y_accel, z_accel);
            printf("X: %lf °/s, Y: %lf °/s, Z: %lf °/s\n", x_anglvel, y_anglvel, z_anglvel);
            printf("Angle X: %lf °, Angle Y: %lf °\n\n", angle_x, angle_y);
            print_counter = 0;
        }

        nanosleep(&delay, NULL);
    }

    return 0;
}

```


9. 卡尔曼滤波(性能优于互补滤波)(以下代码写入`mpu6050.c`文件)
```
#include <stdio.h>
#include <math.h>
#include <unistd.h>
#include <time.h>

#define DT 0.001  // 1ms
#define PRINT_INTERVAL 0.1  // 100ms
#define GYRO_SCALE_FACTOR 0.001064724
#define ACCEL_SCALE_FACTOR 0.000598

double get_value(char *filename) {
    double value;
    FILE *fp = fopen(filename, "r");
    fscanf(fp, "%lf", &value);
    fclose(fp);
    return value;
}

// 卡尔曼滤波器的结构
typedef struct {
    double q;  // 过程噪声协方差
    double r;  // 测量噪声协方差
    double x;  // 最优化估算值
    double p;  // 估算误差协方差
    double k;  // 卡尔曼增益
} kalman_state;

// 卡尔曼滤波器的初始化
void kalman_init(kalman_state *state, double q, double r, double p, double initial_value) {
    state->q = q;
    state->r = r;
    state->p = p;
    state->x = initial_value;
}

// 卡尔曼滤波器的更新
void kalman_update(kalman_state *state, double measurement) {
    // 预测
    state->p += state->q;

    // 更新
    state->k = state->p / (state->p + state->r);
    state->x += state->k * (measurement - state->x);
    state->p = (1 - state->k) * state->p;
}

int main() {
    struct timespec delay = {0, DT * 1e9}; // Delay for nanosleep
    int print_counter = 0;
    int print_interval_counts = PRINT_INTERVAL / DT;

    kalman_state state_x;
    kalman_state state_y;
    kalman_init(&state_x, 0.125, 32, 1023, 0);  // You may need to adjust these values based on your sensor's characteristics
    kalman_init(&state_y, 0.125, 32, 1023, 0);  // You may need to adjust these values based on your sensor's characteristics

    while (1) {
        double x_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_x_raw") * ACCEL_SCALE_FACTOR;
        double y_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_y_raw") * ACCEL_SCALE_FACTOR;
        double z_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_z_raw") * ACCEL_SCALE_FACTOR;
        double x_anglvel = get_value("/sys/bus/iio/devices/iio:device0/in_anglvel_x_raw") * GYRO_SCALE_FACTOR;
        double y_anglvel = get_value("/sys/bus/iio/devices/iio:device0/in_anglvel_y_raw") * GYRO_SCALE_FACTOR;
        double z_anglvel = get_value("/sys/bus/iio/devices/iio:device0/in_anglvel_z_raw") * GYRO_SCALE_FACTOR;

        double accel_angle_x = atan2(y_accel, sqrt(pow(x_accel, 2) + pow(z_accel, 2))) * 180 / M_PI;
        double accel_angle_y = atan2(x_accel, sqrt(pow(y_accel, 2) + pow(z_accel, 2))) * 180 / M_PI;

        kalman_update(&state_x, accel_angle_x);
        kalman_update(&state_y, accel_angle_y);

        if (++print_counter >= print_interval_counts) {
            printf("X: %lf m/s², Y: %lf m/s², Z: %lf m/s²\n", x_accel, y_accel, z_accel);
            printf("X: %lf °/s, Y: %lf °/s, Z: %lf °/s\n", x_anglvel, y_anglvel, z_anglvel);
            printf("Angle X: %lf °, Angle Y: %lf °\n\n", state_x.x, state_y.x);
            print_counter = 0;
            print_counter = 0;
        }

        nanosleep(&delay, NULL);
    }

    return 0;
}

```

10. 编译
```
gcc -o mpu6050 mpu6050.c -lm
```
11. 运行
```
./mpu6050
```

12. **耐心大作战|一个利用X轴角度和Y轴角度设计的小游戏**
>在这个游戏中，你将看到一个由"."组成的20x20的网格。玩家（标记为"P"）通过调整设备的角度来在屏幕上移动P。目标位置（标记为"T"）在网格的一个固定位置。当玩家到达目标位置时，游戏结束，并显示"Congratulations, you won!"的消息。

**新手模式**(以下代码写入`mpu6050_game.c`文件)

```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <unistd.h>
#include <time.h>

#define DT 0.001  // 1ms
#define PRINT_INTERVAL 0.05  // 50ms
#define GYRO_SCALE_FACTOR 0.001064724
#define ACCEL_SCALE_FACTOR 0.000598
#define BOARD_SIZE 20

int TARGET_X=0,TARGET_Y=0;

double get_value(char *filename) {
    double value;
    FILE *fp = fopen(filename, "r");
    fscanf(fp, "%lf", &value);
    fclose(fp);
    return value;
}

typedef struct {
    double q;  
    double r;  
    double x;  
    double p;  
    double k;  
} kalman_state;

void kalman_init(kalman_state *state, double q, double r, double p, double initial_value) {
    state->q = q;
    state->r = r;
    state->p = p;
    state->x = initial_value;
}

void kalman_update(kalman_state *state, double measurement) {
    state->p += state->q;
    state->k = state->p / (state->p + state->r);
    state->x += state->k * (measurement - state->x);
    state->p = (1 - state->k) * state->p;
}

void print_board(int player_x, int player_y) {
    for(int i=0; i<BOARD_SIZE; i++) {
        for(int j=0; j<BOARD_SIZE; j++) {
            if(i == player_x && j == player_y) {
                printf("P ");
            } else if(i == TARGET_X && j == TARGET_Y) {
                printf("T ");
            } else {
                printf(". ");
            }
        }
        printf("\n");
    }
}

int main() {
    srand(time(NULL));
    TARGET_X = rand() % BOARD_SIZE;
    TARGET_Y = rand() % BOARD_SIZE;
    struct timespec delay = {0, DT * 1e9}; 
    int print_counter = 0;
    int print_interval_counts = PRINT_INTERVAL / DT;

    kalman_state state_x;
    kalman_state state_y;
    kalman_init(&state_x, 0.125, 32, 1023, 0);
    kalman_init(&state_y, 0.125, 32, 1023, 0); 

    int player_x = BOARD_SIZE / 2;
    int player_y = BOARD_SIZE / 2;

    while (1) {
        double x_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_x_raw") * ACCEL_SCALE_FACTOR;
        double y_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_y_raw") * ACCEL_SCALE_FACTOR;
        double z_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_z_raw") * ACCEL_SCALE_FACTOR;

        double accel_angle_x = atan2(y_accel, sqrt(pow(x_accel, 2) + pow(z_accel, 2))) * 180 / M_PI;
        double accel_angle_y = atan2(x_accel, sqrt(pow(y_accel, 2) + pow(z_accel, 2))) * 180 / M_PI;

        kalman_update(&state_x, accel_angle_x);
        kalman_update(&state_y, accel_angle_y);

        // 根据角度调整角色的位置
        if(state_x.x > 15 && player_x > 0) {
            player_x--;
        } else if(state_x.x < -15 && player_x < BOARD_SIZE - 1) {
            player_x++;
        }

        if(state_y.x > 15 && player_y < BOARD_SIZE - 1) {
            player_y++;
        } else if(state_y.x < -15 && player_y > 0) {
            player_y--;
        }

        // 清屏并打印游戏版面
        system("clear");
        print_board(player_x, player_y);

        // 检查角色是否已经到达目标
        if(player_x == TARGET_X && player_y == TARGET_Y) {
            printf("Congratulations, you won!\n");
            break;
        }

        nanosleep(&delay, NULL);
    }

    return 0;
}
```

**高难度模式**(以下代码写入`mpu6050_game.c`文件)
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <unistd.h>
#include <time.h>

#define DT 0.001  // 1ms
#define PRINT_INTERVAL 0.05  // 50ms
#define GYRO_SCALE_FACTOR 0.001064724
#define ACCEL_SCALE_FACTOR 0.000598
#define BOARD_SIZE 20

int TARGET_X=0,TARGET_Y=0;

char last_board[BOARD_SIZE][BOARD_SIZE];

double get_value(char *filename) {
    double value;
    FILE *fp = fopen(filename, "r");
    fscanf(fp, "%lf", &value);
    fclose(fp);
    return value;
}

typedef struct {
    double q;  
    double r;  
    double x;  
    double p;  
    double k;  
} kalman_state;

void kalman_init(kalman_state *state, double q, double r, double p, double initial_value) {
    state->q = q;
    state->r = r;
    state->p = p;
    state->x = initial_value;
}

void kalman_update(kalman_state *state, double measurement) {
    state->p += state->q;
    state->k = state->p / (state->p + state->r);
    state->x += state->k * (measurement - state->x);
    state->p = (1 - state->k) * state->p;
}

void print_board(int player_x, int player_y) {
    for(int i=0; i<BOARD_SIZE; i++) {
        for(int j=0; j<BOARD_SIZE; j++) {
            char new_char;
            if(i == player_x && j == player_y) {
                new_char = 'P';
            } else if(i == TARGET_X && j == TARGET_Y) {
                new_char = 'T';
            } else {
                new_char = '.';
            }
            if(last_board[i][j] != new_char) {
                printf("\033[%d;%dH%c", i+1, j*2+1, new_char);
                fflush(stdout); // 确保字符被立即打印
                last_board[i][j] = new_char;
            }
        }
    }
}

int main() {
    srand(time(NULL));
    system("clear");
    TARGET_X = rand() % BOARD_SIZE;
    TARGET_Y = rand() % BOARD_SIZE;
    struct timespec delay = {0, DT * 1e9}; 
    int print_counter = 0;
    int print_interval_counts = PRINT_INTERVAL / DT;

    kalman_state state_x;
    kalman_state state_y;
    kalman_init(&state_x, 0.125, 32, 1023, 0);
    kalman_init(&state_y, 0.125, 32, 1023, 0); 

    int player_x = BOARD_SIZE / 2;
    int player_y = BOARD_SIZE / 2;

    while (1) {
        double x_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_x_raw") * ACCEL_SCALE_FACTOR;
        double y_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_y_raw") * ACCEL_SCALE_FACTOR;
        double z_accel = get_value("/sys/bus/iio/devices/iio:device0/in_accel_z_raw") * ACCEL_SCALE_FACTOR;

        double accel_angle_x = atan2(y_accel, sqrt(pow(x_accel, 2) + pow(z_accel, 2))) * 180 / M_PI;
        double accel_angle_y = atan2(x_accel, sqrt(pow(y_accel, 2) + pow(z_accel, 2))) * 180 / M_PI;

        kalman_update(&state_x, accel_angle_x);
        kalman_update(&state_y, accel_angle_y);

        // 根据角度调整角色的位置
        if(state_x.x > 15 && player_x > 0) {
            player_x--;
        } else if(state_x.x < -15 && player_x < BOARD_SIZE - 1) {
            player_x++;
        }

        if(state_y.x > 15 && player_y < BOARD_SIZE - 1) {
            player_y++;
        } else if(state_y.x < -15 && player_y > 0) {
            player_y--;
        }

        // 打印游戏版面
        print_board(player_x, player_y);

        // 检查角色是否已经到达目标
        if(player_x == TARGET_X && player_y == TARGET_Y) {
            printf("\033[%d;%dH", BOARD_SIZE + 1, 1); // 将光标移动到版面下方
            printf("Congratulations, you won!\n");
            break;
        }

        nanosleep(&delay, NULL);
    }

    return 0;
}

```

13. 编译
```
gcc -o mpu6050_game mpu6050_game.c -lm
```
14. 运行
```
./mpu6050_game
```

#### 1.3.4 2.8寸ISP电容触摸屏驱动&LVGL

0. 下载交叉编译工具链
```
#!/bin/sh

HOST=arm-linux-gnueabi
SCRIPT_PATH=$(pwd)

#修改源码包解压后的名称
MAJOR_NAME=gcc-arm-linux-gnueabi

#修改需要下载的源码版本前缀和后缀
OPENSRC_VER_PREFIX=7.2
OPENSRC_VER_SUFFIX=.1

PACKAGE_NAME=${MAJOR_NAME}-${OPENSRC_VER_PREFIX}${OPENSRC_VER_SUFFIX}

#定义压缩包名称
COMPRESS_PACKAGE=gcc-linaro-7.2.1-2017.11-x86_64_arm-linux-gnueabi.tar.xz

#定义编译后安装--生成的文件,文件夹位置路径
INSTALL_PATH=/opt/${PACKAGE_NAME}

#无需修改--下载地址
DOWNLOAD_LINK=https://releases.linaro.org/components/toolchain/binaries/7.2-2017.11/arm-linux-gnueabi/${COMPRESS_PACKAGE}

#下载源码包
do_download_src () {
   echo "start download ${COMPRESS_PACKAGE}..."
   if [ ! -f "${COMPRESS_PACKAGE}" ];then
      if [ ! -d "${PACKAGE_NAME}" ];then
        wget -c ${DOWNLOAD_LINK}
      fi
   fi
   echo "\033[1;33mdone...\033[0m"
}

#解压源码包
do_tar_package () {
   echo "start unpacking the ${PACKAGE_NAME} package ..."

   mkdir -p ${INSTALL_PATH}

   if [ ! -d "${PACKAGE_NAME}" ];then
      tar -xf ${COMPRESS_PACKAGE} -C ${INSTALL_PATH} --strip-components=1
   fi
   echo "done..."
}

#删除下载的文件
do_delete_file () {
   cd ${SCRIPT_PATH}
   if [ -f "${PACKAGE_NAME}" ];then
      sudo rm -f ${PACKAGE_NAME}
   fi
}

do_download_src
do_tar_package
# do_delete_file

exit $?
```

1. 拉取源码
**所有控件展示的demo**
```
git clone https://github.com/xddcore/lv_port_linux_frame_buffer -b zero-lvgl
```
**心率，血压demo**
```
git clone https://github.com/xddcore/lv_port_linux_frame_buffer -b zero_lvgl_heartrate
```
2. 拉取子模块
```
cd lv_port_linux_frame_buffer/
git submodule update --init --recursive
```

3. 生成Makefile，然后编译源码
```
#ls看一下，如有/build，则请先执行rm -rf build/
mkdir build
cd build
cmake ..
make
```

4. 运行
```
./lvgl_fb
```

一些优化体验的指令
```
echo -e "\033[?25l" > /dev/tty1 #关闭光标
echo -e "\033[?25h" > /dev/tty1 #开启光标
```






#### 1.3.5 树莓派RP2040 USB驱动

RP2040的`RUN(PE8，NUM=136)引脚`以及`BOOT(PE7，NUM=135)引脚`受到F1C200S的控制，因此F1C200S可以方便的对RP2040进行编程。


1. 操作RP2040进入DFU模式
```
echo 136 > /sys/class/gpio/export
echo 135 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio136/direction
echo out > /sys/class/gpio/gpio135/direction
echo 0 > /sys/class/gpio/gpio136/value
echo 0 > /sys/class/gpio/gpio135/value
sleep 1
echo 1 > /sys/class/gpio/gpio136/value
sleep 1
echo 1 > /sys/class/gpio/gpio135/value
echo 136 > /sys/class/gpio/unexport
echo 135 > /sys/class/gpio/unexport
```

2. 将F1C200s USB模式切换为Host
```
echo host > /sys/devices/platform/soc/1c13000.usb/musb-hdrc.1.auto/mode

#补充一下如果要换成device模式的话，执行以下代码:
echo peripheral > /sys/devices/platform/soc/1c13000.usb/musb-hdrc.1.auto/mode
```

3. RP2040已进入DFU模式(此时在Linux上表现为一个存储设备)
```
fdisk -l
```
![rp2040_fdisk-l](/img/rp2040_fdisk-l.jpeg)

4. 挂载RP2040
```
#此处根据实际情况修改可能为sda1或sdb1
mount -t vfat /dev/sda1 /media
```

5. 下载MicroPython固件
```
wget https://micropython.org/download/rp2-pico/rp2-pico-latest.uf2
```

**Bug修复**    
**Bug现象**:重启后固件丢失，以及flash size无法正确返回的问题。     
**SPI Flash型号**:W25Q128JV      
**解决办法**:    
根据数据手册，`Clock frequency for Read Data instruction (03h) fR D.C. 50 MHz`，最大读取数据指令时钟为50Mhz。MicroPython配置的PICO_FLASH_SPI_CLKDIV=4时，时钟约为60Mhz，将会导致SPI Flash无法工作。我们在编译程序时，需要手动降低至40Mhz(添加编译选项 PICO_FLASH_SPI_CLKDIV= 6,BOOT2_S_CFLAGS ?= -DPICO_FLASH_SPI_CLKDIV= 6)。     
**参考:**
> https://github.com/adafruit/circuitpython/issues/4377        
> https://github.com/raspberrypi/pico-sdk/issues/1304 (两种fixup思路)    
> https://github.com/adafruit/circuitpython/commit/aec03a409f66cdb90e1b51c7ffb827750eadd830    

5. 下载CircuitPython固件
```
wget https://downloads.circuitpython.org/bin/raspberry_pi_pico/en_US/adafruit-circuitpython-raspberry_pi_pico-en_US-8.2.0.uf2
```

5. Pico-SDK
```
git clone https://github.com/raspberrypi/pico-sdk
```
> Note: Pico-SDK的SPI Flash时钟部分和MicroPython具有相同Bug，参考上述方法进行修复。

6. 烧录固件至RP2040
```
#micropython
cp /xddcore_toolbox/rp2-pico-latest.uf2 /media/

#circuitpython
cp /xddcore_toolbox/adafruit-circuitpython-raspberry_pi_pico-en_US-8.2.0.uf2 /media/
```

7. 成功烧录后，你将看到如下提示：
```
[  164.934750] usb 1-1: USB disconnect, device number 2
[  164.948943] blk_update_request: I/O error, dev sda, sector 260 op 0x1:(WRITE) flags 0x0 phys_seg 1 prio class 0
[  164.959264] Buffer I/O error on dev sda1, logical block 259, lost async page write
[  165.499616] usb 1-1: new full-speed USB device number 3 using musb-hdrc
[  165.692558] cdc_acm 1-1:1.0: ttyACM0: USB ACM device
```

8. 装个MINICOM(与MicroPython进行交互)
```
apt install minicom
```

9. 查看USB串口设备
>USB 串行设备通常显示为 /dev/ttyUSBx 或 /dev/ttyACMx，其中 x 是一个数字。
```
 ls /dev/tty*
```

10. 连接RP2040
```
minicom -o -D /dev/ttyACM0
```
![rp2040_micropython](/img/rp2040_micropython.jpeg)
![circuitpython](/img/circuitpython.jpg)
11. 运行如下测试代码

>代码作用:查看SPI FLASH大小
```
import os

stat = os.statvfs('/')
flash_size_bytes = stat[0] * stat[2]

flash_size_MB = flash_size_bytes / (1024 * 1024)
print('SPI Flash size:', flash_size_MB, 'MB')

```
返回结果:
```
Adafruit CircuitPython 8.2.0 on 2023-07-05; Raspberry Pi Pico with rp2040
>>> import os

stat = os.statvfs('/')
flash_size_bytes = stat[0] * stat[2]

flash_size_MB = flash_size_bytes / (1024 * 1024)
print('SPI Flash size:', flash_size_MB, 'MB')

SPI Flash size: 14.9688 MB
>>> 
```

12. 退出MINICOM
```
ctrl A Q
```

13. 重启RP2040(如果需要)
```
echo 136 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio136/direction
echo 0 > /sys/class/gpio/gpio136/value
sleep 1
echo 1 > /sys/class/gpio/gpio136/value
sleep 1
echo 136 > /sys/class/gpio/unexport
```

14. 操作RP2040进入DFU模式
```
echo 136 > /sys/class/gpio/export
echo 135 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio136/direction
echo out > /sys/class/gpio/gpio135/direction
echo 1 > /sys/class/gpio/gpio136/value
echo 1 > /sys/class/gpio/gpio135/value
echo 136 > /sys/class/gpio/unexport
echo 135 > /sys/class/gpio/unexport
```

#### 1.3.6 语音识别与交互驱动
离线文字转语音espeak
```
apt install espeak
```



### 1.4 玩法推荐

> 以下所有DEMO，若运行报错，可尝试git pull拉取最新代码。

#### 1.4.1 在ISP屏幕上显示系统信息
```
neofetch --off > /dev/tty1
```


#### 1.4.2 在ISP屏幕上显示图片
1. 安装`fbi`
```
apt install fbi
```
2. 显示图片
>这里，-a：这个选项会让 fbi 自动缩放图像，使其适应屏幕的大小。 -noverbose：这个选项告诉 fbi 在启动时不要显示任何冗长的信息或警告。 -d /dev/fb0 指定了帧缓冲设备，-T 1 指定了使用哪个虚拟终端，image.jpg 是要显示的图像的路径。
```
fbi -a -noverbose -d /dev/fb0 -T 1 image.jpg
```
如果要关闭可以键盘`esc`或`q`，或者直接杀死进程。       .
3.使用`ffmpeg`显示图片
```
#demo1(无缩放)
ffmpeg -i input.jpg -c:v rawvideo -pix_fmt rgb565le -f fbdev /dev/fb0

#demo2(自动缩放)
ffmpeg -i ../ILSVRC2012_val_00000003.JPEG -vf "scale='min(320,iw)':'min(240,ih)'" -c:v rawvideo -pix_fmt rgb565le -f fbdev /dev/fb0
```


#### 1.4.3 在ISP屏幕上视频播放

```
ffmpeg -re -i video2_h264.mp4 -c:v rawvideo -pix_fmt rgb565le -f fbdev /dev/fb0
```

#### 1.4.4 USB摄像头
>注意，由于F1C200S USB EndPoint不足，所以无法驱动USB摄像头。
1. 查看摄像头支持的输出格式
```
v4l2-ctl --list-formats
v4l2-ctl --list-formats-ext
```
```
root@xddcore-zero:/xddcore_toolbox/v4l2_cameara# v4l2-ctl --list-formats
ioctl: VIDIOC_ENUM_FMT
        Type: Video Capture

        [0]: 'MJPG' (Motion-JPEG, compressed)
        [1]: 'YUYV' (YUYV 4:2:2)
```
2. 捕获图像
```
fswebcam -d /dev/video0 -r 320x240 test.jpeg
ffmpeg -f v4l2 -s 640x480 -i /dev/video0 output.jpg
```

#### 1.4.5 本地音乐播放

**音频播放请先通过以下命令打开运放**:
```
echo 138 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio138/direction
echo 1 > /sys/class/gpio/gpio138/value
echo 138 > /sys/class/gpio/unexport
```
```
mplayer xxx.mp3

或

aplayer xxx.mp3
```

#### 1.4.6 网易云音乐播放音乐播放
```
musicbox
```

#### 1.4.7 6轴陀螺仪
```
#demo1
/xddcore_toolbox/mpu6050

#demo2
/xddcore_toolbox/mpu6050_game
```

#### 1.4.8 LVGL
```
#demo1
/xddcore_toolbox/zero_lvgl_port/demo/lvgl_fb_example

#demo2
/xddcore_toolbox/zero_lvgl_port/demo/lvgl_fb_heartrate
```

#### 1.4.9 RP2040编程

见上述RP2040驱动章节

需要注意:在发布镜像中，由于F1C200S USB Endpoint不足，且开启了USB HID设备，并且USB HUB会占用一定的EndPoint。所以(以Circuit Python为例):

1. `如果要对RP2040的disk进行操作，改写Code.py文件。`则需要将拨码开关配置为`1010 1010`（越过USB Hub进行通信）。
2. `如果要对RP2040的disk进行操作，且需要依赖USB串口的交互模式。`则需要在Linux Kernel Menuconfig中关闭USB HID驱动(或将USB HID驱动编译为模块)后，自行编译内核。
3. `如果要对RP2040的disk进行操作，且需要依赖USB串口的交互模式，且想快速完成rp2040编程的话。`则需要将拨码开关配置为`0101 1010`（F1C200S连接板载USB Hub，RP2040通过Type-C连接电脑）。

#### 1.4.10 智能助手(Chatgpt-3.5)
1. 编辑文件，并填入自己的OPENAI API密钥 
```
vim /xddcore_toolbox/Hello-Pinecone/Hello-Pinecone.py
```
2. 运行DEMO
```
python3 /xddcore_toolbox/Hello-Pinecone/Hello-Pinecone.py
```

#### 1.4.11 登陆月球模拟器
详情见https://github.com/xddcore/TinyLander-Linux-fb

运行DEMO:
```
/xddcore_toolbox/TinyLander-Linux-fb/TinyLander
```

> 如遇屏幕闪烁，请git pull重新拉取最新代码后，重新编译运行。


#### 1.4.12 NES模拟器
>游戏ROM下载地址:https://www.emulatorgames.net/roms/nintendo/

1. 安装依赖
```
apt install alsa-utils
apt install libasound2-dev
apt install zlib1g-dev
```

2. 拉取InfoNES源码
```
git clone https://github.com/xddcore/arm-NES-linux.git -b zero-InfoNES
```

3. 编译
```
cd arm-NES-linux/linux
make
```

>测试游戏包下载:https://github.com/xddcore/arm-NES-linux/releases/tag/NES_Game_Pack

4. 下载测试游戏
```
wget https://github.com/xddcore/arm-NES-linux/releases/download/NES_Test_Game/Super_Mario_Bros_3.nes
```

5. 运行游戏
```
/xddcore_toolbox/arm-NES-linux/linux/InfoNES ./Super_Mario_Bros_3.nes
```


#### 1.4.13 OpenNNA2.0神经网络框架

1.拉取源码
```
git clone https://github.com/xddcore/OpenNNA2.0.git
```

2.编译
```
cd OpenNNA2.0/platform/zero_linux_board/
#ls看一下，如有/build，则请先执行rm -rf build/
mkdir build
cd build
cmake ..
make
```

3.运行
```
#结果显示在cmd
ffmpeg -i ../ILSVRC2012_val_00000003.JPEG -vf "scale=w=320:h=240" -c:v rawvideo -pix_fmt rgb565le -f fbdev /dev/fb0
./core
#结果显示在isp屏幕
ffmpeg -i ../ILSVRC2012_val_00000003.JPEG -vf "scale=w=320:h=240" -c:v rawvideo -pix_fmt rgb565le -f fbdev /dev/fb0
./core > /dev/tty1
```

#### 1.4.14 搭建个人博客(Typecho)

运行博客四件套(Nginx+php+SQlite3+typecho+rathole)，怎么轻量化怎么来

1. **安装nginx**
```
apt install nginx
```

此步骤后会遇到报错```Nginx Error: [::1]:80 failed: Address family not supported by protocol [Solved]```

原因及解决方法:
```
 该错误消息表明该服务正在尝试在 IPv6 地址“ [::]:80 ”上启动，但由于地址系列不受支持而失败。这意味着该机器没有设置 IPv6 地址。您需要做的就是简单地编辑 Ngnix 配置文件来监听 IPv4 地址，如下所示。
```
1. 打开/etc/nginx/sites-enabled/default
```
vim /etc/nginx/sites-enabled/default
```

2. 注释以下行：
```
listen [::]:80 default_server;
```

3. 重新运行安装
```
apt install nginx
```

4. 检查nginx运行状态
```
systemctl status nginx
```

5. 浏览器输入IP地址，再次检查Nginx是否运行正常


2. **安装PHP(内含mysql，sqlite等插件)**
```
apt install php7.3-cli php7.3-fpm php7.3-curl php7.3-mysql php7.3-gd php7.3-xml php7.3-mbstring php-sqlite3
```

3. **安装SQlite3**
```
apt install sqlite3 php-sqlite3
```

4. **修改/etc/nginx/sites-enabled/default(如下图)**
```
vim /etc/nginx/sites-enabled/default
```
![Nginx配置修改](/img/nginx.jpg)
5. **重启nginx**
```
service nginx restart
```

6. **下载`Typecho`(地址:https://typecho.org/download)**
```
cd /var/www/html/
wget https://github.com/typecho/typecho/releases/latest/download/typecho.zip
unzip typecho.zip
rm typecho.zip
```

7. **将上传目录修改为可写入**
```
pwd=/var/www/html
chmod -R 777 ./
```

8. **访问开发板的IP地址**
```
ifconfig
```

9. **按照提示安装Typecho**
注意:数据库驱动请选择 pdo sqlite驱动        
后台:http://开发板IP地址/admin/      


10. Enjoy it!

#### 1.4.15 内网穿透(Rathole)
对于没有公网IP的场景，我们还需要一个内网穿透软件。最终选择`Rathole`(相比frpc`70MB`的内存占用来说，Rathole的内存占用仅`10MB`左右，非常适合部署在zero linux board中)。       

Rathole基于rust开发，官方并没有提供基于armv5tejl的二进制构建文件。所以我们需要手动交叉编译。(万幸，armv5tejl在rust的第二层支持列表中)            

所有服务运行起来后的系统资源信息:
![Typeho+Rathole资源占用](/img/Blog_Rathole_resouce.jpeg)

**以下为在交叉编译环境中的操作**
1. 安装rust
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

2. 安装交叉编译工具链
```
sudo apt-get install -qq gcc-arm-linux-gnueabi
sudo apt-get install gcc-arm-linux-gnueabi libc6-armel-cross libc6-dev-armel-cross
 sudo apt install pkg-config
 sudo apt install libssl-dev
 sudo apt-get install libudev-dev
 sudo apt install librust-openssl-sys-dev
 sudo apt install perl

export OPENSSL_DIR="usr/lib/ssl"
export OPENSSL_INCLUDE_DIR="/usr/include/openssl"
export OPENSSL_LIB_DIR="/usr/lib/x86_64-linux-gnu"
```
3. 添加目标

```
rustup target add armv5te-unknown-linux-gnueabi​​

```

4. 配置cargo
```
$ mkdir -p ~/.cargo
$ vim ~/.cargo/config
#添加以下内容:
[target.armv5te-unknown-linux-gnueabi​​]
linker = "arm-linux-gnueabi-gcc"

```
5. 拉取rathole源码
```
git clone https://github.com/rapiz1/rathole.git
cd rathole/
git checkout tags/v0.4.8
```
6. 编译源码
```
cargo build --release --target armv5te-unknown-linux-gnueabi \
  --no-default-features --features noise,client,server,hot-reload \
  --config target.armv5te-unknown-linux-gnueabi.linker=\"rust-lld\"

  cargo build --release --target armv5te-unknown-linux-gnueabi \
  --no-default-features --features noise,client,server,hot-reload \
  --config target.armv5te-unknown-linux-gnueabi.linker=\"arm-linux-gnueabi-gcc\"
```

7. 编译好的二进制文件在`rathole/target/armv5te-unknown-linux-gnueabi/release`目录下



**服务器部署**
1. 下载构建好的二进制文件
```
wget https://github.com/rapiz1/rathole/releases/download/v0.4.8/rathole-x86_64-unknown-linux-gnu.zip
```
2. 创建并编辑配置文件
```
vim server.toml

#填入以下内容
# server.toml
[server]
bind_addr = "0.0.0.0:2333" # `2333` 配置了服务端监听客户端连接的端口
[server.services.my_blog]
token = "123456" # 用于验证的 token
bind_addr = "0.0.0.0:80" # `5202` 配置了将 `my_blog` 暴露给互联网的端口
```
3. 运行rothole
```
./rothole server.toml
```

**客户端部署(即Zero Linux Board)**
1. 下载构建好的二进制文件
```
wget https://github.com/xddcore/Zero_Linux_Board/releases/download/Rathole_Armv5tejl/rathole
```
2. 创建并编辑配置文件
```
vim client.toml

#填入以下内容
# client.toml
[client]
remote_addr = "myserver.com:2333" # 服务器的地址。端口必须与 `server.bind_addr` 中的端口相同。
[client.services.my_nas_ssh]
token = "use_a_secret_that_only_you_know" # 必须与服务器相同以通过验证
local_addr = "127.0.0.1:22" # 需要被转发的服务的地址
```
3. 运行rothole
```
./rothole client.toml
```





## 1.5 一些图片
![PCB_v10](/img/PCB_v10.JPG)
![Front_Board_Basic_Shell_2](/img/Front_Board_Basic_Shell_2.jpg)
![board1](/img/board1.JPG)
![board2](/img/board2.jpeg)
![board3](/img/board3.jpeg)
![board4](/img/board4.JPG)
![board5](/img/board5.JPG)