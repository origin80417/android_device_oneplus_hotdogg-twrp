# Device Tree for OnePlus 7T Pro aka hotdogg for TWRP (this should be unified with 7T, but I cannot test since I do not own that device)
## Disclaimer - Unofficial TWRP!
These are personal test builds of mine, experimenting with further development of this device. In no way do I hold responsibility if it/you brick your device.
Proceed at your own risk because I am doing the same, so make a backup and have a msmtool ready to use if necessary

## Setup repo tool
Setup repo tool from here https://source.android.com/setup/develop#installing-repo

## Compile

Sync Pitch Black Recovery manifest:

```
repo init -u https://github.com/PitchBlackRecoveryProject/manifest_pb -b android-11.0
```

Make a directory named local_manifest under .repo, and create a new manifest file named local_manifest.xml
and then paste the following

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
<remote name="origin8" fetch="https://github.com/origin80417" />

<project path="device/oneplus/hotdogg" name="origin80417/android_device_oneplus_hotdogg-twrp" remote="origin8" revision="PBRP" />
</manifest>
```

Sync the sources with

```
repo sync
```

To build, execute these commands in order

```
. build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
lunch twrp_hotdogg-eng
mka adbd pbrp
```

To test it:

```
# To temporarily boot it
fastboot boot out/target/product/hotdogg/recovery.img 

# Since 7T / Pro has a dedicated recovery partition, you can flash the recovery with
fastboot flash recovery recovery.img

I personally prefer to boot with the .img and then flash the zip. 
```

##### Credits
- me2151 for his updating to hotdogg device.
- CaptainThrowback for original trees.
- mauronofrio for original trees.
- TWRP team and everyone involved for their amazing work.
