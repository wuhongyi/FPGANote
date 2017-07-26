<!-- README.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 一 7月 17 22:47:08 2017 (+0800)
;; Last-Updated: 二 7月 25 13:25:59 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 3
;; URL: http://wuhongyi.cn -->

# Quartus II

## 必装组件：
```
Quartus II
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/QuartusSetup-15.0.0.145-linux.run   2.3GB
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/QuartusHelpSetup-15.0.0.145-linux.run    380MB
```

## 选装组件：

```
器件库（不用全装，用哪个系列的器件就安装哪个系列的器件库）
Arria II
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/arria-15.0.0.145.qdz    665MB
Arria 10
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/arria10_part1-15.0.0.145.qdz   2.7GB
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/arria10_part2-15.0.0.145.qdz   3.4GB
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/arria10_part3-15.0.0.145.qdz   2.7GB
Arria V
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/arriav-15.0.0.145.qdz      1.3GB
Arria V GZ
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/arriavgz-15.0.0.145.qdz       1.9GB
Cyclone IV
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/cyclone-15.0.0.145.qdz      464MB
Cyclone V
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/cyclonev-15.0.0.145.qdz     1.1GB
MAX II,MAX V
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/max-15.0.0.145.qdz      11.3MB
MAX 10
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/max10-15.0.0.145.qdz    295MB
Stratix IV
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/stratixiv-15.0.0.145.qdz    535MB
Stratix V
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/stratixv-15.0.0.145.qdz     2.8GB


DSP Builder（是MATLAB的插件，可以不装，主要用于信号处理类产品开发）
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/DSPBuilderSetup-15.0.0.145-linux.run    63MB

SOC（必须装才能开发集成高性能硬核Cortex-A的SOC FPGA，内含全世界最厉害的ARM开发工具，来自ARM公司的DS-5安装包）
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/SoCEDSSetup-15.0.0.145-linux.run     2.3GB

JNEye（可以不装，用于FPGA高速收发器的PCB级的仿真和分析，不用FPGA的高速收发器，就不用安装这个工具）
无Linux版

Altera OpenCL（用C语言开发FPGA的工具，可以不装，主要用于信号处理和科学计算类产品开发）
Altera SDK for OpenCL
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/AOCLSetup-15.0.0.145-linux.run    273MB
Altera Runtime Environment for OpenCL Linux x86-64 RPM
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/aocl-rte-15.0.0-1.x86_64.rpm   612KB
Altera Runtime Environment for OpenCL Linux PowerPC RPM
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/aocl-rte-15.0.0-1.ppc64.rpm    480KB
Altera Runtime Environment for OpenCL Linux Cyclone V SoC TGZ
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/aocl-rte-15.0.0-1.arm32.tgz    706KB
Altera Runtime Environment for OpenCL Windows x86-64
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/aocl-rte-15.0.0.145-windows.exe     8.9MB

ModelSim AE（可以不装AE版，推荐更好的ModelSim SE版，可去Mentor官方网站下载软件对应的SE版本10.3d再去找Crack，SE的破解器也可以用在AE上）
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/ModelSimSetup-15.0.0.145-linux.run    1.1GB

Quartus II Programmer（建议工厂烧写流水线上安装，普通开发者不要安装，因为Quartus II已经集成了此工具）
http://download.altera.com/akdlm/software/acdsinst/15.0/145/ib_installers/QuartusProgrammerSetup-15.0.0.145-linux.run   692MB
```

硬盘空间：完全安装Altera全部设计套装 v15.0 对于您要安装软件的硬盘或者分区，大约需要31GB的可用硬盘空间。
操作系统要求：必须是64位的Linux操作系统，Altera推荐RHEL 5或者6。

----

将要安装的包下载到同一个文件夹内

```bash
chmod 774 QuartusSetup-15.0.0.145-linux.run
./QuartusSetup-15.0.0.145-linux.run
#设置安装路径，默认会将该文件夹内的说有包都安装了
```


安装Quartus II 15.0后（Linux版本），破解方法如下：

- 第一步： 把Crack_QII_15.0_Linux.zip里面的libgcl_afcq.so和libsys_cpt.so文件分别解压缩后，替换/path_to/altrea/15.0/quartus/linux64里面的同名文件，这样2个so文件里面的加密点就全部被破解了。
- 第二步： 把license.dat里的XXXXXXXXXXXX 用你的网卡号替换(在Quartus II 15.0的Tools菜单下选择License Setup，下面就有NIC ID)。
- 第三步： 在Quartus II 15.0的Tools菜单下选择License Setup，然后选择License file，最后点击OK。
- 注意：license文件存放的路径名称不能包含汉字和空格，空格可以用下划线代替。



<!-- README.md ends here -->
