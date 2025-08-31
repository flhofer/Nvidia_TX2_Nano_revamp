# Patched Jetson kernel

Disclaimer:
In addition to the patch, we have to disable the following features.

```
ONFIG_TEGRA_WAKEUP -> Device drivers, enable wakeup
CONFIG_TEGRA_PM_IRQ -> Device drivers, enable PM irq
CONFIG_TEGRA_PMC_AO_WAKE -> Device drivers, enable AO_WAKE from PMC
```
Thus, the proprietary power management does not work.

Also, the patch excludes Nvidia's cpufreq and cpuidle. But the kernel already provides them :)

To be continued..
