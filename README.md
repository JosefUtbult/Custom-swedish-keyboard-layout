# Custom swedish keyboard layout
This is a tutorial on how to add a custom swedish keymap layout to Linux. It uses the standard american keyboard layout but with six additional characters.
| Character     | Key combination     |
| ------------- |:-------------------:|
| å             | Alt Gr + [          |
| Å             | Alt Gr + Shift + [  |
| ö             | Alt Gr + ;          |
| Ö             | Alt Gr + Shift + ;  |
| ä             | Alt Gr + '          |
| Ä             | Alt Gr + Shift + '  |

# Setup
## Add Variant
The file containing the link between the keys and the character they should display is `/usr/share/X11/xkb/symbols/se`. Add the following to the end of the file.
```
partial alphanumeric_keys
xkb_symbols "us" {
    include "us"

    name[Group1]="Swedish (US, with Swedish letters)";

    key <AC10> { [ NoSymbol, NoSymbol, odiaeresis, Odiaeresis ] };
    key <AC11> { [ NoSymbol, NoSymbol, adiaeresis, Adiaeresis ] };
    key <AD11> { [ NoSymbol, NoSymbol, aring, Aring ] };

    include "level3(ralt_switch)"
};
```
## Add the variant to rules
In the file `/usr/share/X11/xkb/rules/evdev.xml` you have the rules/descriptions of all the different keyboard layouts and the keymaps. Search for `<name>se</name>` and insert the following after `<variantList>`
```
<variant>
  <configItem>
    <name>us</name>
    <description>Swedish (US, with Swedish letters)</description>
  </configItem>
</variant>
```

## Reload the keyboard service - Ubuntu
Reload the keyboard service with `sudo service keyboard-setup restart`

## Select the layout in settings - Ubuntu
Go to System settings &rarr; Keyboard &rarr; Layouts (At least in Linux mint, but it shouldnt be inpossible to find it in another distro). There, add a layout and search for `Swedish (US, with Swedish letters)`.

## Select the layout - Arch
Run the following command to try the keymap out.
```setxkbmap se -variant us```

## Set persistant keymap - Arch
In ``/etc/X11/xorg.conf.d`` there should be a .conf file to setup input stuff. Add the following in the bottom of that.
```
Section "InputClass"
    Identifier "system-keyboard"
    MatchIsKeyboard "on"
    Option "XkbLayout" "se"
    Option "XkbVariant" "us"
EndSection
```

# Prologue
There you go! Hope this helps someone that has some trouble with their swedish letters. It will at least help me the next time I'll have to do it.
