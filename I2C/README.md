<!-- README.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 二 3月  5 14:01:39 2019 (+0800)
;; Last-Updated: 二 3月  5 14:37:13 2019 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 2
;; URL: http://wuhongyi.cn -->

# I2C

- [I2C总线入门](http://wuhongyi.cn/FPGANote/pdf/I2C/I2C总线入门_很详细很经典.doc)
- [I2C总线简介](http://wuhongyi.cn/FPGANote/pdf/I2C/I2C总线简介很经典.docx)

----

I2C（Inter-integrated Circuit）总线支持设备之间的短距离通信，用于处理器和一些外围设备之间的接口，它只需要两根信号线来完成信息交换。I2C最早是飞利浦在1982年开发设计并用于自己的芯片上，一开始只允许100kHz、7-bit标准地址。1992年，I2C的第一个公共规范发行，增加了400kHz的快速模式以及10-bit扩展地址。在I2C的基础上，1995年Intel提出了“System Management Bus” (SMBus)，用于低速设备通信，SMBus 把时钟频率限制在10kHz~100kHz，但I2C可以支持0kHz~5MHz的设备：普通模式（100kHz即100kbps）、快速模式（400kHz）、快速模式+（1MHz）、高速模式（3.4MHz）和超高速模式（5MHz）。


2C最少只需要两根线，和异步串口类似，但可以支持多个slave设备。和SPI不同的是，I2C可以支持mul-master系统，允许有多个master并且每个master都可以与所有的slaves通信（master之间不可通过I2C通信，并且每个master只能轮流使用I2C总线）。master是指启动数据传输的设备并在总线上生成时钟信号以驱动该传输，而被寻址的设备都作为slaves。 

I2C的数据传输速率位于串口和SPI之间，大部分I2C设备支持100KHz和400KHz模式。使用I2C传输数据会有一些额外消耗：每发送8bits数据，就需要额外1bit的元数据（ACK或NACK）。I2C支持双向数据交换，由于仅有一根数据线，故通信是半双工的。 
硬件复杂度也位于串口和SPI之间，而软件实现可以相当简单。


## I2C协议

I2C协议把传输的消息分为两种类型的帧： 
- 一个地址帧 —— 用于master指明消息发往哪个slave； 
- 一个或多个数据帧 —— 由master发往slave的数据（或由slave发往master），每一帧是8-bit的数据。 

注：协议要求每次放到SDA上的字节长度必须为8位，并且每个字节后须跟一个ACK位。 
数据在SCL处于低电平时放到SDA上，并在SCL变为高电平后进行采样。读写数据和SCL上升沿之间的时间间隔是由总线上的设备自己定义的，不同芯片可能有差异。 

![I2C数据传输的时序图](/img/20170820192701519.png)

开始条件（start condition）： 
为了标识传输正式启动，master设备会将SCL置为高电平（当总线空闲时，SDA和SCL都处于高电平状态），然后将SDA拉低，这样，所有slave设备就会知道传输即将开始。如果两个master设备在同一时刻都希望获得总线的所有权，那么谁先将SDA拉低，谁就赢得了总线的控制权。在整个通信期间，可以存在多个start来开启每一次新的通信序列（communication sequence），而无需先放弃总线的控制权，后面会讲到这种机制。 

地址帧（address frame）： 
地址帧总是在一次通信的最开始出现。一个7-bit的地址是从最高位（MSB）开始发送的，这个地址后面会紧跟1-bit的操作符，1表示读操作，0表示写操作。 
接下来的一个bit是NACK/ACK，当这个帧中前面8bits发送完后，接收端的设备获得SDA控制权，此时接收设备应该在第9个时钟脉冲之前回复一个ACK（将SDA拉低）以表示接收正常，如果接收设备没有将SDA拉低，则说明接收设备可能没有收到数据（如寻址的设备不存在或设备忙）或无法解析收到的消息，如果是这样，则由master来决定如何处理（stop或repeated start condition）。 

数据帧（data frames）： 
在地址帧发送之后，就可以开始传输数据了。Master继续产生时钟脉冲，而数据则由master（写操作）或slave（读操作）放到SDA上。每个数据帧8bits，数据帧的数量可以是任意的，直到产生停止条件。每一帧数据传输（即每8-bit）之后，接收方就需要回复一个ACK或NACK（写数据时由slave发送ACK，读数据时由master发送ACK。当master知道自己读完最后一个byte数据时，可发送NACK然后接stop condition）。 

停止条件（stop condition）： 
当所有数据都发送完成时，master将产生一个停止条件。停止条件定义为：在SDA置于低电平时，将SCL拉高并保持高电平，然后将SDA拉高。 
注意，在正常传输数据过程中，当SCL处于高电平时，SDA上的值不应该变化，防止意外产生一个停止条件。 

重复开始条件（repeated start condition）： 
有时master需要在一次通信中进行多次消息交换（例如与不同的slave传输消息，或切换读写操作），并且期间不希望被其他master干扰，这时可以使用“重复开始条件” —— 在一次通信中，master可以产生多次start condition，来完成多次消息交换，最后再产生一个stop condition结束整个通信过程。由于期间没有stop condition，因此master一直占用总线，其他master无法切入。 
为了产生一个重复的开始条件，SDA在SCL低电平时拉高，然后SCL拉高。接着master就可以产生一个开始条件继续新的消息传输（按照正常的7-bit/10-bit地址传输时序）。





----

> https://blog.csdn.net/jasonchen_gbd/article/details/77431951

<!-- README.md ends here -->
