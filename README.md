# TWRP tree for Motorola MSM8916 Family

## Dependencies:
(you probably don't need most of these)
```
sudo apt-get install bison build-essential curl flex git gnupg gperf libesd0-dev liblz4-tool libncurses5-dev libsdl1.2-dev libwxgtk2.8-dev libxml2 libxml2-utils lzop openjdk-6-jdk openjdk-6-jre pngcrush schedtool squashfs-tools xsltproc zip zlib1g-dev
sudo apt-get install g++-multilib gcc-multilib lib32ncurses5-dev lib32readline-gplv2-dev lib32z1-dev
```
You also need the repo tool for cloning Android source trees.

## Set up and get the repo:
```
mkdir ~/omni-twrp-tree
cd ~/omni-twrp-tree
repo init -u https://github.com/sultanqasim/twrp_recovery_manifest.git -b android-7.1
mkdir -p .repo/local_manifests
```
Create a file .repo/local\_manifests/motorola.xml and paste this in
```
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
    <project name="kingrj999/twrp_android_device_motorola_msm8916-common" path="device/motorola/msm8916-common" remote="github" revision="twrp" />
    <project name="sultanqasim/android_device_motorola_surnia" path="device/motorola/surnia" remote="github" revision="twrp" />
    <project name="kingrj999/twrp_android_device_motorola_osprey" path="device/motorola/osprey" remote="github" revision="twrp" />
    <project name="sultanqasim/android_device_motorola_merlin" path="device/motorola/merlin" remote="github" revision="twrp" />
    <project name="sultanqasim/android_device_motorola_lux" path="device/motorola/lux" remote="github" revision="twrp" />
    <project name="kingrj999/twrp_android_kernel_motorola_msm8916" path="kernel/motorola/msm8916" remote="github" revision="squid_nougat" />
    <project name="LineageOS/android_device_qcom_common" path="device/qcom/common" remote="github" revision="cm-14.1" />
</manifest>
```

Now fetch the code
```
repo sync
```
Just clone TWRP, MultiROM and libbootimg repos into your Android Tree, the commands would look something like this:
```
rm -r bootable/recovery  
git clone https://github.com/Tasssadar/Team-Win-Recovery-Project.git bootable/recovery  
git clone https://github.com/Tasssadar/multirom.git system/extras/multirom  
git clone https://github.com/Tasssadar/libbootimg.git system/extras/libbootimg
cd system/extras/multirom
git submodule update --init

```
## Building:
```
source build/envsetup.sh
breakfast osprey
make clean
make -j5 recoveryimage
```
## Building Multirom
```bash
make recoveryimage # builds the recovery image
make multirom # builds multirom binary
make trampoline # builds trampoline - MultiROM's init daemon
make multirom_zip # builds multirom and trampoline and installation ZIP file
make multirom_uninstaller # builds uninstaller ZIP
```
