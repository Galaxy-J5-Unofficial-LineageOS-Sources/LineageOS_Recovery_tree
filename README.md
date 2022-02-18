# LineageOS Recovery tree
<img src="https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/LineageOS_Recovery_tree/blob/lineage-19.0/res/logo.png">
<br/>

# Build Instructions (Needs LineageOS Build environment)

```
. build/envsetup.sh
rm -rf device/samsung/j5nlte # if exists
git clone https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/LineageOS_Recovery_tree device/samsung/j5nlte
lunch lineage_j5nlte-eng
mka recoveryimage
```
