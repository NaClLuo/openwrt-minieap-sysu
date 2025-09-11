# minieap for OpenWrt

minieap 的中山大学适配版，已在东校园至善园稳定运行一学年。

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

2. 下载对应路由器型号的 SDK：

   - [OpenWrt Firmware Selector](https://firmware-selector.openwrt.org/)
   - [ImmortalWrt Firmware Selector](https://firmware-selector.immortalwrt.org/)

   点击搜索结果下的文件夹图标，然后搜索 `sdk`，得到我们需要的 SDK 包，右键复制文件地址。

   ```sh
   wget https://downloads.immortalwrt.org/releases/24.10-SNAPSHOT/targets/mediatek/filogic/immortalwrt-sdk-24.10-SNAPSHOT-mediatek-filogic_gcc-13.3.0_musl.Linux-x86_64.tar.zst
   tar --zstd -xf immortalwrt-sdk-*.tar.zst && rm immortalwrt-sdk-*.tar.zst
   cd immortalwrt-sdk-*
   ```

3. 编译：

   ```sh
   git clone https://github.com/Undefined443/openwrt-minieap-sysu package/minieap
   make menuconfig # choose `minieap` in section `Network`
   make package/minieap/compile V=s
   ```

   查找编译产物位置：

   ```sh
   find . -name "minieap*.ipk"
   ```

4. 将编译得到的软件包上传到路由器，并安装：

   ```sh
   opkg install minieap*.ipk
   ```

5. 启动：

   ```sh
   minieap -u <username> -p <password> -n wan -w
   ```

参见：[使用 minieap 实现路由器锐捷认证上网 | 博客园](https://www.cnblogs.com/Undefined443/p/18375072)
