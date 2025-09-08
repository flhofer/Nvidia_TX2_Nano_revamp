# Nvidia_TX2_Nano_revamp
Patches, changes, and instructions to revive these lovely pieces of hardware that have been abandoned 7 years ago

This repository will contain source patches, such as those required to compile the official 5.10 kernel for Jetson systems. keep posted for updates.



## Lessons learned so far

While building kernels, installing tools and testing applications, I learned the following:

* the iGPU driver installed works only with CUDA versions upto 10.2
* kernel driver sources are available, but build only with Nvidia kernels 5.x and up -- vanilla kernels do not work
* kernel 5.x sources are available but do not build for T186 and T210 (as is )
* you can manually compile apps to run with CUDA 10.2, but the compiler provided is too old
* same for cmake
* you can upgrade the system to, say Ubuntu 22.04 LTS while keeping kernel 4.9 and old L4T with a slightly different kernel config
* if you upgrade, xorg stops working. There exist workarounds.
* if you upgrade, you can not build CUDA applications as it is locked to gcc <9
* the only gcc that works for building is gcc 8.5 and it must be manually compiled
* you can install a vanilla kernel, and most features seem to work, but not the GPU as gpGPU.

That said, you should immediately compile and install a newer cmake and gcc (=8.5) version.
