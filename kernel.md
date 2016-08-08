export PATH=$(pwd)/aarch64-linux-android-4.9/bin:$PATH
export CROSS_COMPILE=$(pwd)/aarch64-linux-android-4.9/bin/aarch64-linux-android-

export PATH=$(pwd)/aarch64-linux-android-5.x/bin:$PATH
export CROSS_COMPILE=$(pwd)/aarch64-linux-android-5.x/bin/aarch64-linux-android-

export PATH=$(pwd)/aarch64-linux-android-6.x/bin:$PATH
export CROSS_COMPILE=$(pwd)/aarch64-linux-android-6.x/bin/aarch64-linux-android-

export PATH=$(pwd)/arm-eabi-4.9/bin:$PATH
export CROSS_COMPILE=$(pwd)/arm-eabi-4.9/bin/arm-eabi-

export PATH=$(pwd)/arm-eabi-5.x/bin:$PATH
export CROSS_COMPILE=$(pwd)/arm-eabi-5.x/bin/arm-eabi-

export PATH=$(pwd)/arm-eabi-6.x/bin:$PATH
export CROSS_COMPILE=$(pwd)/arm-eabi-6.x/bin/arm-eabi-


mkdir out
cd kernel
make ARCH=arm64 O=../out mrproper
make ARCH=arm64 O=../out hammerhead_defconfi
make ARCH=arm64 O=../out -j8


mkbootimg_tools/mkboot boot.img boot.extracted

cp out/arch/arm64/boot/Image.gz boot.extracted/kernel
cp out/arch/arm64/boot/Image.gz-dtb boot.extracted/kernel
cp out/arch/arm/boot/zImage-dtb boot.extracted/kernel

mkbootimg_tools/mkboot boot.extracted boot.newkernel.img

