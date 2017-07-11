# Android编译源代码，烧录到Hikey960开发板

##编译环境

Android Sdk 25(Nougat 7.1.1)
Ubuntu 16.04
------------------------
##参考资料
-----------------------
Google官方资料（中英文版有差距，最好是英文版）:https://source.android.com/source/

Alpha Star极客社区（诚迈科技）:https://bbs.alpha-star.org/%E8%BD%AF%E4%BB%B6%E4%BA%A4%E6%B5%81/hikey960-%E6%BA%90%E7%A0%81%E4%B8%8B%E8%BD%BD%EF%BC%8C%E7%BC%96%E8%AF%91%E4%B8%8E%E7%83%A7%E5%BD%95
----------------------------
##步骤

一、先翻墙！

      我用的是shadowsocks-QT5

二、准备编译环境

1、jdk：根据google官方文档说明，如果Ubuntu>=15.04使用jdk8

sudo apt-get install openjdk-8-jdk

2、安装所需程序包： 

sudo apt-get install git-core gnupg flex bison gperf build-essential \

zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 \

lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache \

libgl1-mesa-dev libxml2-utils xsltproc unzip

3、配置USB使用权限（可放在烧录到开发板时在执行）

注：我在使用google文档上给出的命令时，下载不下来，所以采用的以下方法

直接打开浏览器下载：http://source.android.com/source/51-android.txt

修改文件里面的用户名：sed -i "s/<username>/$USER/"

拷贝文件的内容

在/etc/udev/rules.d目录下新建文件51-android.rules

sudo udevadm control --reload-rules

4、使用单独的输出目录（所有编译的输出都会在源代码目录下的/out文件夹内，这部可以选择性设置）

export OUT_DIR_COMMON_BASE=路径名

三、下载源代码

安装repo

mkdir ~/bin

PATH=~/bin:$PATH

curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo

chmod a+x ~/bin/repo

初始化Repo

mkdir WORKING_DIRECTORY（名自取）

cd WORKING_DIRECTORY

git config --global user.name "Your Name"

git config --global user.email "you@example.com"

开始下载源代码（耗时）

repo init -u https://android.googlesource.com/platform/manifest

repo init -u https://android.googlesource.com/platform/manifest -master

repo sync

四、下载hikey960专有二进制文件

wget https://dl.google.com/dl/android/aosp/arm-hikey960-NOU-7ad3cccc.tgz

tar xzf arm-hikey960-NOU-6eafa750.tgz

./extract-arm-hikey960.sh

wget https://dl.google.com/dl/android/aosp/hisilicon-hikey960-NOU-5db76395.tgz

tar xzf hisilicon-hikey960-NOU-5db76395.tgz

$ ./extract-hisilicon-hikey960.sh

五、编译hikey960源代码（耗时）

. ./build/envsetup.sh

lunch hikey960-userdebug

make -j32

六、烧录到开发板

1.设置拨码开关1/3为ON,使HiKey960进入fastboot mode；

2.HiKey960供电

3.烧录android初始镜像:

cd device/linaro/hikey/installer/hikey960

./flash-all.sh

4.设置拨码开关3为OFF后，HiKey960重新供电 。
