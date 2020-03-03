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
In the file `/usr/share/X11/xkb/rules/evdev.xml` you have the rules/descriptions of all the different keybord layouts and the keymaps. Search for the following.
```
<configItem>
        <name>se</name>
        <shortDescription>sv</shortDescription>
        <description>Swedish</description>
        <languageList>
          <iso639Id>swe</iso639Id>
        </languageList>
      </configItem>
      <variantList>
```
On the line over the first variant, insert the following.
```
<variant>
  <configItem>
    <name>us</name>
    <description>Swedish (US, with Swedish letters)</description>
  </configItem>
</variant>
```

## Reload the keybord service
Reload the keybord service with `sudo service keyboard-setup restart`

## Select the layout in settings
Go to System settings &rarr;
