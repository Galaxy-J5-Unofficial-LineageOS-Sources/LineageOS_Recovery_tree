# SHRP Recovery tree
<img src="https://avatars.githubusercontent.com/u/66643114?s=200&v=4">
<br/>

# Build Instructions


## Create Build path
```
mkdir -p recovery/shrp && cd recovery/shrp
```

## Init SHRP repo & Sync products
```
repo init -u git://github.com/SHRP/manifest.git -b v3_11.0
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
```

## Clone J5 device specific repos and & Kernel Source
```
rm -rf device/samsung/j5nlte && rm -rf kernel/samsung/msm8916  # if exists
git clone -b android-11.0 https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/LineageOS_Recovery_tree device/samsung/j5nlte
git clone https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/samsung_kernel_msm8916 kernel/samsung/msm8916
```

## Build recovery image
```
. build/envsetup.sh
lunch omni_j5nlte-eng
mka recoveryimage
```
