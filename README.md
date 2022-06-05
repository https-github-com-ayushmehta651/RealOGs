Project Robust
=======================

Co-authors of the project <a href="https://github.com/debz-g/">Debayan Ghosh Dastider</a>, <a href="https://github.com/madhurmehta007/">Madhur Mehta</a>, <a href="https://github.com/danascape/">Saalim Quadri</a>.
<br/><br/>
This project includes Android fullstack which involves our own Custom Android OS and an Application. The Custom ROM build system is synced with [Jenkins](http://badwolf.network:8081/).

# RobustOS

- A free and open-source aftermarket distribution, based on the Android Open-Source Platform(AOSP), aiming to give you the cleanest possible alternative and a perfectly stable, smooth and beautiful experience right out of the box.

### Problem Statements
- In some devices like Realme and Xiaomi, while setting up these devices for the first time, the software asks the user for a consent in order to provide personalised ads based on the user content. This implies that the user will not have any idea about the information that will be sent to the OEM.
- In most of android devices, OEMs provide extra services or frameworks that run during the background of userspace, which drains a lot amount ouf the battery thus decreasing life expectancy of the android device.
- The extra bloatware applications and servies that are provided in many distributions tend to introduce UI glitches and lags that slows down the system.

- We aim to
    - Work on the ROM to make it extremely stable; we believe in the user not facing any issues regarding their device, flash and forget.
    - To be really minimalistic and beautiful right out of the box. We merge patches from master and other sources to give you the best performance out of your device.
    - Ship without any sort of bloat, and many hardening patches are in the process of being merged to give you the most secure and bloatfree experience possible.
    - Provide AOSP security patches, Linux and CodeAurora tags being merged within hours of its release, you are sure to receive the latest security fixes and updates on your device as soon as possible!
- Source Code is publicly available to sync and compile at our [GitHub Organization](https://github.com/ProjectRobust).

# Robust Battery App
[![Android CI](https://github.com/ProjectRobust/RobustBatteryService/actions/workflows/android.yml/badge.svg)](https://github.com/ProjectRobust/RobustBatteryService/actions/workflows/android.yml)
<br/><br/>
[Source Code](https://github.com/ProjectRobust/RobustBatteryService)
<br/>

- This is our inline app that we ship with the OS itself.
- Our app Robust Battery shows information such as the condition of the device, device temperature, voltage and current while charging the device.
- All of the information is displayed without using any third party API and using Android’s default BatteryManager system service.
- This app is a foreground service which means it will run in foreground on top of the background thread layer and display important info via notification. We have plans to add more information to our notification service like temperature, voltage, current and estimated time of charge and discharge, etc.
- Now you might think that since our app runs always in the foreground there might be two most common issues related to the app.
    - First, the app might consume more battery since it is always running. But it doesn’t. Since most of the information displayed via notification channel is text and the whole data is taken from Android’s native SystemServiceManager so BatteryUsage is minimal.
    - Second, you might think that our app might take in permissions, we do not. We plan to use Android’s own local database to store the usage patterns and not track it.

## RobustOS CodeBase
**The repositories below are listed according to decreasing priorities.**
<br/>
**The testing device used for bringup of Custom ROM is Redmi Note 8(Codename :- ginkgo).**

[ci_scripts](https://github.com/ProjectRobust/ci_scripts) :- This repository contains the shell script that is used by the CI to build RobustOS. The script is made specifically for ginkgo device. The script downloads and checks out the source code, the script also has an option to give your build updates on telegram. The script asks for necessary build flavors that are needed according to the user.

[device_xiaomi_ginkgo](https://github.com/ProjectRobust/device_xiaomi_ginkgo) :- This is the repository brought from scratch and consists of device specific configurations that are needed to boot RobustOS on the device with no issues whatsoever. This repository also consists of the necessary Makefiles that are needed to call this specific device product in order to start the build. This also includes necessary build time flags that are used to call the ROM vendor repository in order to bringout ROM specific customizations.

[device_xiaomi_ginkgo-sepolicy](https://github.com/ProjectRobust/device_xiaomi_ginkgo-sepolicy) :- This repository consists of the SELinux rules that are needed for the device to function well with no issues. 
SELinux is part of the Android Security Model. It stands for Security Enhanced Linux and is used to enforce mandatory access control(MAC) over all processes that are running inside the Android userspace, it also enforces the processes that are running with root/superuser privileges. It also enforces security over kernel namespace.

[platform_manifest](https://github.com/ProjectRobust/platform_manifest) :- The initial repository of AOSP project, it contains the list of repositories tracked from [android.googlesource.com](http://android.googlesource.com) and additional repositories tracked from our own organization.
This repository is used to download the source code of AOSP. Since there are more than 1000 repositories that are required for building android, rather than cloning each repository individually, the ‘repo’ command enables us to sync these repositories in one go. The ‘repo’ package finds a default.xml on the given remote in order to start syncing the repositories, this default.xml can track other XMLs for more additional repositories that may be required for device specific configurations.

[platform_vendor_robust](https://github.com/ProjectRobust/platform_vendor_robust) :- This is the heart of our AOSP custom ROM, the repository includes all the configurations required to call out the extra Qualcomm repositories that are tracked from LineageOS Organization.  This repository also includes overlays that tweaks out the UI of the OS in order to make it look sleek and better to the user. This repository also includes the kernel build system that can build the Linux Kernel Source Code from source, pure AOSP does not include this support.

[kernel_xiaomi_ginkgo](https://github.com/ProjectRobust/kernel_xiaomi_ginkgo) :- This repository consists of the linux kernel source code that is used to boot the ginkgo device. The kernel source code is forked and merged with Qualcomm Code Aurora Forum (CAF) Tag on top of it, along with the needed changes and extra drivers that are needed to boot the ‘ginkgo’ device.

[device_xiaomi_ginkgo-kernel](https://github.com/ProjectRobust/device_xiaomi_ginkgo-kernel) :- This is the repository that consists of the prebuilt kernel binaries built from the provided kernel source.

[vendor_xiaomi_ginkgo](https://github.com/ProjectRobust/vendor_xiaomi_ginkgo) :- This repository consists of the proprietary binaries that are provided by Stock OEM with no source code, so they are copied directly after cleaning up the unneeded libraries, these unneeded repositories consists of the unused frameworks and libraries that are either left unused or are not required by the Android userspace.

[platform_vendor_robust-prebuilts](https://github.com/ProjectRobust/platform_vendor_robust-prebuilts) :- This repository consists of the prebuilt application binaries that are being shipped inline with the custom ROM.

[platform_build](https://github.com/ProjectRobust/platform_build) :- This consist of the Android build system that is required to build the libraries, frameworks, applications, etc. This also consists of the environment setup script that is needed in order to setup the environment to build Android Source Code. Android uses Make, Ninja and Soong in its build system.

[platform_frameworks](https://github.com/ProjectRobust/platform_frameworks_base) :-  It consists of the application framework, written in C++ and java. It contains all of the system services and core implementation of Android.

[platform_bionic](https://github.com/ProjectRobust/platform_bionic) :- This repository consists of Andoid’s C library like libc, dynamic linker and math.
