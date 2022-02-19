# LineageOS Recovery tree
<img src="https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/LineageOS_Recovery_tree/blob/lineage-19.0/res/logo.png">
<br/>

# Build Instructions (Needs LineageOS Build environment)

```
. build/envsetup.sh
rm -rf device/samsung/j5nlte && rm -rf kernel/samsung/msm8916  # if exists
git clone https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/LineageOS_Recovery_tree device/samsung/j5nlte
git clone https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/samsung_kernel_msm8916 kernel/samsung/msm8916
lunch lineage_j5nlte-eng
mka recoveryimage
```
