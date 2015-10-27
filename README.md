# SBShortcutMenuSimulator

`SBShortcutMenuSimulator` is a tweak for the iPhone Simulator that allows you to simulate the new `UIApplicationShortcutItem` API for iPhone with 3D Touch enabled.

## Requirements

- Xcode 7 GM or later, set as your default version of Xcode

## Build

``` sh
git clone https://github.com/DeskConnect/SBShortcutMenuSimulator.git
cd SBShortcutMenuSimulator
make
```

**Note:** If you installed SBShortcutMenuSimulator using the old method, go [here](https://github.com/DeskConnect/SBShortcutMenuSimulator/blob/85c3d73b9e22a20e5c59144fa1b3d19883a68f0e/README.md) and follow the uninstallation directions.

## Quick Setup

For a detailed breakdown of the setup steps, please take a look at the Usage section below, otherwise, do:

- Activate a simulator
- Add this to your `bash_profile` (please modify `PATH_TO_3D_TOUCH` to whatever is on your machine):

```
export PATH_TO_3D_TOUCH="~/git/esplorio/SBShortcutMenuSimulator"

alias setup-3d-touch="cd $PATH_TO_3D_TOUCH && xcrun simctl spawn booted launchctl debug system/com.apple.SpringBoard --environment DYLD_INSERT_LIBRARIES=$PWD/SBShortcutMenuSimulator.dylib && xcrun simctl spawn booted launchctl stop com.apple.SpringBoard"

alias 3d-touch="echo 'io.esplor.ios' | nc 127.0.0.1 7007"
```

- In the command line, run `make` under `PATH_TO_3D_TOUCH`
- Run `setup-3d-touch` to set up the 3D touch server
- Run `3d-touch` to make a call to summon the 3D touch menu

## Usage

First, start SpringBoard with SBShortcutMenuSimulator enabled (run this from the cloned directory):

``` sh
xcrun simctl spawn booted launchctl debug system/com.apple.SpringBoard --environment DYLD_INSERT_LIBRARIES=$PWD/SBShortcutMenuSimulator.dylib
xcrun simctl spawn booted launchctl stop com.apple.SpringBoard
```

Now, to show an app's quick action menu, send the app's bundle identifier over TCP to port 8000. For example, running this command will show the shortcut menu for Calendar:

``` sh
echo 'com.apple.mobilecal' | nc 127.0.0.1 7007
```

<img src="https://raw.githubusercontent.com/DeskConnect/SBShortcutMenuSimulator/screenshot/Shortcuts.png" width="326" height="592"></img>

**NOTICE**: For our own (Esplorio) fork, I have updated the port number from `8000` to `7007` so that we can avoid clashing with the Django server port

## License

SBShortcutMenuSimulator is available under the MIT license. See the LICENSE file for more info.
