# Compile OpenWrt firmware(No GL.iNet packages)

1. Run `git clone https://github.com/gl-inet/gl-infra-builder.git && cd gl-infra-builder` to clone repository

2. Run `ls configs -hl` to list the openwrt verizon

3. Chose your want version, for example, if you want to use openwrt-21.02.2, Run `python3 setup.py -c configs/config-21.02.2.yml` to download openwrt-21.02.2 source code

4. Run `cd openwrt-21.02/openwrt-21.02.2` to enter openwrt-21.02.2 directory

5. Run `./scripts/gen_config.py list` to get target_xxx and glinet_xxx files. target_xxx is you want to compile products, don't modify. glinet_xxx is you want to add/delete packages, you can modify. Those files in the **profiles** directory.

6. Run `./scripts/gen_config.py <target_profile> <function_profile>` to chose the product target and add some packages. <target_profile> is you want to compile products. <function_profile> is you want to add/delete packages. 

7. For example, If you want to compile GL-A1300 product and add luci, you can run `./scripts/gen_config.py target_ipq40xx_gl-a1300 luci`. You can run `make menuconfig` to chose other packages

8. Run `make` to build your firmware.

# Compile GL.iNet standard firmware

9. Base on the steps above, at openwrt-21.02/openwrt-21.02.2 directory, run `git clone https://github.com/gl-inet/glinet4.x.git` to get GL.iNet packages.

10. Run `./scripts/gen_config.py target_ipq40xx_gl-a1300 glinet_depends` to add A1300 GL.iNet packages

11. Run ` make V=s -j5 GL_PKGDIR=`pwd`/glinet4.x/ipq40xx/`  to compile GL.iNet standard firmware.

# Example compile firmware

## 0.Compile 360T7（2023.2.27）

0.0

with gl-inet package installed,original partition is not big enough,you should flash the bl blow.

https://github.com/hanwckf/bl-mt798x

1.1  Compile 360t7-108M OpenWrt firmware(No GL.iNet packages)

```
 git clone https://github.com/FUjr/gl-infra-builder && cd gl-infra-builder
 # 如果没有git账户，务必执行
 git config --global user.email 'youremail.com'
 git config --global user.name 'your name'
```

```
 python3 setup.py -c configs/config-mt798x-7.6.6.1.yml && cd mt7981
```

```
 ./scripts/gen_config.py target_mt7981_360t7-108M luci
 # 增删插件（可选）
 make manuconfig   # 错误
 cd work/openwrt-64/openwrt-64/gl-infra-builder/mt7981
```

1.2 Compile 360t7-108M GL.iNet standard firmware

```
 git clone https://github.com/gl-inet/glinet4.x.git
```

```
 cp ./glinet4.x/pkg_config/gl_pkg_config_mt3000.mk  ./glinet4.x/mt7981/gl_pkg_config.mk
```

```
 ./scripts/gen_config.py target_mt7981_360t7-108M glinet_depends
```

```
 make -j2 GL_PKGDIR=`pwd`/glinet4.x/mt7981/ | make -j1 V=s GL_PKGDIR=`pwd`/glinet4.x/mt7981/
```

## 

