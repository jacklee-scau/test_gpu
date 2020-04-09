# test_gpu
test device for gpu
#test_gpu.py脚本测试gpu是否可用
#若是运行脚本后打印gpu 则可用
#若是运行脚本后打印cpu 则不可用

#1 更新软件源
sudo vim /etc/apt/sources.list

#2 选择比较合适的源(选择一个即可）
#中科大
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
#阿里云
deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
#清华大学
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
#更新源
sudo apt-get update

#3 sources.list 换源  导入公钥验证签名
https://www.jianshu.com/p/7f04a4448634

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 76F1A20FF987672F #最后面公钥换成自己对应所缺的密钥

#4
卸载原驱动
sudo apt-get remove --purge nvidia*
#禁用nouveau
sudo gedit /etc/modprobe.d/blacklist.conf
#此时会打开一个文件，将文件末尾最后一行将nouveau添加加入黑名单
blacklist nouveau
#最后在终端输入
sudo update-initramfs -u

#5 安装显卡驱动
https://www.jianshu.com/p/f74d4534af80
https://blog.csdn.net/qq_42974800/article/details/100544112
#先到英伟达官网下载号对应的驱动
sudo chmod a+x NVIDIA-Linux-x86_64-418.67.run#换成自己的驱动 变成可执行文件

#开始安装 记得加 后缀-no-x-check -no-nouveau-check -no-opengl-files  防循环
 
sudo ./NVIDIA-Linux-x86_64-440.31.run -no-x-check -no-nouveau-check -no-opengl-files

#不行就换后缀   --add-this-kernel //尽量别用这个 不然nvidia-smi会有问题

sudo ./NVIDIA-Linux-x86_64-375.20.run --add-this-kernel
如果提示没有gcc g++ make 等依赖版本问题
gcc g++ 加入ppa源 装4.8版本

https://www.sysgeek.cn/ubuntu-install-gcc-compiler/

sudo apt install software-properties-common
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
#安装自己需要的版本
sudo apt install gcc-7 g++-7

#sudo apt-get install gcc
#sudo apt-get install make

#安装430驱动问题
https://blog.csdn.net/qq_41185868/article/details/97521492
#6
#cuda 官网
https://developer.nvidia.com/cuda-toolkit-archive
#选择cuda10  稳妥

cudnn :
https://developer.nvidia.com/rdp/cudnn-download
#选择7.6.5

#安装cuda cudnn
https://blog.csdn.net/weixin_44003563/article/details/90311584
#装上之后 配置环境变量
gedit ~/.bashrc
在最后写入并保存：
export CUDA_HOME=/usr/local/cuda
export PATH=$PATH:$CUDA_HOME/bin
export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

#使其生效
source ~/.bashrc
#查看是否生效
nvcc -V
#7
#安装cudnn
https://blog.csdn.net/qq_32408773/article/details/84112166?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task
#下载对应版本并解压 进入cuda文件夹 外面的目录 打开终端
sudo cp cuda/include/cudnn.h /usr/local/cuda/include/
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64/
sudo chmod a+r /usr/local/cuda/include/cudnn.h
sudo chmod a+r /usr/local/cuda/lib64/libcudnn*

#8
#在终端查看CUDNN版本：
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
#安装pycharm
https://blog.csdn.net/qq_15192373/article/details/81091278
#进入相应的bin目录
cd /home/lsx/software/pycharm-community-2019.3.3/bin
sudo sh ./pycharm.sh
#如果提示没有jdk
#则下载1.8的jdk
https://blog.csdn.net/qq_43158393/article/details/82825550?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

###############################
https://login.oracle.com/mysso/signon.jsp
931118435@qq.com
123456scAU
############################

#tw安装卸载
https://blog.csdn.net/xiaxuesong666/article/details/88013691
#安装deb
sudo dpkg -i teamviewer_14.0.xxxxx_i386.deb
#使用dpkg时，提示：dpkg：处理软件包XXX时出错：

sudo apt-get install -f
#等分析完之后，重新使用dpkg –i XXX.deb，就可以了（安装的文件少，不可以的没碰到呢）

#卸载命令
sudo apt --purge remove teamviewer

#gt710 驱动地址
https://www.geforce.cn/hardware/desktop-gpus/geforce-gt-710

# flatpak
https://blog.csdn.net/u011469138/article/details/82320761

#Ubuntu中使用dpkg安装deb文件提示依赖关系问题，仍未被配置，使用如下命令
sudo apt-get install -f

# ubuntu系统查看显卡驱动是否安装正确
https://www.cnblogs.com/kaishirenshi/p/12143962.html

sudo apt-get install mesa-utils
glxinfo | grep rendering


#安装pip 时候
#无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。（亲身体验）
https://blog.csdn.net/qq_40879809/article/details/88366788?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

#解决后
sudo apt install python-pip
#国内源清华镜像pip安装tensorflow-gpu 1.13.1
#先安装pip:
sudo apt-get install python-pip python-dev
#然后安装tensorflow-gpu 1.13.1:    
sudo python -m pip install -i https://pypi.tuna.tsinghua.edu.cn/simple tensorflow-gpu==1.13.1
#如果显存爆掉 mrmorr erro  则加后缀 --no-cache-dir 表示 安装 但不缓存
sudo python -m pip install -i https://pypi.tuna.tsinghua.edu.cn/simple tensorflow-gpu==1.13.1      	--no-cache-dir

#9
ubuntu python2和python3的切换
https://www.cnblogs.com/xia-Autumn/p/6683076.html
方法一：
echo alias python=python3 >> ~/.bashrc && source ~/.bashrc
相当于先打开gedit ~/.bashrc 修改alias python=python3这行内容

方法二（使用update-alternatives来修改priority）：
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 100
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 150

如果要切换到python2
sudo update-alternatives --config python
E: Sub-process /usr/bin/dpkg returned an error code (1)解决办法

https://blog.csdn.net/stickmangod/article/details/85316142?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

#解决锁
https://blog.csdn.net/qq_40879809/article/details/88366788?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

#pycharm连接器出错
https://blog.csdn.net/c_chuxin/article/details/82761486
import sys
sys.executable
#可以查看但前python连接器的位置
#如果pycharm还提示
ImportError: libcublas.so.10.0: cannot open shared object file: No such file

sudo ldconfig /usr/local/cuda-10.0/lib64

 gsettings-desktop-schemas : 破坏: mutter (< 3.31.4) 但是 3.28.4-0ubuntu18.04.1 正要被安装
E: 错误，pkgProblemResolver::Resolve 发生故障，这可能是有软件包被要求保持现状的缘故。

https://www.zhihu.com/question/55884688?sort=created
