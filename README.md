# minieap for OpenWrt

## Build

First download [OpenWrt SDK](https://downloads.openwrt.org/) for your device.

```sh
cd /path/to/your/sdk
git clone https://github.com/Undefined443/openwrt-minieap-sysu package/minieap
make menuconfig # choose `minieap` in section `Network`
make package/minieap/compile V=s
```
