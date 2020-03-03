# Custom swedish keyboard layout
This is a tutorial on how to add a custom swedish keyboard layout to Linux. It uses the standard american keyboard layout but with six additional characters.
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
