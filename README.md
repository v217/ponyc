# Getting help

Need help? Not to worry, we have you covered.

We have a couple resources designed to help you learn, we suggest starting with the tutorial and from there, moving on to the Pony Patterns book. Additionally, standard library documentation is available online.

* [Tutorial](http://tutorial.ponylang.org).
* [Pony Patterns](http://patterns.ponylang.org) cookbook is in progress
* [Standard library docs](http://ponylang.github.io/ponyc/).

If you are looking for an answer "right now", we suggest you give our IRC channel a try. It's #ponylang on Freenode. If you ask a question, be sure to hang around until you get an answer. If you don't get one, or IRC isn't your thing, we have a friendly mailing list you can try. Whatever your question is, it isn't dumb, and we won't get annoyed.

* [Mailing list](mailto:pony+user@groups.io).
* [IRC](https://webchat.freenode.net/?channels=%23ponylang).

Think you've found a bug? Check your understanding first by writing the mailing list. Once you know it's a bug, open an issue.

* [Open an issue](https://github.com/ponylang/ponyc/issues)

# Editor support

* Sublime Text: [Pony Language](https://packagecontrol.io/packages/Pony%20Language)
* Atom: [language-pony](https://atom.io/packages/language-pony)
* Visual Studio: [VS-pony](https://github.com/ponylang/VS-pony)
* Visual Studio Code: [vscode-pony](https://marketplace.visualstudio.com/items?itemName=npruehs.pony)
* Vim:
    - [vim-pony](https://github.com/jakwings/vim-pony)
    - [pony.vim](https://github.com/dleonard0/pony-vim-syntax)
* Emacs:
    - [ponylang-mode](https://github.com/seantallen/ponylang-mode)
    - [flycheck-pony](https://github.com/rmloveland/flycheck-pony)
    - [pony-snippets](https://github.com/SeanTAllen/pony-snippets)
* BBEdit: [bbedit-pony](https://github.com/TheMue/bbedit-pony)
* Micro: [micro-pony-plugin](https://github.com/Theodus/micro-pony-plugin)

# Installation

## Using Docker

Want to use the latest revision of Pony source, but don't want to build from source yourself? You can run the `ponylang/ponyc` Docker container, which is created from an automated build at each commit to master.

You'll need to install Docker using [the instructions here](https://docs.docker.com/engine/installation/). Then you can pull the latest `ponylang/ponyc` image using this command:

```bash
docker pull ponylang/ponyc:latest
```

Then you'll be able to run `ponyc` to compile a Pony program in a given directory, running a command like this:

```bash
docker run -v /path/to/my-code:/src/main ponylang/ponyc
```

If you're unfamiliar with Docker, remember to ensure that whatever path you provide for `/path/to/my-code` is a full path name and not a relative path, and also note the lack of a closing slash, `/`, at the *end* of the path name.

Note that if your host doesn't match the docker container, you'll probably have to run the resulting program inside the docker container as well, using a command like this:

```bash
docker run -v /path/to/my-code:/src/main ponylang/ponyc ./main
```

If you're using `docker-machine` instead of native docker, make sure you aren't using [an incompatible version of Virtualbox](#virtualbox).

### Docker and AVX2 Support

By default, the Pony Docker image is compiled without support for AVX CPU instructions. For optimal performance, you should build your Pony installation from source.

## Linux using an RPM package (via Bintray)

For Red Hat, CentOS, Oracle Linux, or Fedora Linux, the `master` and `release` branches are packaged and available on Bintray ([pony-language/ponyc-rpm](https://bintray.com/pony-language/ponyc-rpm)).

To install release builds via DNF:
```bash
wget https://bintray.com/pony-language/ponyc-rpm/rpm -O bintray-pony-language-ponyc-rpm.repo
sudo mv bintray-pony-language-ponyc-rpm.repo /etc/yum.repos.d/

sudo dnf --refresh install ponyc
```

Or via Yum:
```
wget https://bintray.com/pony-language/ponyc-rpm/rpm -O bintray-pony-language-ponyc-rpm.repo
sudo mv bintray-pony-language-ponyc-rpm.repo /etc/yum.repos.d/

sudo yum install ponyc
```

### RPM and AVX2 Support

By default, the Pony RPM package is compiled without support for AVX CPU instructions. For optimal performance, you should build your Pony installation from source.

## Linux using a DEB package (via Bintray)

For Ubuntu or Debian Linux, the `master` and `release` branches are packaged and available on Bintray ([pony-language/ponyc-debian](https://bintray.com/pony-language/ponyc-debian)).

To install release builds via Apt:

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 379CE192D401AB61
sudo echo "deb https://dl.bintray.com/pony-language/ponyc-debian pony-language main" | sudo tee -a /etc/apt/sources.list
sudo apt-get update
sudo apt-get install ponyc
```


### DEB and AVX2 Support

By default, the Pony DEB package is compiled without support for AVX CPU instructions. For optimal performance, you should build your Pony installation from source.

## Arch Linux

```bash
pacman -S ponyc
```

## Gentoo Linux

```bash
layman -a stefantalpalaru
emerge dev-lang/pony
```

A live ebuild is also available in the [overlay](https://github.com/stefantalpalaru/gentoo-overlay) (dev-lang/pony-9999) and for Vim users there's app-vim/pony-syntax.

## Linux using [Linuxbrew](http://linuxbrew.sh)

```bash
$ brew update
$ brew install ponyc
```

## Mac OS X using [Homebrew](http://brew.sh)

```bash
$ brew update
$ brew install ponyc
```

## Windows using ZIP (via Bintray)

Windows users will need to install:

- Visual Studio 2015 (available [here](https://www.visualstudio.com/vs/community/)) or the Visual C++ Build Tools 2015 (available [here](http://landinghub.visualstudio.com/visual-cpp-build-tools)), and
- Windows 10 SDK (available [here](https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk)).

Once you have installed the prerequisites, you can download the latest ponyc release from [bintray](https://dl.bintray.com/pony-language/ponyc-win/).

# Building ponyc from source

First of all, you need a compiler with decent C11 support. The following compilers are supported, though we recommend to use the most recent versions.

- GCC >= 4.7
- Clang >= 3.3
- MSVC >= 2013
- XCode Clang >= 6.0

Pony requires one of the following versions of LLVM:

- 3.7.1
- 3.8.1
- 3.9.1

Compiling Pony is only possible on x86 and ARM (either 32 or 64 bits).

## Building on Linux

Get Pony-Sources from Github (More Information about Set Up Git https://help.github.com/articles/set-up-git/ ):
```bash
$ sudo apt install git
$ git clone git://github.com/ponylang/ponyc
```

[![Linux and OS X](https://travis-ci.org/ponylang/ponyc.svg?branch=master)](https://travis-ci.org/ponylang/ponyc)

### Arch

```
pacman -S llvm make ncurses openssl pcre2 zlib
```

To build ponyc and compile helloworld:

```bash
$ make
$ ./build/release/ponyc examples/helloworld
```

If you get errors like

```bash
/usr/bin/ld.gold: error: ./fb.o: requires dynamic R_X86_64_32 reloc against 'Array_String_val_Trace' which may overflow at runtime; recompile with -fPIC
```

try running `ponyc` with the `--pic` flag.

```bash
$ ./build/release/ponyc --pic examples/helloworld
```

### Debian Jessie

Add the following to `/etc/apt/sources`:

```
deb http://llvm.org/apt/jessie/ llvm-toolchain-jessie-3.8 main
deb-src http://llvm.org/apt/jessie/ llvm-toolchain-jessie-3.8 main
```

Install the LLVM toolchain public GPG key, update `apt` and install packages:

```bash
$ wget -O - http://llvm.org/apt/llvm-snapshot.gpg.key|sudo apt-key add -
$ sudo apt-get update
$ sudo apt-get install make gcc g++ git zlib1g-dev libncurses5-dev \
                       libssl-dev llvm-3.8-dev
```

Debian Jessie and some other Linux distributions don't include pcre2 in their package manager. pcre2 is used by the Pony regex package. To download and build pcre2 from source:

```bash
$ wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre2-10.21.tar.bz2
$ tar xvf pcre2-10.21.tar.bz2
$ cd pcre2-10.21
$ ./configure --prefix=/usr
$ make
$ sudo make install
```

To build ponyc, compile and run helloworld:

```bash
$ cd ~/ponyc/
$ make
$ ./build/release/ponyc examples/helloworld
$ ./helloworld
```

### Ubuntu (14.04, 15.10, 16.04)

```bash
$ sudo apt-get update
$ sudo apt-get install -y build-essential git zlib1g-dev libncurses5-dev libssl-dev libpcre2-dev
```

You should install LLVM 3.7.1, 3.8.1, or 3.9.1 from the [LLVM download page](http://llvm.org/releases/download.html) under Pre-Built Binaries.  Then you can extract that LLVM to `/usr/local`, for example, like so:

```bash
tar xJf clang+llvm-${LLVM_VERSION}-x86_64-linux-gnu-ubuntu-16.04.tar.xz \
    --strip-components 1 -C /usr/local/ \
    clang+llvm-${LLVM_VERSION}-x86_64-linux-gnu-ubuntu-16.04
```
where `${LLVM_VERSION}` is whatever version of LLVM you've downloaded the `.xz` file for.

To build ponyc, compile and run helloworld:

```bash
$ cd ~/ponyc/
$ make
$ ./build/release/ponyc examples/helloworld
$ ./helloworld
```

### Other Linux distributions

You need to have the development versions of the following installed:

* LLVM 3.7.1, 3.8.1, or 3.9.1
* zlib
* ncurses
* pcre2
* libssl

If your distribution doesn't have a package for prce2, you will need to download and build it from source:

```bash
$ wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre2-10.21.tar.bz2
$ tar xvf pcre2-10.21.tar.bz2
$ cd pcre2-10.21
$ ./configure --prefix=/usr
$ make
$ sudo make install
```

Finally to build ponyc, compile and run the hello world app:

```bash
$ cd ~/ponyc/
$ make
$ ./build/release/ponyc examples/helloworld
$ ./helloworld
```

## Building on FreeBSD

First, install the required dependencies:

```bash
sudo pkg install gmake
sudo pkg install llvm38
sudo pkg install pcre2
sudo pkg install libunwind
```

This will build ponyc and compile helloworld:

```bash
$ gmake
$ ./build/release/ponyc examples/helloworld
```

Please note that on 32-bit X86, using LLVM 3.7.1 or 3.8.1 on FreeBSD currently produces executables that don't run. Please use LLVM 3.9.1. 64-bit X86 does not have this problem, and works fine with LLVM 3.7.1 and 3.8.1.

## Building on Mac OS X
[![Linux and OS X](https://travis-ci.org/ponylang/ponyc.svg?branch=master)](https://travis-ci.org/ponylang/ponyc)

You'll need llvm 3.7.1, 3.8.1 or 3.9.1 and the pcre2 library to build Pony. You can use either homebrew or MacPorts to install your dependencies. Please note that llvm 3.9.1 is not available via homebrew. As such, the instructions below install 3.8.1

Installation via [homebrew](http://brew.sh):
```
$ brew update
$ brew install llvm@3.9 pcre2 libressl
```

Installation via [MacPorts](https://www.macports.org):
```
$ sudo port install llvm-3.9 pcre2 libressl
$ sudo port select --set llvm mp-llvm-3.9
```

Launch the build with `make` after installing the dependencies:
```
$ make
$ ./build/release/ponyc examples/helloworld
```

## Building on Windows
[![Windows](https://ci.appveyor.com/api/projects/status/kckam0f1a1o0ly2j?svg=true)](https://ci.appveyor.com/project/sylvanc/ponyc)

_Note: it may also be possible (as tested on build 14372.0 of Windows 10) to build Pony using the [Ubuntu 14.04](#ubuntu-1404-1510-1604) instructions inside [Bash on Ubuntu on Windows](https://msdn.microsoft.com/en-us/commandline/wsl/about)._

Building on Windows requires the following:

- [Visual Studio 2015](https://www.visualstudio.com/downloads/) at least Update 2; make sure that a Windows 10 SDK is installed; otherwise install it from [here](https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk).
- [Python](https://www.python.org/downloads) (3.5 or 2.7) needs to be in your PATH.

In a command prompt in the `ponyc` source directory, run the following:

```
> make.bat configure
```

(You only need to run this the first time you build the project.)

```
> make.bat build test
```

This will automatically perform the following steps:

- Download some pre-built libraries used for building the Pony compiler and standard library.
  - [LLVM](http://llvm.org)
  - [LibreSSL](https://www.libressl.org/)
  - [PCRE](http://www.pcre.org)
- Build the pony compiler in the `build-<config>-<llvm-version>` directory.
- Build the unit tests for the compiler and the standard library.
- Run the unit tests.

You can provide the following options to `make.bat` when running the `build` or `test` commands:

- `--config debug|release`: whether or not to build a debug or release build (debug is the default).
- `--llvm <version>`: the LLVM version to build against (3.9.1 is the default).

Note that you need to provide these options each time you run make.bat; the system will not remember your last choice.

Other commands include `clean`, which will clean a specified configuration; and `distclean`, which will wipe out the entire build directory.  You will need to run `make configure` after a distclean.

## Building with link-time optimisation (LTO)

You can enable LTO when building the compiler in release mode. There are slight differences between platforms so you'll need to do a manual setup. LTO is enabled by setting `lto` to `yes` in the build command line:

```bash
$ make lto=yes
```

If the build fails, you have to specify the LTO plugin for your compiler in the `LTO_PLUGIN` variable. For example:

```bash
$ make LTO_PLUGIN=/usr/lib/LLVMgold.so
```

Refer to your compiler documentation for the plugin to use in your case.

## VirtualBox

Pony binaries can trigger illegal instruction errors under VirtualBox 4.x, for at least the x86_64 platform and possibly others.

Use VirtualBox 5.x to avoid possible problems.


You can learn more about [AVX2](https://en.wikipedia.org/wiki/Advanced_Vector_Extensions#Advanced_Vector_Extensions_2) support.

## Building Pony on Non-x86 platforms

On ARM platforms, the default gcc architecture specification used in the Makefile of _native_ does not work correctly, and can even result in the gcc compiler crashing.  You will have to override the compiler architecture specification on the _make_ command line.  For example, on a RaspberryPi2 you would say:
```bash
$ make arch=armv7
```

To get a complete list of acceptable architecture names, use the gcc command:

```bash
gcc -march=none
```

This will result in an error message plus a listing off all architecture types acceptable on your platform.
