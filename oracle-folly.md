## Ubuntu20.04-LTS下配置occi(21_6)和folly(2017.12)环境

#### 1.安装gcc

```bash
sudo apt update 

sudo vim /etc/apt/sources.list

#添加源
sudo vim /etc/apt/sources.list
#加入
deb http://dk.archive.ubuntu.com/ubuntu/ xenial main
deb http://dk.archive.ubuntu.com/ubuntu/ xenial universe
sudo apt update

#安装
sudo apt install gcc-4.9

sudo apt install g++-4.9

#降级
cd /usr/bin

rm gcc

ln -s gcc-4.9 gcc
```

#### 2.安装folly依赖

```bash

sudo apt-get install \
    g++ \  4.9
    automake \  
    autoconf \  
    autoconf-archive \  
    libtool \  
    libevent-dev \
    libdouble-conversion-dev \
    liblz4-dev \
    liblzma-dev \
    libsnappy-dev \
    make \  
    zlib1g-dev \ 
    binutils-dev \
    libjemalloc-dev \
    libssl-dev \
    pkg-config \
    libiberty-dev
```

#### 3.安装googletest

```bash

  (cd folly/test && \
     rm -rf gtest && \
     wget https://github.com/google/go
     ogletest/archive/release-1.8.0.tar.gz && \
     tar zxf release-1.8.0.tar.gz && \
     rm -f release-1.8.0.tar.gz && \
     mv googletest-release-1.8.0 gtest)
```

#### 4.安装gflag和glog

```bash
#安装ccmake
sudo apt install cmake-curses-gui

git clone gflags
ccmake your gflags and configure to build gflags with shared lib.
cmake, make and sudo make install your gflags
git clone glog
export LDFLAGS='-L/usr/local/lib' # since my gflags lib is installed under /usr/local/lib
cd ${your_glog_folder} && ./configure && make
make install

```

#### 5.安装boost-1.51

```bash
./bootstrap.sh 
./b2 cxxflags="-std=c++14"
sudo ./b2 install 

```

#### 6.修改配置

```bash
sudo vim /etc/ld.so.conf
#添加
/usr/lib /usr/local/lib
```

#### 7.安装folly

```bash
  autoreconf -ivf
  ./configure
  make
  make check
  sudo make install
```







