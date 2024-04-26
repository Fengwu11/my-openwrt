# my-openwrt
上面存放着些自己编译openwrt的配置文件

### 注意
编译时最好"全局上网"  
默认登陆IP 192.168.1.1 密码 password  

### 根据lede源码 编译openwrt
1.安装依赖
```bash
sudo apt update -y
sudo apt full-upgrade -y

sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
bzip2 ccache cmake cpio curl device-tree-compiler fastjar flex gawk gettext gcc-multilib g++-multilib \
git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libfuse-dev libglib2.0-dev libgmp3-dev \
libltdl-dev libmpc-dev libmpfr-dev libncurses5-dev libncursesw5-dev libpython3-dev libreadline-dev \
libssl-dev libtool lrzsz mkisofs msmtp ninja-build p7zip p7zip-full patch pkgconf python2.7 python3 \
python3-pyelftools python3-setuptools qemu-utils rsync scons squashfs-tools subversion swig texinfo \
uglifyjs upx-ucl unzip vim wget xmlto xxd zlib1g-dev

sudo apt -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev \
patch python3 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib \
p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool \
autopoint device-tree-compiler g++-multilib antlr3 gperf wget curl swig rsync aria2 ca-certificates python3-pyelftools \
python3-setuptools yasm libpython3-dev
```

2.下载lede源码
```bash
git clone https://github.com/coolsnowwolf/lede
cd lede
```

3.选择配置
```bash
cp openwrt-config-raspi4b/feeds.conf.default ./feeds.conf.default -f    #使用上面的配置文件，也可以使用默认的配置文件
cp openwrt-config-raspi4b/config ./.config -f

./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
```

4.下载dl库、编译固件(第一次建议单线程编译)
```bash
make download -j8
make V=s -j$(nproc)
```
