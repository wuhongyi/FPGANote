<!-- README.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 二 7月 25 09:42:16 2017 (+0800)
;; Last-Updated: 日 8月 13 20:35:11 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 24
;; URL: http://wuhongyi.cn -->

# Xilinx ISE

[Xilinx13.4调试环境安装步骤](http://wuhongyi.cn/FPGANote/pdf/XilinxISE/Xilinx134调试环境安装步骤.doc)  
[XilinxFPGA开发实用教程第1版](http://wuhongyi.cn/FPGANote/pdf/XilinxISE/XilinxFPGA开发实用教程第1版.pdf)


## 下载安装包

到官网注册，然后下载linux版本的ISE14.7。

链接：  
http://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/design-tools.html 

## 安装

```bash
tar -xvf Xilinx_ISE_DS_Lin_14.7_1015_1.tar -C /home/wuhongyi/
cd /home/wuhongyi
Xilinx_ISE_DS_Lin_14.7_1015_1/xsetup
```

然后弹出的是图形化安装向导，选择安装路径，其它全部默认即可。本人安装在/home/wuhongyi/Xilinx下

## 激活

成功启动之后打开HELP菜单的Mange Licence子项，然后再弹出的窗口中点击Load Licence然后弹出的浏览窗口中选择你的licence即可。或者将Licence文件放在用户目录下 .Xlinix 文件夹中。


## 启动软件

加载配置脚本

```bash
source settings64.sh  #该脚本在 /home/wuhongyi/Xilinx/14.7/ISE_DS/ 目录下
```

加载脚本之后

```bash
ise
```

----

[新建工程示例](http://blog.csdn.net/lishengbo/article/details/51113794)  
[Xilinx ISE12.0 烧录步骤](http://xilinx.eetrend.com/forum/6824)  

[UCF文件中时序约束的语法](http://blog.sina.com.cn/s/blog_62c7814b0101jma7.html)  
[ISE 约束文件 *.ucf的写法](http://www.360doc.com/content/14/1030/15/4077337_421173478.shtml)
[ISE中UCF约束文件的编写](http://blog.csdn.net/ladywn/article/details/34531871)

----

工程文件

```
*.xise

*.vhd
*.ucf


*.bit
*.mcs
```

----

## 其它暂放材料

[ISE中Xilinx全局时钟系统的设计](http://blog.sina.com.cn/s/blog_bff0927b010173bp.html)  
[DCM 学习 设计](http://xjhit.spaces.eepw.com.cn/articles/article/item/73904)  
[Xilinx的时钟资源](http://xilinx.eetop.cn/viewnews-1632)
[《Xilinx可编程逻辑器件设计与开发（基础篇）》连载11：Spartan-6的时钟管理器（CMT）](http://xilinx.eetrend.com/blog/1941)
[ISE11 中DCM的使用](https://wenku.baidu.com/view/58d7f40b76c66137ee06192d.html)

[FPGA的xilinx培训1](https://max.book118.com/html/2017/0616/115982247.shtm)

----

> http://www.cnblogs.com/tracyone/p/3561781.html
> http://blog.csdn.net/weiweiliulu/article/details/23351429
> http://blog.sina.com.cn/s/blog_98740ded0101jxt8.html



<!-- README.md ends here -->
