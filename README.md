Project Robust
=======================

This project includes Android fullstack including our own Custom Android OS and Applications whose build system is synced with [Jenkins](http://badwolf.network:8081/).

# RobustOS

- A free and open-source aftermarket distribution, based on the Android Open-Source Platform(AOSP), aiming to give you the cleanest possible alternative and a perfectly stable, smooth and beautiful experience right out of the box.
- We aim to
    - Provide AOSP security patches, Linux and CodeAurora tags being merged within hours of its release, you are sure to receive the latest security fixes and updates on your device as soon as possible!
    - We work on the ROM to make it extremely stable; we believe in the user not facing any issues regarding their device, flash and forget.
    - It is a distribution that aims to be really minimalistic and beautiful right out of the box. We merge patches from master and other sources to give you the best performance out of your device.
    - The ROM doesn't ship with any sort of bloat, and many hardening patches are in the process of being merged to give you the most secure and bloatfree experience possible.

# Robust Battery App
[Source Code](https://github.com/ProjectRobust/RobustBatteryService) <br/>

- This is our inline app that we ship with the OS itself.
- Our app Robust Battery shows information such as the condition of the device, device temperature, voltage and current while charging the device.
- All of the information is displayed without using any third party API and using Android’s default BatteryManager system service.
- This app is a foreground service which means it will run in foreground on top of the background thread layer and display important info via notification. We have plans to add more information to our notification service like temperature, voltage, current and estimated time of charge and discharge, etc.
- Now you might think that since our app runs always in the foreground there might be two most common issues related to the app.
    - First, the app might consume more battery since it is always running. But it doesn’t. Since most of the information displayed via notification channel is text and the whole data is taken from Android’s native SystemServiceManager so BatteryUsage is minimal.
    - Second, you might think that our app might take in permissions, we do not. We plan to use Android’s own local database to store the usage patterns and not track it.
