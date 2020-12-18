---
title: Patching macOS to run on unsupported Macs
---


### Who am I?
My name is Julian Fairfax and I’m the founder and leader of Research, Modification, Customization, and it’s team of researchers, developers, and more.

### What is an unsupported Mac?
A Mac becomes unsupported when Apple’s latest operating system no longer runs on it, without our patches, of course.

### Why should I run a patched version of macOS on my unsupported Mac?
A newer version of macOS means you’ll have better security, and better support for the apps you want to use.

### Why should I learn how to patch macOS?
If you use an automatic patcher tool, you won’t have to do any work by yourself in order to patch macOS, but it’s still cool to know what your tool is doing, isn’t it? If you’d like to develop your own patcher tool, this writeup is a good place to start!


## OS X 10.8 Mountain Lion

### What Macs became unsupported with this version’s release?

- iMac5,1
- iMac5,2
- iMac6,1
- MacBook2,1
- MacBook3,1
- MacBook4,1
- MacBookAir1,1
- MacBookPro2,1
- MacBookPro2,2
- Macmini2,1
- MacPro1,1
- MacPro2,1
- Xserve1,1
- Xserve2,1

### The 32-bit driver problem
The Intel and Nvidia graphics drivers were written before 64-bit support was common. Mountain Lion has a 64-bit kernel and no longer supports loading 32-bit drivers. This isn’t a problem for ATI cards since they have 64-bit drivers.

Mountain Lion beta 1 had a 32-bit kernel, which you can use on newer versions. However, this also requires replacing a bunch of system components with 32-bit copies from the beta. This method supports graphics acceleration on all Macs. With the stock kernel, you can only achieve graphics acceleration on ATI cards.

### The 32-bit firmware problem
Most older Intel Macs have 64-bit CPUs but still use 32-bit firmware, so they can’t load a 64-bit kernel. The MacBook3,1 and MacBook4,1 both have 64-bit firmware but still try to load a 32-bit kernel. The best solution is to use the official file from Yosemite, which seems to work without patches!

If you compile Apple’s boot.efi yourself, you can add support for Macs with 32-bit firmware. Due to the efforts of tiamo and Piker Alpha, you can download pre-compiled copies from patchers. I used efilipo to combine the compiled 32-bit copy and Yosemite file into one single boot.efi file which supports all unsupported Macs.

### What tools can I use/browse for more information?
parrotgeek1 recently released NexPostFacto 10.8 32-bit for running Mountain Lion on unsupported Macs and NexPostFacto 10.8 64-bit for unsupported Macs with ATI cards.

I also released a tool of my own, OS X Patcher, which doesn’t support graphics acceleration on any Mac, but it’s still useful for some!

### What new patches do I have to use for this version?
Delete all ATI and AMD drivers before replacing them, otherwise your system won’t boot.

You have to replace these with older versions from 10.6.2 beta 1 (for 64-bit mode):

- AppleIntelGMA950.kext
- AppleIntelGMA950GA.plugin
- AppleIntelGMA950GLDriver.bundle
- AppleIntelGMA950VADriver.bundle
- AppleIntelGMAX3100.kext
- AppleIntelGMAX3100FB.kext
- AppleIntelGMAX3100GA.plugin
- AppleIntelGMAX3100GLDriver.bundle
- AppleIntelGMAX3100VADriver.bundle
- AppleIntelIntegratedFramebuffer.kext
- GeForce.kext
- GeForce7xxxGLDriver.bundle
- GeForce8xxxGLDriver.bundle
- GeForceGA.plugin
- GeForceVADriver.bundle
- NVDANV40Hal.kext
- NVDANV50Hal.kext
- NVDAResman.kext

Or replace these with older versions from 10.7.5 (for 32-bit mode):

- AppleIntelGMA950.kext
- AppleIntelGMA950GA.plugin
- AppleIntelGMA950GLDriver.bundle
- AppleIntelGMA950VADriver.bundle
- AppleIntelGMAX3100.kext
- AppleIntelGMAX3100FB.kext
- AppleIntelGMAX3100GA.plugin
- AppleIntelGMAX3100GLDriver.bundle
- AppleIntelGMAX3100VADriver.bundle
- AppleIntelIntegratedFramebuffer.kext
- GeForce.kext
- GeForce7xxx.kext
- GeForce7xxxGA.plugin
- GeForce7xxxGLDriver.bundle
- GeForce7xxxVADriver.bundle
- GeForceGA.plugin
- GeForceGLDriver.bundle
- GeForceVADriver.bundle
- NVDAGF100Hal.kext
- NVDAGK100Hal.kext
- NVDANV40HalG7xxx.kext
- NVDANV50Hal.kext
- NVDAResman.kext
- NVDAResmanG7xxx.kext

