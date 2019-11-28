# Compiling the latest OpenSSL for Android

I created this to specifically answer the question on stackoverflow (http://stackoverflow.com/a/37043683/2210080) with regards to building the latest OpenSSL. It has been a big pain for me and I would like to help people on how to go about this. For this guide, I am using the version openssl-1.0.2g and Android NDK32 r10b. Do the following commands via terminal: 
 
    $ rm -rf openssl-1.0.2g/
    $ tar xzf openssl-1.0.2g.tar.gz
    $ chmod a+x setenv-android.sh
    $ . ./setenv-android.sh ---> Note: make sure in the same folder of your openssl-1.0.2g
    $ cd openssl-1.0.2g/
        
    $ perl -pi -e 's/install: all install_docs install_sw/install: install_docs install_sw/g' Makefile.org
    
    # Use this if for ArmV7 
    $ ./config shared no-ssl2 no-ssl3 no-comp no-hw no-engine --openssldir=<Path of your OpenSSL> 
    # Use this if for old Arm 
    $ ./Configure android shared no-ssl2 no-ssl3 no-comp no-hw no-engine --openssldir=<Path of your OpenSSL> 
    # Use this if for x86
    $ ./Configure android-x86 shared no-ssl2 no-ssl3 no-comp no-hw no-engine --openssldir=<Path of your OpenSSL> 
        
    $ make depend
    $ make clean
    $ make all
    before make install, ---Delete the "include" folder (path/of/your/openssl-1.0.2g/include)  or you may move it to another directory for safe keeping. 
    $ make install 


Note:

Make sure that you input the right NDK paths into your setenv-android.sh or else you will have errors. Get the proper scripts for setenv-android.sh that are needed to build OpenSSL for different architectures (ArmV7, old Arm, and Android x86). 

Example for this build I used Android NDK vr10b (http://dl.google.com/android/ndk/android-ndk32-r10b-darwin-x86.tar.bz2) 
 and used the ff path values inside my setenv-android.sh file:

    _ANDROID_NDK="android-ndk-r10b" (Line 12)
    _ANDROID_EABI="arm-linux-androideabi-4.8"(Line 16)
    _ANDROID_API="android-19"(Line 24)

They will differ via on the architecture(ArmV7, x86, etc) that you want the OpenSSL to build on. Please refer to the files I uploaded on this for x86: OpenSSL/x86/ and ArmV7: OpenSSL/ArmV7/ 

TIP: 
- If you want to change or remove the SHLIB_VERSION_NUMBER of your libcrypto and libssl files. Go to <path of your opensssl>/crypto/opensslv.h and change SHLIB_VERSION_NUMBER to whichever you like. 

- Also if the scripts given are not working for you, you may do it manually: Please see Issue: https://github.com/rjmangubat23/OpenSSL/issues/1 (Special thanks to Luiz C. Valdetaro, for pointing this out to me) 


Reference:

https://wiki.openssl.org/index.php/Android

https://github.com/seabat/openssl-android

Download Openssl here: ftp://ftp.openssl.org/source

Download Complete list of Android NDK files here: https://developer.android.com/ndk/downloads/index.html

If this has helped you in anyway feel free to share this to other people who are having problems on this. Also please upvote my answer on Stackoverflow: http://stackoverflow.com/a/37043683/2210080 that would mean a lot to me. Thank you!

If you have any questions, feel free to email me: mangubatrj@gmail.com
