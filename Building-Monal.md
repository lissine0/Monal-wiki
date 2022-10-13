## Software needed to build Monal:
- CocoaPods (see [below](#installing-cocoapods))
- Xcode (only runs on macOS, see below if you don't own a Mac)
- git 

## Build steps:
1. clone repo
```bash
git clone https://github.com/monal-im/Monal.git
cd Monal
```
2. init and update submodules (localizations)
```bash
git submodule update --init --recursive
```
3. install dependencies 
```bash
cd Monal
pod install
```
4. open in Xcode and build
```bash
open Monal.xcworkspace
```

Read here how to use logging with the [Monal UDP Logger](https://github.com/monal-im/Monal/wiki/Introduction-to-use-of-Monal-UDP-Logger) to debug things.

## Developing without Mac
If you are interested in building Monal but don't have a Mac you can virtualize:

- [MacOS Bis Sur (current buildserver)](https://github.com/kholia/OSX-KVM)
- [MacOS Catalina (used for old buildserver)](https://github.com/foxlet/macOS-Simple-KVM)
- [Alternative 1](https://github.com/myspaghetti/macos-guest-virtualbox)
- [Alternative 2](https://www.intoguide.com/install-macos-catalina-on-vmware/)
- [Alternative 3](https://techsviewer.com/how-to-install-macos-10-15-catalina-on-vmware-on-windows-pc/)
- [Mac OS Beta ISO](https://gist.github.com/steinybot/105e6631504f1026662035acb4d592b8) as well as the [free preview image](https://apps.apple.com/us/app/macos-catalina/id1466841314?mt=12)

Direct download links to all [XCode versions](https://stackoverflow.com/questions/10335747/how-to-download-xcode-dmg-or-xip-file)
If you want to connect your physical iPhone to XCode inside your VM, [use this (tested by Monal devs)](https://github.com/sickcodes/Docker-OSX#usbfluxd-iphone-usb---network-style-passthrough-osx-kvm-docker-osx)

## Alpha builds (bleeding edge)
If you want to live on the edge and use all new bleeding-edge features that just got implemented, you can use the alpha builds of Monal, too.
Just sent the UDID of your device (the serial number visible via `lsusb` on a Linux system) to [info@monal-im.org](mailto:info@monal-im.org). Once your device has been added, you can [download and install](https://www.eightysoft.de/monal) the build. For each new commit to the develop branch a new build will go down the pipeline.

**Please be reminded that the alpha builds obviously might be unstable, slower or come with other severe issues.**

Read here how to use logging with the [Monal UDP Logger](https://github.com/monal-im/Monal/wiki/Introduction-to-Monal-Logging) to debug things.

# Installing Cocoapods
You'll need to use homebrew to install cocoapods, other ways to install cocoapods may result in strange errors.

## Step #1: Install Homebrew
Go to https://brew.sh/ and follow the instructions to install homebrew.  
Don't forget to follow the "next steps" printed to your terminal once homebrew finishes.

## Step #2: Install Cocoapods via Homebrew
In the terminal type `brew install cocoapods`

Done.


