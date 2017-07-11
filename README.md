# Android编译源代码，烧录到Hikey960开发板
编译环境
Android Sdk 25(Nougat 7.1.1)
Ubuntu 16.04
参考资料
Google官方资料（中英文版有差距，最好是英文版）:https://source.android.com/source/
Alpha Star极客社区（诚迈科技）:https://bbs.alpha-star.org/%E8%BD%AF%E4%BB%B6%E4%BA%A4%E6%B5%81/hikey960-%E6%BA%90%E7%A0%81%E4%B8%8B%E8%BD%BD%EF%BC%8C%E7%BC%96%E8%AF%91%E4%B8%8E%E7%83%A7%E5%BD%95
一、先翻墙！
一、准备编译环境
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
      sed -i "s/<username>/$USER/"
      copy 51-android.txt /
      4、使用单独的输出目录（所有编译的输出都会在源代码目录下的/out文件夹内，这部可以选择性设置）
二、下载源代码
三、编译源代码
四、烧录到开发板
