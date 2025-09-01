# Patched Jetson kernel

Download the source for the Linux-Tegra 5.10 kernel from [Nvidia](https://developer.nvidia.com/embedded/jetson-linux-r3562). Extract the archive, and then kernel sources. Apply the patch in this directory.
For cross-compilation, prepare the environment as described in the developer guide of the link above.

Load the kernel default config (the same as `tegra_default`) -- you can omit the `CROSS_COMPILE` part if you compile on the Tegra. The `KCFLAGS=-mno-outline-atomics` is necessary to instruct the compiler to avoid ARM v8.2+ optimizations.
```
make -C kernel/kernel-5.10/ ARCH=arm64 LOCALVERSION="-tegra" O=$PWD/kernel_out CROSS_COMPILE="${CROSS_COMPILE_AARCH64}" KCFLAGS=-mno-outline-atomics defconfig
```

Then, edit the config with `menuconfig`
```
make -C kernel/kernel-5.10/ ARCH=arm64 LOCALVERSION="-tegra" O=$PWD/kernel_out CROSS_COMPILE="${CROSS_COMPILE_AARCH64}" KCFLAGS=-mno-outline-atomics menuconfig
```

In addition to selecting T186 as board type (deselecting the others), you need to disable the following due to incompatibilities
```
CONFIG_TEGRA_WAKEUP -> Device drivers, Enable wakeup
CONFIG_TEGRA_PM_IRQ -> Device drivers, Enable PM irq
CONFIG_TEGRA_PMC_AO_WAKE -> Device drivers, Enable AO WAKE from PMC
```
Thus, the proprietary power management does not work.

Additionally, the patch excludes Nvidia's cpufreq and cpuidle features. But the kernel already provides them :)

To compile, remove menuconfig, and (optionally) add `-j` with the number of parallel threads to use, typically `$nproc` or the number of processors.

## What has been patched?


To be continued..
