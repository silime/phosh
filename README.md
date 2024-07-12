# Manjaro Phosh Stable Edition
[![iso_build](https://github.com/manjaro-pinephone/phosh/workflows/image_build/badge.svg)](https://github.com/manjaro-pinephone/phosh/actions)

## description

Stable branch for Phosh of Manjaro Linux for the Pinephone

## where can I download an iso?

Images are build and uploaded in a relatively regular interval to [github releases](https://github.com/manjaro-pinephone/phosh/releases)

## sources

- [image profile](https://github.com/manjaro-pinephone/arm-profiles)

## building

1. check out the arm-profiles
2. `sudo buildarmimg -d pinephone -e phosh -v dev-20210227 -b unstable`

## credentials

```
user: manjaro
password: 123456
```
## OnePlus 6/6T Device status

| USB Networking   | Works   |
| :--------------- | ------- |
| Flashing         | Works   |
| Touchscreen      | Works   |
| Display          | Works   |
| WiFi             | Works   |
| FDE              | Works   |
| Mainline         | Works   |
| Battery          | Works   |
| 3D Acceleration  | Works   |
| Audio            | Works   |
| Bluetooth        | Works   |
| Camera           | Broken  |
| GPS              | Partial |
| Mobile data      | Partial |
| Internal storage |         |
| SMS              | Works   |
| Calls            | Partial |
| USB OTG          | Partial |
| NFC              | Broken  |
|                  |         |

| Accelerometer | Works |
| :------------ | ----- |
| Magnetometer  | Works |
| Ambient Light | Works |
| Proximity     | Works |

## Usage
Dowload Manjaro-ARM-phosh-fajita-beta3X-rootfs.tar.xz
1. Unpack Manjaro-ARM-phosh-fajita-beta3X-rootfs.img to /data/Manjaro-ARM-phosh-fajita-beta3X-rootfs.img
2. If you want to change the partition size, run the following command in your adb shell 
```
su
e2fsck -f /data/Manjaro-ARM-phosh-fajita-beta3X-rootfs.img
resize2fs /data/Manjaro-ARM-phosh-fajita-beta3X-rootfs.img 16G # you root partition is 16G now
# backup your boot and dtbo partition,after that we will replace it 
dd if=/dev/block/by-name/dtbo_a of=/sdcard/dtbo_a 
dd if=/dev/block/by-name/boot_a of=/sdcard/boot_a 
```
> The default data partition is /dev/sda17, and you may need to modify the cmdline of manjaro-fajita-boot.img if you have changed the data partition 

```
fastboot erase dtbo
fastboot boot [the file that ends in -boot.img]
```
## Bugs
Run the following command to start the necessary services to make your modem work 
```
systemctl enable q6voiced.service && systemctl start q6voiced.service
systemctl enable msm-modem-uim-selection.service && systemctl start  msm-modem-uim-selection.service
systemctl enable call_audio_idle_suspend_workaround.service && systemctl start  call_audio_idle_suspend_workaround.service
```
