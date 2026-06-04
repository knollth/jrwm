# jrwm - A Junior Window Manager

_(Alternatively, jpco's river window manager)_

jrwm is a tiling window manager written against [the river Wayland
compositor](https://isaacfreund.com/software/river/).

It is a tiling WM, with a layout inspired by that of dwm.  The implementation is
based on that of tinyrwm, although jrwm seems to be, surprisingly, slightly more
fastidiously protocol-rule-following than tinyrwm itself.


## Configuration

jrwm comprises a single file, `jrwm.c`, which can be edited.  A real method for
configuration, likely via an IPC mechanism, is a TODO.


## Building and installation

jrwm only requires a C99-capable compiler, GNU `make`, and wayland-scanner to
build.  (And GNU `make` can be replaced with an alternative with some very
simple changes to the makefile.  `make install` will (by default) install jrwm
to `/usr/local/bin`.

Of course, to run, jrwm requires river to be running.


## TODO

jrwm is still in active development.  Desired additions include:

-   Better multi-Space support: more Spaces, better Space/Output assignment,
    dynamic/configurable Spaces
-   Dialog-style windows
-   Optional focus-follows-pointer and pointer-follows-focus behavior
-   Actual configuration, probably via IPC
-   Additional minor, nice behaviors: output scaling, libinput config,
    background color

In addition, the WM is very untested, and probably somewhat broken, with
multiple outputs.
