# [Nervos CKB](https://github.com/nervosnetwork/ckb) for aarch64

This branch maintains aarch64 port for Nervos CKB. It currently lives outside of upstream, since it is still in experimental phase.

Since this is early days of the aarch64 port, you might experience quirks or slowdowns, we are still working on optimizing the aarch64 port.

THe following steps can be used to build Nervos CKB for aarch64 on a x86_64 machine running Ubuntu 18.04:

```
$ export TOP=$(pwd)
$ sudo apt-get install gcc-aarch64-linux-gnu g++-aarch64-linux-gnu
# First we need to build OpenSSL for aarch64
$ curl -LO https://www.openssl.org/source/openssl-1.1.1.tar.gz
$ cd openssl-1.1.1
$ tar -xvzf openssl-1.1.1.tar.gz
$ ./Configure linux-aarch64 shared
$ make
$ cd ..
$ export OPENSSL_LIB_DIR=$TOP/openssl-1.1.1
$ export OPENSSL_INCLUDE_DIR=$TOP/openssl-1.1.1/include
$ git clone https://github.com/xxuejie/ckb-on-aarch64
$ cd ckb-on-aarch64
$ rustup target add aarch64-unknown-linux-gnu
$ CC=gcc CC_aarch64_unknown_linux_gnu=aarch64-linux-gnu-gcc cargo build --target=aarch64-unknown-linux-gnu --release
```

If everything goes well, you will find a static linked CKB binary for aarch64 architecture at `target/aarch64-unknown-linux-gnu/release/ckb`. Now we can copy it to a real aarch64 architecture powered CPU to run it. We have tested this on a Raspberry Pi 3B, which works all good.

## Raspberry Pi note

Note that we only support 64-bit ARM CPU now(hence the aarch64 architecture). When you are playing with this on Raspberry Pi, make sure you use Raspberry Pi 3B or later models. You also need a [64-bit OS](https://www.raspberrypi.org/forums/viewtopic.php?t=275370) to run CKB.
