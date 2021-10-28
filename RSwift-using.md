# R.Swift library
## _Another way to store resources_


### Why should I use this
It makes your code that uses resources:

- Fully typed, less casting and guessing what a method will return
- Compile time checked, no more incorrect strings that make your app crash at runtime
- Autocompleted, never have to guess that image name again

Currently you type:
```sh
let icon = UIImage(named: "settings-icon")
let font = UIFont(name: "San Francisco", size: 42)
let color = UIColor(named: "indicator highlight")
```
With R.swift it becomes:
```sh
let icon = R.image.settingsIcon()
let font = R.font.sanFrancisco(size: 42)
let color = R.color.indicatorHighlight()
```
_Note on Carthage_: `R.swift` is a tool used in a build step, it is not a dynamic library. Therefore it is not possible to install it with Carthage.

## Installation

### CocoaPods (recommended)
- Add pod `R.swift` to your Podfile and run pod install
- In Xcode: Click on your project in the file list, choose your target under TARGETS, click the Build Phases tab and add a New Run Script Phase by clicking the little plus icon in the top left
- Drag the new Run Script phase above the `Compile Sources` phase and below `Check Pods Manifest.lock`, expand it and paste the following script:
```sh
if [ $ACTION != "indexbuild" ]; then
  "$PODS_ROOT/R.swift/rswift" generate "$SRCROOT/R.generated.swift"
fi
```
- Add `$TEMP_DIR/rswift-lastrun` to the "Input Files" and `$SRCROOT/R.generated.swift` to the "Output Files" of the Build Phase
- Build your project, in Finder you will now see a `R.generated.swift` in the `$SRCROOT-folder`, drag the `R.generated.swift` files into your project and uncheck _Copy items if needed_
