# Prebuilt GCC toolchains

These are my personal toolchains, cross compiled for arm and aarch64. I currently use them for compiling [Flash Kernel](https://github.com/nathanchance/angler). They are compiled with [crosstool-NG](http://crosstool-ng.github.io).


## Supported operating systems

Most if not all versions of 64-bit Linux should work with these as they are statically linked. Let me know if there are any issues following the questions section below.


## Variants

* A standard GNU version, build straight from the [standard GCC source](https://gcc.gnu.org/git/?p=gcc.git)
* A Linaro version, currently compiled from the [linaro-local/gcc-7-integration-branch](https://git.linaro.org/toolchain/gcc.git/log/?h=linaro-local/gcc-7-integration-branch) branch

| Architecture | GCC source | Branch | Prefix |
| ------------ | ---------- | ------ | ------ |
| arm          | GNU        | arm-gnu-7.x | arm-gnu-linux-gnueabi- |
| arm          | Linaro     | arm-linaro-7.x | arm-linaro-linux-gnueabi - |
| aarch64      | GNU        | aarch64-gnu-7.x | aarch64-gnu-linux-gnu- |
| aarch64      | Linaro     | aarch64-linaro-7.x | aarch64-linaro-linux-gnu- |


## Using these toolchains

To use these toolchains, you first need to do a shallow clone (to avoid pulling too much history):

```bash
git clone -b <branch> --depth=1 https://github.com/nathanchance/gcc-prebuilts
```

Then point your cross compiler to the toolchain. For kernels, you can do the following:

```bash
export CROSS_COMPILE=$(pwd)/gcc-prebuilts/bin/<prefix>
```

For kernels, you must have the following four commits:
+ [Makefile: Fix device not booting with GCC 7.x and above](https://github.com/nathanchance/angler/commit/406d54a7f006142372157d4fb49d7e76a5564d00)
+ [Revert "scripts: gcc-wrapper: Use wrapper to check compiler warnings"](https://android.googlesource.com/kernel/msm/+/e7fb62baa7c8b803d7e3b3f3d8bf4e2b916b659d)
+ [kernel: use the gnu89 standard explicitly](https://github.com/torvalds/linux/commit/51b97e354ba9fce1890cf38ecc754aa49677fc89)
+ [compiler-gcc: integrate the various compiler-gcc\[345.h\] files](https://github.com/torvalds/linux/commit/cb984d101b30eb7478d32df56a0023e4603cba7f)

The last two commits are from Linux upstream. The first is only needed if your version is 3.10.79 or earlier. The second is needed for both 3.10 (3.10.101 or earlier) and 3.18 (3.18.31 or earlier). I do [recommend upstreaming your kernels](https://forum.xda-developers.com/android/software-hacking/reference-how-to-upstream-android-kernel-t3626913) but if you choose not to, just pick that commit.


## Compiling these toolchains

If you would like to learn how to compile these toolchains, please give [this README](https://github.com/nathanchance/build-tools-gcc/blob/master/README.md) a glance.


## Questions?

If you have any questions or issues, please open an issue on this repo or the [build-tools-gcc](https://github.com/nathanchance/build-tools-gcc) repo OR make a post in [the XDA thread](https://forum.xda-developers.com/android/development/toolchains-gnu-linaro-5th-2017-t3606941) and I'll do my best to assist you.
