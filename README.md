# Geet's build of st - the simple (suckless) terminal

The [suckless terminal (st)](https://st.suckless.org/) with some additional features that make it literally the best terminal emulator ever

## Unique features (using [rofi](https://github.com/davatorium/rofi/))

- **copy urls** in the same way with `Alt-l` or `Ctrl-Shift-l`
- **copy the output of commands** with `Alt-o` or `Ctrl-Shift-o`

> :warning: **You will require some themes from my [`Dotfiles`](https://github.com/sethigeet/Dotfiles/) if you want the same exact look in rofi!**

## Bindings for

- **Scrolling**:
  - For the **normal person**:
    - With the Keyboard:
      - line by line: scroll up and down with `Alt-↑/↓`
      - page by page: scroll up and down with `Alt-Page Up/Down`
    - With the mouse:
      - line by line: scroll with mouse
      - page by page: scroll with mouse while holding shift
  - For the **vim freaks**:
    - With the Keyboard:
      - line by line: scroll up and down with `Alt-k/j`
      - page by page: scroll up and down with `Alt-u/d`
    - With the mouse:
      - You don't need the mouse!
- **Zoom or Change Font Size**:
  - For the **normal person**:
    - With the Keyboard:
      - By 1 level: zoom in and out with `Alt-Shift-↑/↓`
      - By 2 levels: zoom in and out with `Alt-Shift-Page Up/Down`
  - For the **vim freaks**:
    - With the Keyboard:
      - By 1 level: zoom in and out with `Alt-Shift-k/j`
      - By 2 levels: zoom in and out with `Alt-Shift-u/d`
- **Copy and Paste**:
  - Copy with `Alt-c` or `Ctrl-Shift-c`
  - Paste with `Alt-v` or `Ctrl-Shift-v` or `Shift-Insert`

## Colors and UI

You can set your custom colors, fonts, transparency and padding(`borderpx`) in the `Xresources` file like so -

```
*.font:	monospace:pixelsize=15:antialias=true:autohint=true;
*.alpha: 0.95
*.borderpx: 2
*.color0: #111
*.color1: #111
...
*.color15: #111
...
```

> :warning: **If you are setting your custom colors in the `Xresources` file**: Make sure you set at least 16 (ie. 0 to 15) colors. You may set more colors if you like!

> :art: **If you want you can also set a fall back font in the `Xresources` file like so**:

```
...
*.font2: Noto Color Emoji:pixelsize=12:antialias=true:autohint=true;
...
```

**Defaults**:

- Default font is the system `monospace at 15pt`, meaning the font will match your system font. (This `monospace` font is specified in the `fonts.conf` file on you system which is usually located at `~/.config/fontconfig/fonts.conf`)
- Default alpha is `0.95 (ie. 95%)` opaque.
- Default colors which are used are from the [`Ayu Mirage`](https://github.com/ayu-theme/ayu-colors) color scheme

The `alpha` value (for transparency) goes from `0` (transparent) to `1` (opaque).

## List of all Patches Applied

- `alpha`: get a transparent background
- `bold-is-not-bright`: draw bold text with normal colors (not bright)
- `boxdraw-v2`: draw some special unicode characters more nicely
- `clipboard`: fix the clipboard issue with st
- `desktopentry`: create a desktop entry for st on installation (when `sudo make install` is run)
- `externalpipe`: pipe all the content of st to an external script (there are two such scripts in the `scripts` folder)
- `font2`: specify multiple fonts as fall back
- `ligatures`: display some cool ligatures(this will work only if your font supports it)
- `newterm`: create a new instance of st in the same working directory
- `scrollback`: scroll back in the history of st
- `vertcenter`: vertically center some text so that all the text is in place
- `vimBrowse`: move around st using `vim` bindings
- `workingdir`: specify the working directory while running st using the `d` flag
- `xresources`: specify some settings in the `Xresources`

## Installation

You should have `xlib` header files and `libharfbuzz` build files installed.

```
git clone https://github.com/sethigeet/st
cd st
sudo make install
```

**_Note_**: Obviously, `make` is required to build. `fontconfig` is required for the default build, since it asks `fontconfig` for your system `monospace` font. It might be obvious, but `libX11` and `libXft` are required as well. Chances are you have all of this installed already.

On `OpenBSD`, be sure to edit `config.mk` first and remove `-lrt` from the
`$LIBS` in the `Makefile` before compiling.

Be sure to have a compositor (`xcompmgr`, `picom`, etc.) running if you want transparency. (If you are running a desktop environment you must be running some compositor)

## Notes on Emojis and Special Characters

If st crashes when viewing emojis, install [`libxft-bgra`](https://aur.archlinux.org/packages/libxft-bgra/) from the `AUR`.

Note that some special characters may appear truncated if too wide. You might want to manually set your prefered emoji/special character font to a lower size in the `config.h` file to avoid this. By default, `Noto Color Emoji`, `JoyPixels` and `Symbola` are used at a smaller size than the usual text.
