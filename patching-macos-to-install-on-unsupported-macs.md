---
title: Patching macOS to install on unsupported Macs
---

Who am I?
My name is Julian Fairfax and I’m the founder and leader of Research, Modification, Customization, and it’s team of researchers, developers, and more.

What is an unsupported Mac?
A Mac becomes unsupported when Apple’s latest operating system no longer runs on it, without our patches, of course.

Why should I run a patched version of macOS on my unsupported Mac?
A newer version of macOS means you’ll have better security, and better support for the apps you want to use.

Why should I learn how to patch macOS?
If you use an automatic patcher tool, you won’t have to do any work by yourself in order to patch macOS, but it’s still cool to know what your tool is doing, isn’t it? If you’d like to develop your own patcher tool, this writeup is a good place to start!


How do I create the installer drive
The installer disk images were in the InstallESD.dmg up to 10.13, when they were moved to /Contents/SharedSupport, set the <installer_images_path> variable accordingly.
Apple’s “modern” installers use signature checks, meaning you can’t modify the installer files, to create a modifiable installer drive, you have to use the following commands, with your proper installer images path and volume paths:

- asr restore -source <installer_images_path>/BaseSystem.dmg -target <installer_volume_path> -noprompt -noverify -erase
- rm <installer_volume_path>/System/Installation/Packages
- cp -R <installesd_mount_path>/Packages <installer_volume_path>/System/Installation/
- cp <installer_images_path>/BaseSystem.dmg <installer_volume_path>/
- cp <installer_images_path>/BaseSystem.chunklist <installer_volume_path>/
- 
- cp <installesd_mount_path>/mach_kernel <installer_volume_path>/

For 10.9, from a full installation

- cp <resources path>/mach_kernel <installer_volume_path>/

For 10.10/10.11, from a full installation

- mkdir -p <installer_volume_path>/System/Library/Kernels
- cp  <resources path>/kernel <installer_volume_path>/System/Library/Kernels

You have to patch the OSInstall distribution file to return true on platform compatibility checks. You can do so by running these commands:

- pkgutil --expand <installer_volume_path>/tmp/OSInstall.mpkg <installer_volume_path>/tmp/OSInstall
- sed -i '' 's/cpuFeatures\[i\] == "VMM"/1 == 1/' <installer_volume_path>/tmp/OSInstall/Distribution
- sed -i '' 's/boardID == platformSupportValues\[i\]/1 == 1/' <installer_volume_path>/tmp/OSInstall/Distribution
- sed -i '' 's/!boardID || platformSupportValues.length == 0/1 == 0/' <installer_volume_path>/tmp/OSInstall/Distribution
- pkgutil --flatten <installer_volume_path>/tmp/OSInstall <installer_volume_path>/tmp/OSInstall.mpkg


OS X 10.8 Mountain Lion

The 32-bit firmware problem
Most older Intel Macs have 64-bit CPUs but still use 32-bit firmware, so they can’t load a 64-bit kernel. The MacBook3,1 and MacBook4,1 both have 64-bit firmware but still try to load a 32-bit kernel. The best solution is to use the official file from Yosemite, which seems to work without patches!

If you compile Apple’s boot.efi yourself, you can add support for Macs with 32-bit firmware. Due to the efforts of tiamo and Piker Alpha, you can download pre-compiled copies from patchers. I used efilipo to combine the compiled 32-bit copy and Yosemite file into one single boot.efi file which supports all unsupported Macs.


OS X 10.11 El Capitan

The 32-bit firmware problem
Most older Intel Macs have 64-bit CPUs but still use 32-bit firmware, so they can’t load a 64-bit kernel. El Capitan updated the way kernel cache is handled, and thus needs a recompiled boot.efi file for Macs with 32-bit firmware.

If you compile Apple’s boot.efi yourself, you can add support for Macs with 32-bit firmware. Due to the efforts of tiamo and Piker Alpha, you can download pre-compiled copies from patchers. I used efilipo to combine the recompiled 32-bit copy and stock file into one single boot.efi file which supports all unsupported Macs.

What new patches do I have to use for this version?
You have to copy the drivers to a full installation and rebuild the prelinkedkernel from there.
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

What new steps do I have to use for this version?
El Capitan updated the way kernel cache, which stores cached versions of drivers, is handled. You now have to update it after replacing any drivers. You can do so by running “kextcache -f -u”.

You have to copy the new AppleDiagnostics.dmg after copying the BaseSystem.dmg You can do so with the following commands:

- cp <installer_images_path>/AppleDiagnostics.dmg <installer_volume_path>/
- cp <installer_images_path>/AppleDiagnostics.chunklist <installer_volume_path>/


macOS 10.12 Sierra

