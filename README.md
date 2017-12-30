Minimum repo manifest to build Nvidia Sheild TV kernel

Based on the work of [bitbucket.org/nopnop9090/shieldtv-kernel](https://bitbucket.org/nopnop9090/shieldtv-kernel)

#### Building

```sh
  #!/bin/bash

  repo sync

  TOP=`pwd`
  cd vendor/nvidia/licensed-binaries || exit
  ./extract-nv-bins.sh <<< echo 'I ACCEPT'
  cd $TOP || exit

  source build/envsetup.sh
  setpaths

  lunch foster_e-userdebug foster_e-userdebug
  mp bootimage # (change j9 to j<number-of-cpu-cores+1> for optimal build speed)
```

#### Flashing Kernel
```sh
# restart in bootloader mode
adb reboot bootloader

# flash the kernel
fastboot flash boot boot.img
fastboot reboot
```
