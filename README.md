[![CI](https://github.com/Mightnire/transmission-og/actions/workflows/ci.yml/badge.svg)](https://github.com/Mightnire/transmission-og/actions/workflows/ci.yml)
[![distcheck](https://github.com/Mightnire/transmission-og/actions/workflows/distcheck.yml/badge.svg)](https://github.com/Mightnire/transmission-og/actions/workflows/distcheck.yml)
[![stylecheck](https://github.com/Mightnire/transmission-og/actions/workflows/stylecheck.yml/badge.svg)](https://github.com/Mightnire/transmission-og/actions/workflows/stylecheck.yml)

# Transmission

Transmission is a fast, easy, and free BitTorrent client.

This repository maintains the rock-solid **Transmission 3.00 C codebase** (inheriting improvements from [Transmission OG](https://github.com/stefantalpalaru/transmission-og)), tailored for maximum stability, minimal memory usage, and seamless drop-in integration with embedded systems and Linux distributions.

It comes in several flavours:
* `transmission-daemon`: Headless daemon for servers, NAS, and embedded routers (Padavan, OpenWrt, etc.)
* `transmission-remote`: CLI client to control and manage `transmission-daemon`
* Standalone tools: `transmission-create`, `transmission-show`, `transmission-edit`
* GTK+ 3 and Qt GUI applications for desktop systems
* A built-in responsive Web UI for remote controlling any of the above

## Key Features & Highlights

* **Pure C Stability**: Preserves the lean, highly optimized C implementation before upstream's C++ rewrite, providing minimal RAM footprint and rock-solid reliability for 24/7 seedboxes and embedded routers.
* **Native Drop-In Replacement**: All `-og` binary prefixes and suffixes have been stripped. Standard binary names (`transmission-daemon`, `transmission-remote`, etc.) and standard config directories (`~/.config/transmission-daemon`) are used, allowing 100% transparent replacement for standard Transmission installations.
* **Standalone Release Archives**: Release tarballs (`transmission-*.tar.xz`, `*.tar.gz`) come pre-bundled with all essential third-party dependencies (`dht`, `libb64`, `libevent`, `libnatpmp`, `libutp`, `miniupnpc`), enabling instant offline compilation without recursive Git submodule fetches.

## Command Line Interface Notes

* `transmission-remote`: The primary CLI tool to control the running daemon.
* `transmission-show`: Inspect `.torrent` file metadata and file lists.
* `transmission-create`: Create new `.torrent` files with custom trackers and piece sizes.
* `transmission-edit`: Update announce URLs / trackers in existing `.torrent` files.
* `transmission-cli`: Standalone client limited to a single torrent at a time (deprecated, kept for legacy hardware compatibility).

## Building from source

### 1. Dependencies

#### Ubuntu / Debian:

```bash
sudo apt-get install --no-install-recommends -yq \
         build-essential \
         gettext \
         intltool \
         libayatana-appindicator3-dev \
         libcurl4-openssl-dev \
         libglib2.0-dev \
         libgtk-3-dev \
         libnotify-dev \
         libssl-dev \
         libsystemd-dev \
         qttools5-dev \
         zlib1g-dev
```

#### macOS (Homebrew):

```bash
export CPPFLAGS="${CPPFLAGS} -I/usr/local/opt/gettext/include"
export LDFLAGS="${LDFLAGS} -L/usr/local/opt/gettext/lib"
export PATH="${PATH}:/usr/local/opt/qt@5/bin:/usr/local/opt/gettext/bin"
export PKG_CONFIG_PATH=/usr/local/opt/qt@5/lib/pkgconfig:/usr/local/opt/openssl@1.1/lib/pkgconfig
export MACOSX_DEPLOYMENT_TARGET=12.0

brew install \
         autoconf \
         automake \
         cmake \
         gettext \
         gtk+3 \
         intltool \
         openssl@1.1 \
         pkg-config \
         qt@5
```

#### Windows (MSYS2 MinGW-w64):

```bash
pacman -Syu \
           base-devel \
           intltool \
           mingw-w64-x86_64-autotools \
           mingw-w64-x86_64-cmake \
           mingw-w64-x86_64-curl \
           mingw-w64-x86_64-gtk3 \
           mingw-w64-x86_64-libnotify \
           mingw-w64-x86_64-openssl \
           mingw-w64-x86_64-qt5-base \
           mingw-w64-x86_64-qt5-tools \
           mingw-w64-x86_64-qt5-winextras \
           mingw-w64-x86_64-toolchain \
           mingw-w64-x86_64-zlib
```

### 2. Getting the Source

#### Option A: From Standalone Release Tarball (Recommended)

Download the release archive with bundled third-party submodules from [Releases](https://github.com/Mightnire/transmission-og/releases):

```bash
tar -xf transmission-3.07.1.tar.xz
cd transmission-3.07.1
```

#### Option B: From Git Repository

```bash
git clone https://github.com/Mightnire/transmission-og.git transmission
cd transmission
git submodule update --init --recursive
```

### 3. Compilation

#### Using Autotools (Recommended for daemon & CLI):

```bash
./configure --enable-cli
make -j$(nproc)
sudo make install
```

#### Using CMake:

```bash
mkdir build && cd build
cmake -DENABLE_CLI=ON -DUSE_SYSTEM_UTP=OFF ..
make -j$(nproc)
sudo make install
```

## License

Transmission is open source software distributed under the terms of the GNU General Public License (GPL) version 2 or version 3, with portions licensed under the MIT license.
