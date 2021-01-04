## 一、下载

### 从官网下载：

```
wget https://download.qemu.org/qemu-5.2.0.tar.xz
tar xvJf qemu-5.2.0.tar.xz
cd qemu-5.2.0
```



### 从GitHub上下载：

```
git clone https://git.qemu.org/git/qemu.git
cd qemu
git submodule init
git submodule update --recursive
```



## 二、安装ninja

Ninja 是Google的一名程序员推出的注重速度的构建工具，一般在Unix/Linux上的程序通过make/makefile来构建编译，而Ninja通过将编译任务并行组织，大大提高了构建速度，而qemu现在采用的是基于ninja的构建系统，所以我们得先安装ninja

构造Ninja可使用CMake或python，需要先安装re2c：

```
apt install re2c
```

re2c安装成功之后开始Ninja安装。

Ninja编译：

```
git clone git://github.com/ninja-build/ninja.git && cd ninja
./configure.py --bootstrap
cp ninja /usr/bin/
```

安装成功之后使用ninja --version可查看安装的版本：

```
ninja --version
1.9.0
```

## 三、编译QEMU

安装依赖：

```
apt install pkg-config libglib2.0-dev libmount-dev python3 python3-pip python3-dev git libssl-dev libffi-dev build-essential autoconf automake libfreetype6-dev libtheora-dev libtool libvorbis-dev pkg-config texinfo zlib1g-dev unzip cmake yasm libx264-dev libmp3lame-dev libopus-dev libvorbis-dev libxcb1-dev libxcb-shm0-dev libxcb-xfixes0-dev pkg-config texinfo wget zlib1g-dev libpixman-1-0-dev
```

编译：

```
./configure
make
```

## 四、安装QEMU

```
make install 
```

查看安装版本：

```
root@60247decd218:~/qemu/qemu-5.2.0# qemu-arm --version
qemu-arm version 5.2.0       
```

## 五、容易出现的错误

5.1 ERROR: pkg-config binary ‘pkg-config’ not found

```
apt install pkg-config
```

5.2 ERROR: glib-2.48 gthread-2.0 is required to compile QEMU

```
apt-get install libglib2.0-dev
```

5.3 ERROR: Dependency “pixman-1” not found, tried pkgconfig

```
apt-get install libmount-dev
```