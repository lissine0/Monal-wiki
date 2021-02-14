## Software needed to build Monal:
- Cocoapods
- Xcode
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
