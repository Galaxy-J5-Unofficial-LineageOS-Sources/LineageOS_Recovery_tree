# SKYHAWK Recovery Project Tree
<img src="https://avatars.githubusercontent.com/u/66643114?s=200&v=4">
<br/>

# Build Instructions
<a href="https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/LineageOS_Recovery_tree/edit/android-11.0/README.md#set-up-android-build-environment">1.- Set-Up Android Environment</a><br/>
<a href="https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/LineageOS_Recovery_tree/edit/android-11.0/README.md#create-build-path">2.- Create Build path Environment</a><br/>
<a href="https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/LineageOS_Recovery_tree/edit/android-11.0/README.md#init-shrp-repo--sync-products">3.- Init SHRP repo & Sync products</a><br/>
<a href="https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/LineageOS_Recovery_tree/edit/android-11.0/README.md#clone-j5-device-specific-repos-and--kernel-source">4.- Clone J5 device specific repos and & Kernel Source</a></br>
<a href="https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/LineageOS_Recovery_tree/edit/android-11.0/README.md#build-recovery-image">5.- Build recovery image</a>


## Set-up Android Build Environment
```
#Install dependencies
sudo apt update&&sudo apt install git-core gnupg flex bison gperf zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip default-jdk build-essential git fastboot adb python python3 rsync libncurses5

#Install latest repo
mkdir ~/bin
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo

#Install Android SDK Platform Tools
wget https://dl.google.com/android/repository/platform-tools-latest-linux.zip
unzip platform-tools-latest-linux.zip -d ~
cat >> ~/.profile<< EOF
if [ -d "\$HOME/platform-tools" ] ; then
    PATH="\$HOME/platform-tools:\$PATH"
fi
EOF

#Set build cache to 50G
export USE_CCACHE=1
export CCACHE_DIR=~/.ccache
source ~/.bashrc
ccache -M 50G

#Git config
git config --global user.email "you@example.com"
git config --global user.name "Your Name"

```

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
git clone -b lineage-18.1 https://github.com/LineageOS/android_system_tools_dtbtool system/tools/dtbtool
```

## Build recovery image
```
. build/envsetup.sh
lunch omni_j5nlte-eng
mka recoveryimage
```
