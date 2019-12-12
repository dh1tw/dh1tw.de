---
title: "Cross-Compiling Golang (CGO) Projects"
author: Tobias (DH1TW)
date: 2019-12-08T09:07:38+01:00
layout: post
categories:
  - Software
  - Golang
tags:
  - golang
  - continuous-integration
  - docker
  - cgo
thumbnailImage: "img/2019/12/gopher-with-c-book.jpg"
thumbnailImagePosition: "left"
---

One of [Golang](https://golang.org)'s strength is that it supports cross compiling to literally any common Operating System and CPU architecture out of the box. However that's only true for projects written in pure Go. Normally that's not a problem, but sometimes we depend on 3rd-party C libraries... and that's when things tend to get complicated.

In this post I will explain how you can cross compile your [cgo](https://golang.org/cmd/cgo) project for multiple operating systems and architectures in a clear and structured manner.

<!--more-->

## Some Background

Over the last few years I've been writing software mainly for remote controlling our Amateur Radio station over the Internet. Most of these programs are written in [Go](https://golang.org) and published on my [Github profile](https://github.com/dh1tw) under permissive Open Source licenses. The most prominent program is [remoteAudio](https://github.com/dh1tw/remoteAudio), a low latency, multi user audio streaming application.

While one can achieve a lot in native [Go](https://golang.org), sometimes there is just no way around using C libraries. One could re-implement those libraries in Go, but often it's just not feasible. In the case of [remoteAudio](https://github.com/dh1tw/remoteAudio), I'm using for example the [OPUS audio codec](https://www.opus-codec.org/) and [Portaudio](http://www.portaudio.com/) for handling cross-platform Audio APIs. Both of them are written in C.

## Assumptions

I personally like [Debian](https://www.debian.org) flavored Linux systems. That's what this article has been written for. However it should be also valid for all other Linux distros. In most cases you just have to replace the `apt-get` package manager commands with the one's from your distro.

There are two important terms which have to be defined:

| Term              | Meaning                                                          |
| ----------------- | ---------------------------------------------------------------- |
| **Host System**   | This is the system on which the compiler and the tools are run.  |
| **Target System** | This is the system for which we generate the programs/libraries. |

In my case, the *Host System* is **Linux/amd64**.

## Get a Cross Compiler

You could [build the (GCC based) cross compiler yourself](https://preshing.com/20141119/how-to-build-a-gcc-cross-compiler),
but fortunately, the popular Linux distributions provide them pre-compiled with all dependencies through their respective package managers.

In order to get started you need at least the cross-compiler and the platform specific standard library (*libc*). The corresponding packages are:

| Operating System | Architecture | Needed package(s)       |
| ---------------- | ------------ | ----------------------- |
| Linux            | armhf        | gcc-arm-linux-gnueabihf |
|                  |              | libc6-dev-armhf-cross   |
| Linux            | arm64        | gcc-aarch64-linux-gnu   |
|                  |              | libc6-dev-arm64-cross   |
| Linux            | i386         | gcc-multilib            |
|                  |              | libc6-dev-i386          |
|                  |              | linux-libc-dev:i386     |
| Windows          | amd64        | gcc-mingw-w64-x86-64    |
| Windows          | i386         | gcc-mingw-w64-i686      |

If your cgo program only uses the [standard C library](https://www.gnu.org/software/libc) this would actually be all you need. However, we often depend on additional libraries. For example, [remoteAudio](https://github.com/dh1tw/remoteAudio) depends also on `libopus` and `libportaudio`. Since our target architecture (e.g. `arm64`) differs from our host's architecture (`amd64`), we cannot simply install the needed libraries with `apt-get`. This would just install the `amd64` versions of those libraries.

## Add support for target architectures

Debian based distributions come fortunately with [Multiarch support](https://wiki.ubuntu.com/MultiarchCross). This allows us to install library packages for multiple architectures on the same machine. Dependencies will be automatically correctly resolved.

To my knowledge, Debian supports at least the following architectures:
`amd64`, `i386`, `armel`, `armhf`, `arm64`, `mips`, `powerpc` and `ppc64el`.

With the help of [dpkg, the Debian Package Manager](https://www.dpkg.org) we can add additional architectures (e.g. `arm64`) on our host system:

```bash

$ dpkg --add-architecture arm64

```

After updating the packages sources with `apt-get update` we are able to install now pre-compiled library packages for the target system. These packages are distinguished by the `:<architecture>` suffix. So installing the opus and portaudio libraries (and header files) for `arm64` looks like this:

```bash

$ apt-get update
$ apt-get install -y libopus-dev:arm64 \
                    libopus0:arm64 \
                    libportaudio19-dev:arm64 \
                    libportaudio2:arm64

```

The Debian package manager will store the installed files on our host system in folders named after the respective architecture. For the case above, we can find the `arm64` libraries in `/usr/lib/aarch64-linux-gnu/` and the corresponding header files in `/usr/include/aarch64-linux-gnu`.

## Preparing the environment

Before we can cross compile our (c)go program, we have to set a few environment variables. We could all set them inline when calling the `go` compiler, but for the sake of clarity we will set and discuss the variables one by one.

```bash

export GOOS=linux
export GOARCH=arm64
export CGO_ENABLED=1
export CC=aarch64-linux-gnu-gcc
export PKG_CONFIG_PATH=/usr/lib/aarch64-linux-gnu/pkgconfig

```

With `GOOS` and `GOARCH` we tell the go compiler the operating system and architecture of our target system. Since our program contains C code, we have to explicitly enable `cgo` by setting `CGO_ENABLED` (`cgo` is disabled by default for cross-compiling). Instead of using the host's default C compiler (gcc), we want to use the previously installed cross compiler for `arm64`. This is accomplished by setting the `CC` variable to the C compiler of choice. Finally we have to set the `PKG_CONFIG_PATH` so that [pkg-config](https://en.wikipedia.org/wiki/Pkg-config) uses the `pkg-config` files for our target architecture. Just in case you wonder, the `pkg-config` files are installed automatically with the corresponding package library.

## Compile

Once all the preparations have been done, it's just a matter of calling

```bash

$ go build

```

In case you don't use `pkg-config` and haven't specified `LDFLAGS` with a [cgo directive](https://golang.org/cmd/cgo/) in your source code, you can specify the locations of the libraries and header files with the `-ldflags` flag:

```bash

$ go build -ldflags="-Ipath/to/headerfile -Lpath/to/lib"

```

## Containerize it

While we could certainly install everything required for cross compiling on our host system,
I personally prefer to keep my host system as *clean* as possible. Over the years, [Docker](https://www.docker.com/) has become one of my indispensible tools. It's the perfect tool for our cross-compilation chains.

For [remoteAudio](https://github.com/dh1tw/remoteAudio) I created the repository [remoteAudio-xcompile](https://github.com/dh1tw/remoteAudio-xcompile) which contains Dockerfiles for each combination of os/architecture I support. These containers can be build either locally or downloaded from the [Docker Hub registry](https://hub.docker.com/repository/docker/dh1tw/remoteaudio-xcompile).

Below you can find the Dockerfile with remoteAudio's `arm64` cross compilation chain.

```dockerfile

FROM golang:1.13-buster
LABEL os=linux
LABEL arch=arm64

ENV GOOS=linux
ENV GOARCH=arm64
ENV CGO_ENABLED=1
ENV CC=aarch64-linux-gnu-gcc
ENV PATH="/go/bin/${GOOS}_${GOARCH}:${PATH}"
ENV PKG_CONFIG_PATH=/usr/lib/aarch64-linux-gnu/pkgconfig

# install build & runtime dependencies
RUN dpkg --add-architecture arm64 \
    && apt update \
    && apt install -y --no-install-recommends \
        protobuf-compiler \
        upx \
        gcc-aarch64-linux-gnu \
        libc6-dev-arm64-cross \
        pkg-config \
        libsamplerate0:arm64 \
        libsamplerate0-dev:arm64 \
        libopusfile0:arm64 \
        libopusfile-dev:arm64 \
        libopus0:arm64 \
        libopus-dev:arm64 \
        libportaudio2:arm64 \
        portaudio19-dev:arm64 \
    && rm -rf /var/lib/apt/lists/*

# install build dependencies (code generators)
RUN GOARCH=amd64 go get github.com/gogo/protobuf/protoc-gen-gofast \
    && GOARCH=amd64 go get github.com/GeertJohan/go.rice/rice \
    && GOARCH=amd64 go get github.com/micro/protoc-gen-micro

```

In order to compile the program for `arm64` you just need to call from the source directory:

```bash

$ docker run --rm -v "$PWD":/usr/src/myapp -w /usr/src/myapp dh1tw/remoteaudio-xcompile:linux-arm64 /bin/sh -c 'go build'

```

With the `-v` flag we mount the current directory of our host (`$PWD`) into the container under the path `/usr/src/myapp`. We select the same directory as our working directory with the `-w`. After generating our binary we automatically delete the container with the `--rm` flag.

After the successful compilation, we find the binary in the current directory of our host system and we can confirm that it has been built for `arm64` (aarch64).

```bash

$ file ./remoteAudio
./remoteAudio: ELF 64-bit LSB executable, ARM aarch64, version 1 (SYSV), statically linked, no section header

```

## Microsoft Windows

Cross compiling cgo applications from Linux host systems for Microsoft Windows is a bit more complicated and requires a few extra steps. [**MinGW** (Minimalist GNU for Windows)](http://mingw.org/) provides a development environment for native Microsoft Windows applications. MinGW is available on Linux and Windows. MinGW works out of the box if no 3rd-party C-Runtime libraries (DLLs) are involved... and that's unfortunately again a problem since remoteAudio depends on 3rd-party libraries like opus and portaudio. How cool would it be if we could also install our dependencies with a package manager like Debian's `apt-get` ?

**MSYS2 & Pacman to the rescue!**

As it turns out, some smart folks have solved this problem and created [MSYS2](https://www.msys2.org/) which is a software distro and building platform for Windows. MSYS2 is built around the MinGW-w64 toolchain and comes with a ported version of [Arch Linux'](https://www.archlinux.org/) package manager [Pacman](https://wiki.archlinux.org/index.php/Pacman). MSYS2 provides read-to-go installers for Windows, but installing MSYS2 on Linux is a bit more work.

Fortunately, [Gary Kramlich](https://twitter.com/rw_grim) who is one of [Pidgin](https://pidgin.im/)'s core developers, has done all the hard work for us and created the Debian based [msys2-cross](https://hub.docker.com/r/rwgrim/msys2-cross) Container. Using this container as the base image, I created containers to compile remoteAudio for `windows/amd64` and `windows/i386` directly from Linux. You can find the Dockerfiles in the respective folders of the [remoteAudio-xcompile repository](https://github.com/dh1tw/remoteAudio-xcompile).

This is the Dockerfile for `windows/amd64`:

```dockerfile

FROM rwgrim/msys2-cross
LABEL os=windows
LABEL arch=amd64

ENV GOVERSION="1.13.4"
ENV GOOS=windows
ENV GOARCH=amd64
ENV GOPATH=/go
ENV CGO_ENABLED=1
ENV CC=x86_64-w64-mingw32-gcc
ENV CXX=x86_64-w64-mingw32-g++
ENV PATH="/go/bin:/usr/local/go/bin:${PATH}"
ENV PKG_CONFIG_PATH=/windows/mingw64/lib/pkgconfig
ENV MSYS2_ARCH=x86_64

# install build dependencies
RUN set -ex \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        gcc-mingw-w64-x86-64 \
        git \
        protobuf-compiler \
        upx \
        pkg-config \
    && rm -rf /var/lib/apt/lists/*

# install golang
RUN set -ex \
    && wget -P /tmp -q https://dl.google.com/go/go$GOVERSION.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf /tmp/go$GOVERSION.linux-amd64.tar.gz

# install build dependencies
RUN set -ex \
    && pacman --noconfirm --needed -Sy mingw-w64-$MSYS2_ARCH-libsamplerate \
    && pacman --noconfirm --needed -Sy mingw-w64-$MSYS2_ARCH-portaudio \
    && pacman --noconfirm --needed -Sy mingw-w64-$MSYS2_ARCH-opus \
    && pacman --noconfirm --needed -Sy mingw-w64-$MSYS2_ARCH-opusfile \
    && pacman --noconfirm -Sc

# install runtime dependencies (DLLs)
RUN set -ex \
    && pacman-cross --noconfirm --needed -Sy mingw-w64-$MSYS2_ARCH-libsamplerate \
    && pacman-cross --noconfirm --needed -Sy mingw-w64-$MSYS2_ARCH-portaudio \
    && pacman-cross --noconfirm --needed -Sy mingw-w64-$MSYS2_ARCH-opus \
    && pacman-cross --noconfirm --needed -Sy mingw-w64-$MSYS2_ARCH-opusfile \
    && pacman-cross --noconfirm -Sc

# install build dependencies (code generators)
RUN set -ex \
    && GOOS=linux GOOARCH=amd64 go get github.com/gogo/protobuf/protoc-gen-gofast \
    && GOOS=linux GOOARCH=amd64 go get github.com/GeertJohan/go.rice/rice \
    && GOOS=linux GOOARCH=amd64 go get github.com/micro/protoc-gen-micro

COPY ./scripts /scripts

```

Here we are installing the 3rd-party dependencies twice. Once for linking & compiling and once for the pre-build DLLs which we later extract conveniently with a script.

So in order to compile our (c)go program for `windows/amd64` and extract the `dlls`, we just execute:

```bash

$ docker run --rm -v "$PWD":/usr/src/myapp -w /usr/src/myapp dh1tw/remoteaudio-xcompile:windows-amd64 /bin/sh -c 'go build && /scripts/getlibs.sh .'
[output not shown]

$ ls -al | grep '*.exe\|*.dll'
-rwxr-xr-x   1 user  staff    85136 Dec 12 14:57 libgcc_s_seh-1.dll
-rwxr-xr-x   1 user  staff    44544 Dec 12 14:57 libogg-0.dll
-rwxr-xr-x   1 user  staff   406177 Dec 12 14:57 libopus-0.dll
-rwxr-xr-x   1 user  staff    54568 Dec 12 14:57 libopusfile-0.dll
-rwxr-xr-x   1 user  staff   183508 Dec 12 14:57 libportaudio-2.dll
-rwxr-xr-x   1 user  staff  1498448 Dec 12 14:57 libsamplerate-0.dll
-rwxr-xr-x   1 user  staff    55808 Dec 12 14:57 libwinpthread-1.dll
-rwxr-xr-x@  1 user  staff  9446400 Dec 12 14:57 remoteAudio.exe

$ file ./remoteAudio.exe
remoteAudio.exe: PE32+ executable (console) x86-64 (stripped to external PDB), for MS Windows

```

## Conclusion

In this article I've explained my approach on how to cross compile Go applications which depend on C libraries for different architectures & operating systems. Putting the Cross compilation chains into Docker containers does not only keep our host system clean, it also documents build process and shows the needed dependencies. As a bonus, the containers integrate nicely in our Continous Integration & Continous Delivery (CI/CD) Pipeline so that we can generate a [releases for a variety of platforms](https://github.com/dh1tw/remoteAudio/releases) without any additional effort.
