# svp-on-ubuntu

Verified on Ubuntu 20.04.2 Focal

update your drivers

```bash
$ ubuntu-drivers devices
$ sudo ubuntu-drivers autoinstall # autoinstall nvidia drivers
# reboot
$ nvidia-settings --version

nvidia-settings:  version 440.82
  The NVIDIA X Server Settings tool.

  This program is used to configure the NVIDIA Linux graphics driver.
  For more detail, please see the nvidia-settings(1) man page.
```

install tools for compiling C/C++ source code

```bash
$ cat ./tools/Aptfile | xargs sudo apt install -y
```

install qt5, (optionally) qt5 docs and examples 
[[source](https://stackoverflow.com/a/48147461)]

```bash
$ cat ./qt5/Aptfile | grep "^[^#]" | xargs sudo apt install -y
# verify qt
$ which qmake
$ qmake --version
```

build and install zimg

```bash
# add `export MAKEFLAGS=-j8` to ~/.bashrc
$ sudo apt install libtool
$ curl -OL https://github.com/sekrit-twc/zimg/archive/refs/tags/release-3.0.1.tar.gz
$ tar -zxvf release-3.0.1.tar.gz
$ mv zimg-release-3.0.1 ~/zimg-v3.0.1
$ cd ~/zimg-v3.0.1
$ ./autogen.sh
$ ./configure
$ make
$ sudo make install
$ sudo checkinstall
```

build imagemagick from source

```bash
$ sudo apt install libjpeg-dev
$ cd ~
$ curl -OL https://github.com/ImageMagick/ImageMagick/archive/refs/tags/7.0.11-13.tar.gz
$ tar -zxvf 7.0.11-13.tar.gz
$ cd ImageMagick-7.0.11-13
$ ./configure --with-modules
$ make
$ sudo make install
# add the following to ~/.bashrc
LD_LIBRARY_PATH="${LD_LIBRARY_PATH:+$LD_LIBRARY_PATH:}/usr/local/lib:/usr/local/lib/ImageMagick-7.0.11/modules-Q16HDRI/coders:/usr/local/lib/ImageMagick-7.0.11/modules-Q16HDRI/filters"
export LD_LIBRARY_PATH
```

install ffmpeg and support libraries

```bash
$ cat ./ffmpeg/Aptfile | xargs sudo apt install -y
```

build VapourSynth

```bash
$ sudo apt install cython3 libass-dev libtesseract-dev
$ cd ~
$ curl -OL https://github.com/vapoursynth/vapoursynth/archive/refs/tags/R53.tar.gz
$ tar -zxvf R53.tar.gz
$ mv vapoursynth-R53 vapoursynth-53 # so that checkinstall doesn't complain about version #
$ cd vapoursynth-53
$ ./autogen.sh
$ ./configure --enable-subtext --enable-imwri --enable-ocr
$ make
$ sudo make install
# add `/usr/local/lib/vapoursynth` to `LD_LIBRARY_PATH`, `export PYTHONPATH=/usr/local/lib/python3.8/site-packages` in ~/.bashrc
$ sudo checkinstall
$ vspipe --version
```

build and install nv-codec-headers

```bash
git clone https://git.videolan.org/git/ffmpeg/nv-codec-headers.git
cd nv-codec-headers
make && sudo make install
```

install meson and ninja

```bash
# add ~/.local/bin to PATH, then
$ pip3 install --user meson ninja
```

build cmake

```bash
$ sudo apt install libssl-dev
$ cd ~
$ curl -OL https://github.com/Kitware/CMake/releases/download/v3.20.3/cmake-3.20.3.tar.gz
$ tar -zxvf cmake-3.20.3.tar.gz
$ cd cmake-3.20.3
$ ./bootstrap
$ make
$ sudo make install
$ sudo checkinstall
```

build and install mujs

```
$ sudo apt install libreadline-dev
$ cd ~
$ curl -OL https://mujs.com/downloads/mujs-1.1.2.tar.gz
$ tar -zxvf mujs-1.1.2.tar.gz
$ cd mujs-1.1.2
$ make
$ sudo make install
$ sudo checkinstall
```

build and install mpv
[[source](https://github.com/mpv-player/mpv/#compilation)]

```bash
$ sudo apt install lua5.1-0-dev libplacebo-dev libbluray-dev libcddb2-dev
$ cd ~
$ curl -OL https://github.com/mpv-player/mpv/archive/refs/tags/v0.33.1.tar.gz
$ tar -zxvf v0.33.1.tar.gz
$ cd mpv-0.33.1
$ ./bootstrap.py
$ ./waf configure --enable-alsa --enable-vapoursynth --enable-javascript
$ sudo ./waf install
$ echo "input-ipc-server=/tmp/mpvsocket" > ~/.config/mpv/mpv.conf
```

install mpv plugins

```bash
$ pip3 install mplug
$ mplug install autocrop
$ mplug install autodeint
$ mplug install Anime4K
```

install svp: https://www.svp-team.com/get/

---

other fun stuff...

install makemkv [[source](https://ubuntuhandbook.org/index.php/2019/09/install-makemkv-snap-ubuntu-18-04-19-04/)]

```bash
$ sudo add-apt-repository ppa:heyarje/makemkv-beta
$ sudo apt update
$ sudo apt install makemkv-bin makemkv-oss
```

install avisynth: https://avs-plus.net/

```bash
$ mkdir build && cd build
$ cmake ..
$ sudo make install
$ sudo checkinstall
```