What new patches do I have to use for this version?
You have to copy the drivers to a full installation and rebuild the prelinkedkernel from there.
You have to replace this one with an older version from 10.12.6:

- macOS Installer.app (in /System/Installation/CDIS)

You have to replace this one with a modified version of the stock 10.12.6 copy:

- Quartz.framework (in /System/Library/Frameworks)

Specifically, replace this file with the current version from /Versions/A/Frameworks:

- QuickLookUI.framework

You have to replace this one with an older version from 10.12 beta 1:

- OSInstaller.framework (in /System/Library/PrivateFrameworks) 


You have to add these custom files from parrotgeek1:

- LegacyUSBInjector.kext
- SIPManager.kext

What new steps do I have to use for this version?
Sierra updated the command for updating the kernel cache, which stores cached versions of drivers. You now have to update it by running “kextcache -i” or “kextcache -u”.


macOS 10.14 Mojave

What new patches do I have to use for this version?
You have to copy the drivers to a full installation and rebuild the prelinkedkernel from there.
You have to replace these with older versions from 10.13.6: 

- IOUSBFamily.kext
- IOUSBHostFamily.kext
- SystemMigration.framework (in /System/Library/PrivateFrameworks)
- SystemMigrationUtils.framework (in /System/Library/PrivateFrameworks)


macOS 10.15 Catalina

The modern installer problem
Catalina added a new read-only system volume which only works with Apple’s modern installer. After creating the installer drive with openinstallmedia (for versions older than 10.9), you need to mount the BaseSystem.dmg and InstallESD.dmg as shadows, then convert both to read-only, using the following commands:

- hdiutil attach -owners on <installer_sharedsupport_path>/BaseSystem.dmg -mountpoint /tmp/Base\ System -nobrowse -noverify -shadow
- hdiutil convert -format UDZO <installer_sharedsupport_path>/BaseSystem.dmg -o <installer_volume_path/installer_application>/Contents/SharedSupport/BaseSystem.dmg -shadow
- hdiutil attach -owners on <installer_sharedsupport_path>/InstallESD.dmg -mountpoint /tmp/InstallESD -nobrowse -noverify -shadow
- hdiutil convert -format UDZO <installer_sharedsupport_path>/InstallESD.dmg -o <installer_volume_path/installer_application>/Contents/SharedSupport/InstallESD.dmg -shadow

dosdude1 patched installer binaries to allow us to modify the installer files without tripping any signature checks. They’re more of a workaround, than a proper solution, and have to be updated for most new Catalina releases. dosdude1 also uses them to run scripts for the APFS software and post-install patches, you may need to replace these with your own scripts/the stock binaries, and sign them with “codesign -f -s”:

- Replace /sbin/apfsbless with /usr/sbin/bless in brtool
- Replace /sbin/runposti with /sbin/shutdown in OSInstaller
- Replace /sbin/apfsinsta with /usr/sbin/nvram in osishelperd
- Replace /sbin/shutdown with /sbin/apfsprep in osishelperd (for installing the APFS software patch)

The APFS firmware problem
The new read-only system volume which only works with APFS. Supported Macs can use it through a firmware update which was bundled with the High Sierra update. Unsupported Macs can’t boot from APFS volumes since they didn’t receive the firmware update.

You can work around this by using an EFI shell script, which loads the stock APFS driver, and boots from the predefined volumes. To do this you’ll have to copy two files into the EFI partition along with the apfs.efi file from /usr/standalone/i386/apfs.efi (this should be dynamically copied by apfsprep before booting to stage 2 of the installer.)

What new patches do I have to use for this version?
You have to copy the drivers to a full installation and rebuild the prelinkedkernel from there.
You have to add this custom file:

- DisableLibraryValidation.kext

You have to replace these with modified files from dosdude1:
 
- <basesystem_mount_path>/usr/libexec/brtool
- <basesystem_mount_path>/System/Library/PrivateFrameworks/OSInstaller.framework/Versions/A/OSInstaller
- <installer_volume_path/installer_application>/Contents/Frameworks/OSInstallerSetup.framework/Versions/A/Frameworks/OSInstallerSetupInternal.framework/Versions/A/OSInstallerSetupInternal
- <basesystem_mount_path/installer_application>/Contents/Frameworks/OSInstallerSetup.framework/Versions/A/Frameworks/OSInstallerSetupInternal.framework/Versions/A/OSInstallerSetupInternal
- <installer_volume_path/installer_application>/Contents/Frameworks/OSInstallerSetup.framework/Versions/A/Resources/osishelperd
- <basesystem_mount_path/installer_application>/Contents/Frameworks/OSInstallerSetup.framework/Versions/A/Resources/osishelperd
