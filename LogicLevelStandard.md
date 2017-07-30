<!-- LogicLevelStandard.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 日 7月 30 18:52:51 2017 (+0800)
;; Last-Updated: 日 7月 30 19:03:52 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 2
;; URL: http://wuhongyi.cn -->

# 常见逻辑电平标准

[TTL、CMOS、LVTTL、LVCMOS等常见的电平标准](http://wuhongyi.cn/VHDLNote/pdf/TTL、CMOS、LVTTL、LVCMOS等常见的电平标准.doc)



现在常用的电平标准有TTL、CMOS、LVTTL、LVCMOS、ECL、PECL、LVPECL、RS232、RS485等，还有一些速度比较高的 LVDS、GTL、PGTL、CML、HSTL、SSTL等。

下面简单介绍一下各自的供电电源、电平标准以及使用注意事项。


## TTL

TTL：Transistor-Transistor Logic 三极管结构。 Vcc：5V；VOH>=2.4V；VOL<=0.5V；VIH>=2V；VIL<=0.8V。

因为2.4V与5V之间还有很大空闲，对改善噪声容限并没什么好处，又会白白增大系统功耗，还会影响速度。所以后来就把一部分“砍”掉了。也就是后面的LVTTL。

LVTTL又分3.3V、2.5V以及更低电压的LVTTL(Low Voltage TTL)。

3.3V LVTTL： Vcc：3.3V；VOH>=2.4V；VOL<=0.4V；VIH>=2V；VIL<=0.8V。

2.5V LVTTL： Vcc：2.5V；VOH>=2.0V；VOL<=0.2V；VIH>=1.7V；VIL<=0.7V。

更低的LVTTL不常用就先不讲了。多用在处理器等高速芯片，使用时查看芯片手册就OK了。

TTL使用注意：

TTL电平一般过冲都会比较严重，可能在始端串22欧或33欧电阻； TTL电平输入脚悬空时是内部认为是高电平。要下拉的话应用1k以下电阻下拉。TTL输出不能驱动CMOS输入。


## CMOS

CMOS：Complementary Metal Oxide Semiconductor??PMOS+NMOS。 Vcc：5V；VOH>=4.45V；VOL<=0.5V；VIH>=3.5V；VIL<=1.5V。

相对TTL有了更大的噪声容限，输入阻抗远大于TTL输入阻抗。对应3.3V LVTTL，出现了LVCMOS，可以与3.3V的LVTTL直接相互驱动。

3.3V LVCMOS： Vcc：3.3V；VOH>=3.2V；VOL<=0.1V；VIH>=2.0V；VIL<=0.7V。

2.5V LVCMOS： Vcc：2.5V；VOH>=2V；VOL<=0.1V；VIH>=1.7V；VIL<=0.7V。

CMOS使用注意：

CMOS结构内部寄生有可控硅结构，当输入或输入管脚高于VCC一定值(比如一些芯片是0.7V)时，电流足够大的话，可能引起闩锁效应，导致芯片的烧毁。

## ECL

ECL：Emitter Coupled Logic 发射极耦合逻辑电路(差分结构)

Vcc=0V；Vee：-5.2V；VOH=-0.88V；VOL=-1.72V；VIH=-1.24V；VIL=-1.36V。

速度快，驱动能力强，噪声小，很容易达到几百M的应用。但是功耗大，需要负电源。为简化电源，出现了PECL(ECL结构，改用正电压供电)和LVPECL。 PECL：Pseudo/Positive ECL

Vcc=5V；VOH=4.12V；VOL=3.28V；VIH=3.78V；VIL=3.64V

LVPELC：Low Voltage PECL

Vcc=3.3V；VOH=2.42V；VOL=1.58V；VIH=2.06V；VIL=1.94V

ECL、 PECL、LVPECL使用注意：

不同电平不能直接驱动。中间可用交流耦合、电阻网络或专用芯片进行转换。以上三种均为射随输出结构，必须有电阻拉到一个直流偏置电压。(如多用于时钟的LVPECL：直流匹配时用130欧上拉，同时用82欧下拉；交流匹配时用82欧上拉，同时用130欧下拉。但两种方式工作后直流电平都在1.95V左右。)

前面的电平标准摆幅都比较大，为降低电磁辐射，同时提高开关速度又推出LVDS电平标准。

## LVDS

LVDS：Low Voltage Differential Signaling

差分对输入输出，内部有一个恒流源3.5-4mA，在差分线上改变方向来表示0和1。通过外部的100欧匹配电阻(并在差分线上靠近接收端)转换为±350mV的差分电平。

LVDS使用注意：

可以达到600M以上，PCB要求较高，差分线要求严格等长，差最好不超过10mil(0.25mm)。100欧电阻离接收端距离不能超过500mil，最好控制在300mil以内。

----







<!-- LogicLevelStandard.md ends here -->
