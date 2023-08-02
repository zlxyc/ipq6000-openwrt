源码fork 自L大 https://github.com/coolsnowwolf/openwrt-gl-ax1800

## 注意

1. **不要用 root 用户进行编译**
2. 国内用户编译前最好准备好梯子
3. 默认登陆IP 192.168.1.1 

## 编译命令

1. 首先装好 Linux 系统， Ubuntu 22.04 LTS

2. 安装编译依赖

   ```
   sudo apt update -y
   sudo apt full-upgrade -y
   sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
   bzip2 ccache cmake cpio curl device-tree-compiler fastjar flex gawk gettext gcc-multilib g++-multilib \
   git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libglib2.0-dev libgmp3-dev libltdl-dev \
   libmpc-dev libmpfr-dev libncurses5-dev libncursesw5-dev libreadline-dev libssl-dev libtool lrzsz \
   mkisofs msmtp nano ninja-build p7zip p7zip-full patch pkgconf python2.7 python3 python3-pip libpython3-dev qemu-utils \
   rsync scons squashfs-tools subversion swig texinfo uglifyjs upx-ucl unzip vim wget xmlto xxd zlib1g-dev
   ```

3. 下载源代码，更新 feeds 并选择配置

   ```
   git clone https://github.com/zlxyc/ipq6000-openwrt.git
   cd ipq6000-openwrt
   ./scripts/feeds update -a && ./scripts/feeds install -a
   make menuconfig
   ```

4. 下载 dl 库，编译固件
（-j 后面是线程数，推荐用单线程）

   ```
   make download -j8
   make -j1 V=s
   ```

5. 二次编译：

   ```
   cd ipq6000-openwrt
   git pull
   ./scripts/feeds update -a && ./scripts/feeds install -a
   rm -rf .config
   make menuconfig
   make -j1 V=s
   ```

6. 编译完成后输出路径：bin/targets
