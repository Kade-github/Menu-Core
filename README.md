# Menu Core
> A FNF helper mod to enable multiple custom main menus and mod content switching.

**Current Funkin' Version:** `0.7.4`

A Friday Night Funkin' mod to enable a custom menu at the start of the game. This menu will allow the user to switch between different mods and their own custom menus, to allow for custom mod content to be enabled/disabled, or grouped together.

<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/52320c53-0084-4494-8376-c11ec65e7125" />

# Download
Head over to the [latest release](https://github.com/Kade-github/Menu-Core/releases/latest), and extract the folder `menu-core` into your mods folder!

## Modders: How to implement?

```haxe
package kade.hex;

import kade.hex.states.HexMainMenu;

import funkin.modding.module.Module;
import flixel.FlxState;

class HMenuCore extends Module {
    var modName = "VS Hex";
    var modDescription = "V.S Hex v3";
    var modAssetKey = "mc_hex";

    var modState = new HexMainMenu();

    public function new() {
        // Priority is set to 3 here.
        super("HMenuCore", 3);
    }
    
    public function isMenuSwitch(state:FlxState):Bool {
        if (state == null || state.rightWatermarkText == null)
            return false;
        
        if (state.rightWatermarkText.text != "menuSwitch")
            return false;
        return true;
    }

    public override function onStateChangeEnd(event:StateChangeScriptEvent):Void {
        if (!isMenuSwitch(event.targetState))
            return;

        event.targetState.addVersion(modName, modAssetKey, modDescription, modState);
        event.targetState.populateVersions();
    }
}
```

You will create a module like so, name it whatever. Make sure it's `priority` is after **2**! After that, copy the two other non-constructor functions and change the top properties to what you'd like!

```haxe
var modName = "VS Hex";
var modDescription = "V.S Hex v3";
var modAssetKey = "mc_hex";
```

Then at the bottom you'll see 
```haxe
var modState = new HexMainMenu();
```

It's very important that you create a new custom state, like so:
```haxe
package kade.hex.states;

import funkin.ui.MusicBeatState;

class HexMainMenu extends MusicBeatState {
    public function new():Void {
        super();
    }

    public override function create():Void {
        super.create();
    }

    public override function update(elapsed:Float):Void {
        super.update(elapsed);
    }
}
```

Then take that state and instantiate it in that variable.

The next step is to take the `mc_template.png` asset and change it to your mod's own icon.

Then put it in your mods `shared/images/` folder, and you'll be done!

### Todo

- Mobile Support
- Animation for selection

### Credits

> Music

Created by Kade


> Assets

Created by YingYang


*Originally created for V.S Hex v3!*