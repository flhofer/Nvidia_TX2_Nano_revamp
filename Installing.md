#How to install a new OS (TX2)

Nowadays, OSs are shipped as images, and for many distros, you can also obtain an ARM64 image. The trick here is to dump the iso and start from there, then install on the HDD, for example.

(Tested with Ubuntu server)

Download the ISO from the website and insert an SD card into your PC. Start `Startup Disk Creator` and prepare the SD as a startup disk. Now, mount the EFI partition (only a few megs) and store the device-tree file that you can "steal" from another kernel build of a similar kernel.
Unmount everything and plug the SD into the Jetson.

Use the Serial adapter to connect a terminal to the TX2 on the GPIO pin-header via software like `tio` or `screen`.

Start the Jetson and press a key to stop the automatic boot. Then type `devnum=1; run mmc_boot`
This will start EFI and GRUB from the SD. Press `e` on the first menu item, go to the `linux` line, and add `console=ttyS0,115200n8` to enable terminal
On a new line, add `devicetree` and the path and filename of the `dtb` file. You can use TAB to autocomplete commands and paths. `ctrl+x` will boot.

Enjoy!
