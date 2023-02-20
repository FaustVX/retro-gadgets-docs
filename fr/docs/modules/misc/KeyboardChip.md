# KeyboardChip

<img src="https://docs.retrogadgets.game/api/modules/KeyboardChip.png" width="200" align="right">

The KeyboardChip is used to get input from a connected keyboard. When connected to something that is interactable, it can allow the component to be controlled via the keyboard.

**_❔ This component is still in the process of being elaborated on._**

## Methods

<!-- TODO: Explain these methods. -->
### GetButton(name `InputName`) `InputSource`

### GetButtonAxis(name `InputName`) `InputSource`

## Event - `KeyboardChipEvent`
The event emitted as part of the [CPU](./CPU.md) event system.

Sent when a key is pressed or released.

### ButtonDown `boolean`
True when a button is down
### ButtonUp `boolean`
True when a button gets releaed
### InputName `InputName`
Name of the key being pressed/released

## Input Names **[Read only]**
Input names can be accessed by `KeyboardChip.`nameOfInput, and are listed below.
- `Return`
- `Space`
- `LeftArrow`
- `RightArrow`
- `DownArrow`
- `UpArrow`
- `Backspace`
- `Escape`
- `Tab`
- `Clear`
- `Pause`
- `Exclaim`
- `DoubleQuote`
- `Hash`
- `Dollar`
- `Percent`
- `Ampersand`
- `Quote`
- `LeftParen`
- `RightParen`
- `Asterisk`
- `Plus`
- `Comma`
- `Minus`
- `Period`
- `Slash`
- `Alpha0`
- `Alpha1`
- `Alpha2`
- `Alpha3`
- `Alpha4`
- `Alpha5`
- `Alpha6`
- `Alpha7`
- `Alpha8`
- `Alpha9`
- `Colon`
- `Semicolon`
- `Less`
- `Equals`
- `Greater`
- `Question`
- `At`
- `LeftBracket`
- `Backslash`
- `RightBracket`
- `Caret`
- `Underscore`
- `BackQuote`
- `A`
- `B`
- `C`
- `D`
- `E`
- `F`
- `G`
- `H`
- `I`
- `J`
- `K`
- `L`
- `M`
- `N`
- `O`
- `P`
- `Q`
- `R`
- `S`
- `T`
- `U`
- `V`
- `W`
- `X`
- `Y`
- `Z`
- `LeftCurlyBracket`
- `Pipe`
- `RightCurlyBracket`
- `Tilde`
- `Delete`
- `Keypad0`
- `Keypad1`
- `Keypad2`
- `Keypad3`
- `Keypad4`
- `Keypad5`
- `Keypad6`
- `Keypad7`
- `Keypad8`
- `Keypad9`
- `KeypadPeriod`
- `KeypadDivide`
- `KeypadMultiply`
- `KeypadMinus`
- `KeypadPlus`
- `KeypadEnter`
- `KeypadEquals`
- `Insert`
- `Home`
- `End`
- `PageUp`
- `PageDown`
- `F1`
- `F2`
- `F3`
- `F4`
- `F5`
- `F6`
- `F7`
- `F8`
- `F9`
- `F10`
- `F11`
- `F12`
- `F13`
- `F14`
- `F15`
- `Numlock`
- `CapsLock`
- `ScrollLock`
- `RightShift`
- `LeftShift`
- `RightControl`
- `LeftControl`
- `RightAlt`
- `LeftAlt`
- `RightCommand`
- `LeftCommand`
- `AltGr`
- `Help`
- `Print`
- `SysReq`
- `Break`
- `Menu`

## Remarks

### How to use the event
The keyboard chip takes advantage of [CPU](.CPU.md) events, which can be hard to wrap your head around at first. The following is a brief tutorial on how to log the name of the key that's currently being pressed or released.

First, place a keyboard chip and a CPU on your gadget and select the CPU with the Multitool:

![Selecting the CPU](./../../../assets/docs/KeyboardChip/SelectingCPU.png)

Then, select `EventChannels` and set the first channel to the keyboard chip.

![Setting the event channel](../../../assets/docs/KeyboardChip/EventChannel.png)

Now go into your CPU's code and add the following function:

```lua
function eventChannel1(sender:KeyboardChip, arg:KeyboardChipEvent)
end
```
Remember that it **must** be global! Prepending the `local` keyword will prevent the CPU from recognizing it. Adding this kind of function will cause the CPU to automatically run it whenever the user presses or released a key.

Now, insert code inside of the function to print whether a key is being pressed or no longer being pressed:

```lua
if arg.ButtonDown then
    log(tostring(arg.InputName) .. " is pressed")
elseif arg.ButtonUp then
    log(tostring(arg.InputName) .. " is not pressed anymore")
end
```

![Multitool output](./../../../assets/docs/KeyboardChip/output.png)

### Multitool configuration

Sometimes, components can be given direct control from the keyboard chip without having to specify the intricacies in code.

<img src="../../../assets/docs/KeyboardChip/KeyboardInput.png">

By using the Multitool, you can provide components such as Sticks with an InputSourceX and an InputSourceY that will control how a keyboard button manipulates the axes it moves upon. When selecting a _NEGATIVE_ and _POSITIVE_ input, NEGATIVE should be the one that moves the stick down or left; in a negative direction, basically. POSITIVE is the opposite. By mapping S to NEGATIVE and W to POSITIVE, we can move the stick up and down with the W (up) and S (down) keys. This method is an abstraction of the manual technique used in code via the KeyboardChip's own methods, and is usually much easier and faster. However, it may not provide the extensibility you need, may be too limited, or may not apply to an object. In that case, manually doing it in a Lua file is the better option.
