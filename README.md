# Catacomb Vita Port

![Catacomb Screenshot](https://raw.githubusercontent.com/l0wigh/CatacombVita/master/catacomb.jpg)

Vita port of Catacomb, a Tetris clone. 

This port is based on the Catacomb SDL2 source code

# How to play

- Download and install the VPK.

- Buy the game [here](https://gog.com/game/catacombs_pack) and install it.

- Inside the install folder locate the ```Catacomb``` directory

- Copy the files from the folder inside ux0:/data/Catacomb or copy the folder direrctly inside ux0:/data (Use USB, more reliable honestly)

- Launch the game

# Controls and features

- DPAD : Mouvements
- X (space) : Heal
- O (lctrl) : Attack
- [] (F3) : Reset the game
- /\ (escape) : Quit the game
- Start (F9) : Pause
- Select (F1) : Help
- L1 (F4) : Save the game
- R1 (F5) : Load the game

Because of the limited buttons on the vita, I had to cut some features. The important ones are there. I don't think that I'll try to add anything else. The game should be playable and you should not encounter issues, if you do open a github issue

# Special Thanks

[sarcastic_cat](https://github.com/isage) : For all the help about Keybinding

All the CBPS community : For the help and the support





CatacombSDL
===========

CatacombSDL is a source port for The Catacomb (also known as Catacomb II). This
port compiles for Windows, OS X, and Linux for 32 and 64-bit X86. The only
dependency is SDL 2.0 and CMake. Supported compilers are GCC, Clang, and MSVC.

It is released under the GNU GPLv2. Please see COPYING for license details.

The source port is a drop in replacement for the DOS binary, and maintains full
compatibility with the DOS game files (demos, saves, and configuration). This
brings about a few limitations most obvious in control configuration. For
example, keyboard binds must correspond to a DOS scan code and joystick support
is limited to 2-axis and 2-buttons.

Also note on case sensitive file systems, this port currently requires that the
game data files (*.CA2) be in all upper case.
