# Hak_05-
Rubber Ducky USB 
README.md
About
A toolchain to turn a Digistump Digispark device into a cheap USB Rubber Ducky knock-off with a minimum amount of fuss. This wouldn't have been possible without the following projects:

The official USB Rubber Ducky encoder defining the Duckyscript language: https://github.com/hak5darren/USB-Rubber-Ducky (unknown license)
The duck2spark converter showing how the encoded payload translates to equivalent C++ code: https://github.com/mame82/duck2spark (unknown license)
Various Digispark projects written in C using Makefiles: https://github.com/yuvadm/digispark-projects (GPL3)
A mapping of Linux key names to USB codes: https://gist.github.com/MightyPork/6da26e382a7ad91b5496ee55fdc73db2 (Public Domain)
The V-USB library: https://www.obdev.at/products/vusb/index.html (GPL2/3)
Digistump's Arduino libraries: https://github.com/digistump/DigistumpArduino (unknown license)
Installation
Run chicken-install inside the project directory.

Workflow
Run the following inside the project directory:

plucky -i example.duck -l de -o keyboard.c
make
make deploy
Supported language
Duckyscript is a language resembling BASIC. Every line contains an all-caps command followed by arguments. The following commands are supported:

REM <comment> / // <comment>: Ignore the rest of the line.
DEFAULT_DELAY <number>: Set the default delay between execution of commands, measured in milliseconds. This is mostly useful for debugging.
DELAY <number>: Wait for the specified amount of milliseconds.
STRING <text>: Type the specified text, using modifiers when needed. Note that this depends on a correctly set keyboard layout.
STRING_DELAY <number> <text>: Like the STRING command, but waiting the specified delay in milliseconds between each letter.
REPEAT <number>: Repeat the previous non-repeat command the specified number of times.
<modifier>... <key>: Type the specified shortcut by pressing the key while holding the specified modifiers. Modifiers are all-caps and may contain underscores and numbers. Keys may be all-caps (like SPACE), but also be a number or letter.
<key>: Types the key, specified by its all-caps name which may contain underscores and numbers. Use STRING for other keys.
For compatibility with existing Duckyscript payloads, the following behavior is supported:

DEFAULTDELAY is considered an alias for the DEFAULT_DELAY command.
Certain shortcuts may use dashes instead of a space as separator:
CTRL-ALT
CTRL-SHIFT
ALT-SHIFT
ALT-TAB
COMMAND-OPTION
Keyboard layouts
Not everyone is using an US layout on their keyboard. To make sure the correct keys are typed, you can pick an alternative keyboard layout. The -l argument allows you to specify the name of a built-in layout or path to a layout file. Use --list-layouts to print a list of built-in layouts or check the duckyscript/sparkling/layouts directory.

The format is a list of S-Expressions, with each S-Expression describing how a character maps to a sequence of shortcuts. Each shortcut can either consist of a symbol (representing a key without modifier) or a list of symbols (representing a key with modifiers). This structure allows typing characters by using dead keys and more.

Incompatibilities and other deficiencies
Currently only German and American keyboard layouts are supported.
The interaction between the DEFAULT_DELAY and DELAY command is still unclear to me and most likely incorrect.
Handling of the REPEAT command is most likely different from the original.
Shortcuts only support pressing a regular key with optional modifiers whereas the original supports modifier-only shortcuts as well.
More can be found on the bug tracker in due time.
