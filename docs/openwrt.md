# Openwrt usage snippts
## Build a customized image

* Clone the repository  
```html
git clone https://git.openwrt.org/openwrt/openwrt.git
```
* Checkout out the target branch tag  
```html
git checkout v22.03.2
```
* Add some custom source to *feeds.conf.default*
```html linenums="1"
src-git-full packages https://git.openwrt.org/feed/packages.git^dba8a0102e5965cad58a871335002e9c964b6719
src-git-full luci https://git.openwrt.org/project/luci.git^96ec0cd3ccfe954f13fd5a337efdd70374dde03f
src-git-full routing https://git.openwrt.org/feed/routing.git^85028704f688a6768d3f10d5d3c10a799a121e0d
src-git-full telephony https://git.openwrt.org/feed/telephony.git^1d2031a5c82816483c51bca15649e2957fbe2bc2
src-git kenzo https://github.com/kenzok8/openwrt-packages
src-git small https://github.com/kenzok8/small

```
* Feeds update & install
```html
./scripts/feeds update -a
./scripts/feeds install -a
```
* Get *config.buildInfo* from openwrt org which contains the arch configuration compatible with your target device
```html
wget https://downloads.openwrt.org/releases/22.03.2/targets/bcm27xx/bcm2711/config.buildinfo -O .config
```
The *config.buildInfo* file is renamed to *.config*.

* Append more default build configurations to .config
```html
make defconfig  //append default config to .config
```
The command above add more default compile configuration for the target arch into *.config* file. 

* Customize the compile configuration
```html
make menuconfig
```
The command loads the *.config*, we now can do some customized update and save to overwrite *.config* file.  
-  User should first add third-part src to feeds.conf.default in step 3, or the third part packages wont display in menuconfig  
- Set the rootfs size bigger, or it may run out of space to install too many third-part packages.  
- Some common known packages conflicts: **dnsmasq**  and **dnsmasq-full**, unselect **dnsmasq** before select **dnsmasq-full**.

* Download dependent resource and compile
```html
make download
make -j world
```

* Clean
```html
make clean //remove the target
make dirclean //remove target, toolchain, tools, cache
make distclean //remove target, toolchain, tools, cache, config, download
```

## Build single package
Select the package to compile in make menuconfig, or the make package/../compile wont acturely compile the package
Remove tmp directory before compile
Run compile
```html
make package/../compile 
```
Find the output packages in *bin/packages* directory

## References
1. https://openwrt.org/docs/guide-developer/toolchain/single.package
2. https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem  
3. https://downloads.openwrt.org/releases/22.03.2/targets/bcm27xx/bcm2711/
