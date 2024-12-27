# minieap for OpenWrt

minieap 的 SYSU 适配版，已在东校园至善园测试。目前稳定运行一学期。

## Build

1. 安装依赖：

   ```sh
   sudo apt update -y
   sudo apt full-upgrade -y
   sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
     bzip2 ccache clang cmake cpio curl device-tree-compiler ecj fastjar flex gawk gettext gcc-multilib \
     g++-multilib git gnutls-dev gperf haveged help2man intltool lib32gcc-s1 libc6-dev-i386 libelf-dev \
     libglib2.0-dev libgmp3-dev libltdl-dev libmpc-dev libmpfr-dev libncurses5-dev libncursesw5 \
     libncursesw5-dev libpython3-dev libreadline-dev libssl-dev libtool lld llvm lrzsz mkisofs msmtp \
     nano ninja-build p7zip p7zip-full patch pkgconf python2.7 python3 python3-pip python3-ply \
     python3-docutils python3-pyelftools qemu-utils re2c rsync scons squashfs-tools subversion swig \
     texinfo uglifyjs upx-ucl unzip vim wget xmlto xxd zlib1g-dev zstd
   ```

2. 下载对应路由器型号的 SDK [OpenWrt SDK](https://downloads.openwrt.org/)

3. 编译

   ```sh
   cd /path/to/your/sdk
   git clone https://github.com/Undefined443/openwrt-minieap-sysu package/minieap
   make menuconfig # choose `minieap` in section `Network`
   make package/minieap/compile V=s
   ```