You have to replace these with older versions from 10.7.5:

- AppleHDA.kext
- ATI1300Controller.kext
- ATI1600Controller.kext
- ATI1900Controller.kext
- ATIFramebuffer.kext
- ATIRadeonX1000.kext
- ATIRadeonX1000GA.plugin
- ATIRadeonX1000GLDriver.bundle
- ATIRadeonX1000VADriver.bundle
- ATISupport.kext

You have to replace this one with an older version from 10.8.4:

- IOAudioFamily.kext


## OS X 10.9 Mavericks

### What tools can I use/browse for more information?
parrotgeek1 recently released NexPostFacto 10.9 for running Mavericks on unsupported Macs with ATI cards.

I also released a tool of my own, OS X Patcher, which doesn’t support graphics acceleration on any Mac, but it’s still useful for some!


## OS X 10.10 Yosemite

### What tools can I use/browse for more information?
Acceleration may be possible on unsupported Macs with ATI cards but no tool has been released.

I released a tool of my own, OS X Patcher, which doesn’t support graphics acceleration, but it’s still useful for some!


## OS X 10.11 El Capitan

### The 32-bit firmware problem
Most older Intel Macs have 64-bit CPUs but still use 32-bit firmware, so they can’t load a 64-bit kernel. El Capitan updated the way kernel cache is handled, and thus needs a recompiled boot.efi file for Macs with 32-bit firmware.

If you compile Apple’s boot.efi yourself, you can add support for Macs with 32-bit firmware. Due to the efforts of tiamo and Piker Alpha, you can download pre-compiled copies from patchers. I used efilipo to combine the recompiled 32-bit copy and stock file into one single boot.efi file which supports all unsupported Macs.

### What tools can I use/browse for more information?
Acceleration may be possible on unsupported Macs with ATI cards but no tool has been released.

I released a tool of my own, OS X Patcher, which doesn’t support graphics acceleration, but it’s still useful for some!

### What new patches do I have to use for this version?
El Capitan updated drivers for input devices such as the mouse and keyboard, you have to replace these with older versions from 10.10.5:

- AppleHIDMouse.kext
- AppleTopCase.kext
- AppleUSBMultitouch.kext
- AppleUSBTopCase.kext
- IOBDStorageFamily.kext
- IOBluetoothFamily.kext
- IOBluetoothHIDDriver.kext
- IOSerialFamily.kext
- IOUSBFamily.kext
- IOUSBMassStorageClass.kext

And this one with a modified version of the stock 10.11.5 copy:

- IOUSBHostFamily.kext

Specifically, remove the following files from Contents/PlugIns:

- AppleUSBEHCI.kext
- AppleUSBEHCIPCI.kext
- AppleUSBOHCI.kext
- AppleUSBOHCIPCI.kext
- AppleUSBUHCI.kext
- AppleUSBUHCIPCI.kext

### What new steps do I have to use for this version?
El Capitan updated the way kernel cache, which stores cached versions of drivers, is handled. You now have to update it after replacing any drivers. You can do so by running “kextcache -f -u”.


## macOS 10.12 Sierra

### What Macs became unsupported with this version’s release?

- iMac7,1
- iMac8,1
- iMac9,1
- MacBook5,1
- MacBook5,2
- MacBookAir2,1
- MacBookPro4,1
- MacBookPro5,1
- MacBookPro5,2
- MacBookPro5,3
- MacBookPro5,4
- MacBookPro5,5
- Macmini3,1
- MacPro3,1
- MacPro4,1
- Xserve2,1
- Xserve3,1

### What Macs are still unsupported (but supported by patchers)?

- MacBook4,1

### What tools can I use/browse for more information?
dosdude1 released macOS Sierra Patcher, a simple to use app for running Sierra on unsupported Macs.

I released a tool of my own, macOS Patcher, which uses a command-line interface instead of an app, but works in a similar way. It also supports the MacBook4,1, but without graphics acceleration.

### What new patches do I have to use for this version?
You have to replace these with older versions from 10.11.5:

- AmbientLightSensorHID.plugin (in /System/Library/Extensions/AppleSMCLMU.kext/Contents/PlugIns)
- AppleAirPortBrcm43224.kext
- AppleHDA.kext
- corecapture.kext
- CoreCaptureResponder.kext 
- IO80211Family.kext
- IOAudioFamily.kext

You have to add these custom files from parrotgeek1:

- LegacyUSBEthernet.kext
- LegacyUSBInjector.kext
- LegacyUSBVideoSupport.kext
- SIPManager.kext
- Trackpad.prefPane (in /System/Library/PreferencePanes)

You have to add these custom files from Czo:

