This guide will describe how mods and their triggers attach to FullScreenShenanigans projects.

# ModAttachr

ModAttachr is a module that allows for extensible triggered mod events.

A mod is a custom modification that changes how the game normally runs and/or how the player interacts with the game.
Each mod can define any number of events, keyed by string, to call when they are fired.
When an event is fired in the game, ModAttachr calls the corresponding events of all enabled mods that have a defined event under that name.

## Adding Mods

A mod can be added with `addMod`.

```javascript
modAttacher.addMod({
    name: "Infinite Health",
    events: {
        "onModEnable": () => {
            // event code when the mod is enabled
        },
        "onModDisable": () => {
            // event code when the mod is disabled
        },
        "onBattleStart": () => {
            // event code when a battle starts
        }
    },
    enabled: false
});
```

## Event Hooks

When a mod is enabled, its `onModEnable` event is called; when a mod is disabled, its `onModDisable` event is called.
A mod can be toggled with `toggleMod`.

```javascript
// Enables, disables, and toggles the mod.
modAttacher.enableMod("Infinite Health");
modAttacher.disableMod("Infinite Health");
modAttacher.toggleMod("Infinite Health");
```

To fire events use the module's `fireEvent` function.

```javascript
// Fires the onBattleStart event for all mods.
modAttacher.fireEvent("onBattleStart");
```

To fire an event for one mod, use `fireModEvent`.

```javascript
modAttacher.fireModEvent("onBattleStart", "Infinite Health");

// Passing in additional arguments.
const opponent = new Opponent();
modAttacher.fireModEvent("onBattleStart", "Infinite Health", opponent);
```

More can be read about ModAttachr on its [Readme](https://github.com/FullScreenShenanigans/ModAttachr/blob/master/README.md).
