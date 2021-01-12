## Leanote: 

### 错误1： 

#### error log:

```
error while loading shared libraries: libgconf-2.so.4: cannot open shared object file: No such file or directory
```

#### solutions:

```
sudo apt-get install libgconf-2-dev
```

### 错误2：

#### error log:

```
Failed to load module "canberra-gtk-module"
```

#### solutions:

```
sudo apt-get install libcanberra-gtk-module
```

## Thunderbird

### 错误：

#### error log:

```
下列软件包有未满足的依赖关系：
 thunderbird-locale-zh-hant : 依赖: thunderbird (< 1:52.7.0+build1-0ubuntu1.1~) 但是 1:68.10.0+build1-0ubuntu0.18.04.1 正要被安装
E: 无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。
```



#### solutions:

去下面这个网址，下载对应的安装包安装；
https://www.ubuntuupdates.org/package/core/bionic/main/updates/thunderbird-locale-zh-hant

## 编译相关

### 错误1：

#### error log:

```
error: possibly undefined macro: AC_DEFINE
      If this token and others are legitimate, please use m4_pattern_allow.
      See the Autoconf documentation.
```



#### soutions:

若是ubuntu下：

```
sudo apt-get install libtool  libsysfs-dev

```

若是Centos下：

```
yum install libtool libsysfs 

```

错误2：



## error log:

### openssl/bio.h: 没有那个文件或目录

#### soutions:

出现这个或者fatal error: openssl/名单.h: No such file or directory。都是没有安装libssl-dev

使用sudo apt-get install libssl-dev来安装libssl-dev即可



  GEN     ./Makefile
 *** Unable to find the ncurses libraries or the
 *** required header files.
 *** 'make menuconfig' requires the ncurses libraries.

***
 *** Install ncurses (ncurses-devel) and try again.

***

sudo apt-get install libncurses5-dev