- SUVMMFaker.dylib (in /usr/lib)
- com.apple.softwareupdated.plist (in /System/Library/LaunchDaemons)

### What new steps do I have to use for this version?
Sierra updated the command for updating the kernel cache, which stores cached versions of drivers. You now have to update it by running “kextcache -i” or “kextcache -u”.


## macOS 10.13 High Sierra

### The APFS firmware problem
High Sierra introduced a new Apple File System (APFS) optimised for Solid State Drives (SSDs). Supported Macs can use it through a firmware update which was bundled with the High Sierra update. Unsupported Macs can’t boot from APFS volumes since they didn’t receive the firmware update.

You can work around this by using an EFI shell script, which loads the stock APFS driver, and boots from the predefined volumes. To do this you’ll have to copy two files into the EFI partition along with the apfs.efi file from /usr/standalone/i386/apfs.efi (this should be dynamically copied by your patch tool)

### What tools can I use/browse for more information?
dosdude1 released macOS High Sierra Patcher, a simple to use app for running High Sierra on unsupported Macs.

I released a tool of my own, macOS Patcher, which uses a command-line interface instead of an app, but works in a similar way. It also supports the MacBook4,1, but without graphics acceleration.

### What new patches do I have to use for this version?
You have to replace these with older versions from 10.12.6:

- DisplayServices.framework (in /System/Library/PrivateFrameworks)
- AMDRadeonX3000.kext
- AMDRadeonX3000GLDriver.bundle
- AMDRadeonX4000.kext
- AMDRadeonX4000GLDriver.bundle
- AppleBacklight.kext
- AppleBacklightExpert.kext
- AppleUSBTopCase.kext
- IOAccelerator2D.plugin
- IOAcceleratorFamily2.kext

### What new steps do I have to use for this version?
The PlatformSupport.plist file has to be deleted from the Preboot volume too. Your patch tool should find the UUID of your system volume, then mount the Preboot volume and delete this file: /UUID/System/Library/CoreServices/PlatformSupport.plist


## macOS 10.14 Mojave

### What Macs became unsupported with this version’s release?

- iMac10,1
- iMac10,2
- iMac11,1
- iMac11,2
- iMac11,3
- iMac12,1
- iMac12,2
- MacBook6,1
- MacBook7,1
- MacBookAir3,1
- MacBookAir3,2
- MacBookAir4,1
- MacBookAir4,2
- MacBookPro6,1
- MacBookPro6,2
- MacBookPro7,1
- MacBookPro8,1
- MacBookPro8,2
- MacBookPro8,3
- Macmini4,1
- Macmini5,1
- Macmini5,2
- Macmini5,3
- MacPro4,1

### What Macs are still unsupported (but supported by patchers)?

- iMac7,1
- iMac8,1
- iMac9,1
- MacBook4,1
- MacBook5,1
- MacBook5,2
- MacBookAir2,1
- MacBookPro4,1
- MacBookPro5,1
- MacBookPro5,2
- MacBookPro5,3
- MacBookPro5,4
- MacBookPro5,5
- Macmini3,1
- MacPro3,1
- MacPro4,1
- Xserve2,1
- Xserve3,1

### What tools can I use/browse for more information?
dosdude1 released macOS Mojave Patcher, a simple to use app for running Mojave on unsupported Macs.

I released a tool of my own, macOS Patcher, which uses a command-line interface instead of an app, but works in a similar way. It also supports the MacBook4,1, but without graphics acceleration.

### What new patches do I have to use for this version?
You have to replace these with older versions from 10.13.6:

- AirPortAtheros40.kext (in /System/Library/Extensions/IO80211Family.kext/Contents/PlugIns)
- AMD2400Controller.kext
- AMD2600Controller.kext
- AMD3800Controller.kext
- AMD4600Controller.kext
- AMD4800Controller.kext
- AMD5000Controller.kext
- AMD6000Controller.kext
- AMDFramebuffer.kext
- AMDLegacyFramebuffer.kext
- AMDLegacySupport.kext
- AMDRadeonVADriver.bundle
- AMDRadeonVADriver2.bundle
- AMDRadeonX4000HWServices.kext
- AMDShared.bundle
- AMDSupport.kext
- AppleGraphicsControl.kext
- AppleGraphicsPowerManagement.kext
- AppleIntelFramebufferAzul.kext
- AppleIntelFramebufferCapri.kext
- AppleIntelHD3000Graphics.kext
- AppleIntelHD3000GraphicsGA.plugin
- AppleIntelHD3000GraphicsGLDriver.bundle
- AppleIntelHD3000GraphicsVADriver.bundle
- AppleIntelHDGraphics.kext
- AppleIntelHDGraphicsFB.kext
- AppleIntelHDGraphicsGA.plugin
- AppleIntelHDGraphicsGLDriver.bundle
- AppleIntelHDGraphicsVADriver.bundle
- AppleIntelSNBGraphicsFB.kext
- AppleIntelSNBVA.bundle
- AppleMCCSControl.kext
- AppleUSBACM.kext
- ATIRadeonX2000.kext
- ATIRadeonX2000GA.plugin
- ATIRadeonX2000GLDriver.bundle
- ATIRadeonX2000VADriver.bundle
- GeForceTesla.kext
- GeForceTeslaGLDriver.bundle
- GeForceTeslaVADriver.bundle
- GPUWrangler.framework (in /System/Library/PrivateFrameworks)
- IOGraphicsFamily.kext
- IONDRVSupport.kext
- IOUSBFamily.kext
- IOUSBHostFamily.kext
- NVDANV50HalTesla.kext
- NVDAResmanTesla.kext

