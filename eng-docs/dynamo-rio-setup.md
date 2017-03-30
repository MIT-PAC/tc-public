# DynamoRIO Setup

1. Build AOSP [1]
2. Start the device running AOSP
3. Gain an adb connection to the device
4. ```adb root```
5. ```adb remount```
6. Download and install the Android NDK [2]:
   1. ```sudo -i```
   2. ```cd /opt```
   3. ```wget https://dl.google.com/android/repository/android-ndk-r13b-linux-x86_64.zip```
   4. ```unzip android-ndk-r13b-linux-x86_64.zip```
   5. ```rm android-ndk-r13b-linux-x86_64.zip```
   6. ```/opt/android-ndk-r13b/build/tools/make-standalone-toolchain.sh --arch=arm
      --platform=android-21 --install-dir=/opt/android-ndk-21 --toolchain=arm-linux-androideabi-4.9```
   7. ```ln -sf arm-linux-androideabi-ld.bfd /opt/android-ndk-21/bin/arm-linux-androideabi-ld```
   8. ```ln -sf ld.bfd /opt/android-ndk-21/arm-linux-androideabi/bin/ld```
   9. ```exit```
7. Build Dynamorio [2]:
   1. ```export DYNRIO=$(pwd)/dynamorio```
   2. ```git clone https://github.com/DynamoRIO/dynamorio.git $DYNRIO```
   3. ```cd $DYNRIO && git checkoutrelease_6_2_0 && cd ..```
   4. ```export DYNRIO_BUILD_DIR=$(pwd)/dynamorio_build```
   5. ```mkdir $DYNRIO_BUILD_DIR && cd $DYNRIO_BUILD_DIR```
   6. ```cmake -DCMAKE_TOOLCHAIN_FILE=$DYNRIO/make/toolchain-android.cmake -DANDROID_TOOLCHAIN=/opt/android-ndk-21
     -DBUILD_TESTS=ON -DDR_COPY_TO_DEVICE=ON -DCMAKE_BUILD_TYPE=Release -DTEST_SUITE=ON $DYNRIO```
   7. ```make```
8. Run test suite [3]:
   1. ```cd $DYNRIO_BUILD_DIR && make test```
9. Run helloworld "APK" under Dynamorio [4]:
   1. ```adb install eden.helloworld.apk```
   2. ```adb push eden.helloworld.wrap.sh /system/xbin/eden.helloworld.wrap.sh```
   3. ```adb shell```
   4. ```cd /data/local/tmp```
   5. ```cp -r dynamorio_build /system/xbin/dynamorio```
   6. ```chown root:root /system/xbin/eden.helloworld.wrap.sh```
   7. ```chmod 0777 /system/xbin/eden.helloworld.wrap.sh```
   8. ```setprop wrap.eden.helloworld "logwrapper /system/xbin/eden.helloworld.wrap.sh"```
   9. ```exit```
10. Now, with your finger tap "HelloWorld" in the apps folder
