# minieap for OpenWrt

![Build Status](https://github.com/NaClLuo/openwrt-minieap-sysu/actions/workflows/build.yml/badge.svg)

minieap 的中山大学适配版，已在东校园至善园稳定运行一学年。

## Automated Builds

本仓库已配置自动化构建，支持多种路由器架构：

- **MediaTek MT7622** (ImmortalWrt) - 适用于小米路由器 4、红米路由器 AC2100 等
- **x86_64** (OpenWrt) - 适用于 PC 软路由、虚拟机等  
- **Ramips MT7621** (OpenWrt) - 适用于小米路由器 3G、4A 千兆版等
- **ARMv8 Cortex-A53** (OpenWrt) - 适用于树莓派 3B+ 等

### 下载预编译包

1. 访问 [Actions 页面](https://github.com/NaClLuo/openwrt-minieap-sysu/actions)
2. 点击最新的成功构建
3. 在 "Artifacts" 部分下载对应架构的 `.ipk` 文件
4. 上传到路由器并安装：`opkg install minieap*.ipk`

### 自动构建触发条件

- 推送到 main/master 分支
- 创建 Pull Request
- 手动触发（Repository → Actions → Build minieap for OpenWrt → Run workflow）

## Build

### 方式一：下载预编译包（推荐）

见上方 [自动构建](#automated-builds) 部分，直接下载对应架构的预编译 `.ipk` 包。

### 方式二：手动编译

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
