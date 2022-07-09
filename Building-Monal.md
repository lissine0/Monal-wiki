## Software needed to build Monal:
- CocoaPods
- Xcode (only runs on macOS, see below if you don't own a Mac)
- git 

## Build steps:
1. clone repo
```bash
git clone https://github.com/monal-im/Monal.git Monal-IM
cd Monal-IM
```
2. init and update submodules (localizations)
```bash
git submodule update --remote --init
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

## Alpha builds (bleeding edge)
If you want to live on the edge and use all new bleeding-edge features that just got implemented, you can use the alpha builds of Monal, too.
Just sent the UDID of your device (the serial number visible via `lsusb` on a Linux system) to [info@monal-im.org](mailto:info@monal-im.org). Once your device has been added, you can [download and install](https://www.eightysoft.de/monal) the build. For each new commit to the develop branch a new build will go down the pipeline.

**Please be reminded that the alpha builds obviously might be unstable, slower or come with other severe issues.**

Read here how to use logging with the [Monal UDP Logger](https://github.com/monal-im/Monal/wiki/Introduction-to-Monal-Logging) to debug things.