You have to replace these with older versions from 10.14.3:

- libGPUSupport.dylib (in /System/Library/PrivateFrameworks/GPUSupport.framework/Versions/A/Libraries)
- OpenGL.framework (in /System/Library/Frameworks)
- SiriUI.framework (in /System/Library/PrivateFrameworks)

You have to replace this one with an older version from 10.14.4:

- CoreDisplay.framework (in /System/Library/Frameworks)

You have to add these custom files from Syncretic:

- AAAMouSSE.kext
- AAAtelemetrap.kext

You have to replace this one with a modified file from ASentientBot:

- SkyLight.framework in (/System/Library/PrivateFrameworks)


## macOS 10.15 Catalina

### What Macs became unsupported with this version’s release?

- MacPro5,1

### The non-Metal acceleration problem
With the release of Mojave, support for Macs without Apple’s Metal graphics framework was dropped. This wasn’t too much of a problem since older versions of Mojave drivers and frameworks were all that was required to patch it. However, Catalina introduced some more changes to two of those, so they couldn’t be replaced.

ASentientBot created wrappers to port the Mojave versions of CoreDisplay and Skylight to Catalina. The wrappers are stable enough to be used on a daily driver but they’re more of a workaround, than a proper solution, and have to be updated for most new Catalina releases.

### The Library Validation problem
The acceleration wrappers unfortunately trip one of Apple’s security systems: Library Validation. This is due to WindowServer, conflicting with the SkyLight wrapper, which replaces the original binary.

You can disable Library Validation by running “sudo defaults write /Library/Preferences/com.apple.security.libraryvalidation.plist DisableLibraryValidation -bool true”. This requires System Integrity Protection (SIP) to be disabled as well, which can be done in two ways: a patched boot.efi file (in /System/Library/CoreServices) or by running “csrutil disable”.

### _The AMFI problem_
_If you’re still unable to boot Catalina, you may have to disable Apple Mobile File Integrity (AMFI) by modifying a file in the Preboot volume. Your patch tool should find the UUID of your system volume, then mount the Preboot volume and add “amfi_get_out_of_my_way=1”to this file: /UUID/Library/Preferences/SystemConfiguration/com.apple.Boot.plist_

_With the latest version of macOS Patcher and it’s patches, you shouldn’t have to use this step._

### What tools can I use/browse for more information?
dosdude1 released macOS Catalina Patcher, a simple to use app for running Catalina on unsupported Macs.

I released a tool of my own, macOS Patcher, which uses a command-line interface instead of an app, but works in a similar way. It also supports the MacBook4,1, but without graphics acceleration.

### What new patches do I have to use for this version?
You have to replace these with older versions from 10.14.6:

- AppleIntelPIIXATA.kext
- AppleYukon2.kext
- IO80211Family.kext
- nvenet.kext

You have to replace these with older versions from 10.15.3:

- MonitorPanel.framework (in /System/Library/PrivateFrameworks)
- MonitorPanels (in /System/Library)

You have to replace this one with an older version from 10.15 beta 6:

- libCoreFSCache.dylib (in /System/Library/Frameworks/OpenGL.framework/Versions/A/Libraries)

You have to replace this one with a modified file from ASentientBot:

- IOSurface.kext

### What new steps do I have to use for this version?
The acceleration wrappers conflict with the dyld cache, which stores cached versions of dylibs. You now have to update it after replacing CoreDisplay and SkyLight. You can do so by running “update_dyld_shared_cache”. Do not run this command on the MacBook4,1.

The patched boot.efi file for disabling Library Validation has to be replaced in the Preboot volume too. Your patch tool should find the UUID of your system volume, then mount the Preboot volume and replace this file: /UUID/System/Library/CoreServices/boot.efi