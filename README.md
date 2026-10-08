# dwm setup

My minimal [suckless](https://suckless.org) desktop on Gentoo: **dwm**, **dmenu**, **st** and **slstatus**, all themed with one soft mauve/gray light palette and set in JetBrains Mono.

<!-- Add a screenshot: -->
<!-- ![screenshot](screenshot.png) -->

## Contents

| Component | Purpose | Config |
|-----------|---------|--------|
| [dwm](https://dwm.suckless.org) | Window manager | `dwm/config.h` |
| [dmenu](https://tools.suckless.org/dmenu) | Application launcher | `dmenu/config.h` |
| [st](https://st.suckless.org) | Terminal emulator | `st/config.h` |
| [slstatus](https://tools.suckless.org/slstatus) | Status bar text | `slstatus/config.h` |

## Theme

Font everywhere: **JetBrains Mono** (size 10 in dwm and the bar, pixelsize 14 in st).

### dwm / dmenu

| Name | Hex | Used for |
|------|-----|----------|
| `col_gray1` | `#e8e1e3` | Bar background |
| `col_gray2` | `#d4c6cb` | Normal window border |
| `col_gray3` | `#171217` | Bar text |
| `col_gray4` | `#0b080b` | Selected text |
| `col_cyan` | `#8a6f7a` | Selected tag / accent |
| (border) | `#5c4650` | Focused window border |

### st

| Color | Normal | Bright |
|-------|--------|--------|
| 0 black | `#2b2228` | `#7a6d74` |
| 1 red | `#a8324a` | `#c4304f` |
| 2 green | `#3f7a4a` | `#2f8f4e` |
| 3 yellow | `#8a6a1c` | `#9a6f00` |
| 4 blue | `#3b5ba5` | `#3e64c8` |
| 5 magenta | `#8c4f7c` | `#b0479f` |
| 6 cyan | `#2a7a80` | `#1c8f98` |
| 7 white | `#6f636a` | `#1c1519` |

Default foreground `#2b2228`, background `#e4dde1`, cursor `#6d3f5e`.

## Installation

### Dependencies (Gentoo)

```sh
emerge --ask x11-base/xorg-server x11-libs/libX11 x11-libs/libXft \
    x11-libs/libXinerama media-libs/fontconfig media-fonts/jetbrains-mono
```

Package names may differ slightly depending on your profile and USE flags.

### Build and install

```sh
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

for d in dwm dmenu st slstatus; do
    (cd "$d" && sudo make clean install)
done
```

### Start

Add this to `~/.xinitrc` and run `startx`:

```sh
slstatus &
exec dwm
```

## Key bindings

**Mod = Super (Mod4)**

### dwm

| Keys | Action |
|------|--------|
| `Mod + p` | Launch dmenu |
| `Mod + Shift + Return` | Open terminal (st) |
| `Mod + b` | Toggle bar |
| `Mod + j` / `k` | Focus next / previous window |
| `Mod + i` / `d` | Increase / decrease master windows |
| `Mod + h` / `l` | Shrink / grow master area |
| `Mod + Return` | Swap focused window with master |
| `Mod + Tab` | Switch to previous tag |
| `Mod + Shift + c` | Close window |
| `Mod + t` | Tiled layout `[]=` |
| `Mod + f` | Floating layout `><>` |
| `Mod + m` | Monocle layout `[M]` |
| `Mod + Space` | Toggle between last two layouts |
| `Mod + Shift + Space` | Toggle floating for window |
| `Mod + 1-9` | View tag |
| `Mod + Ctrl + 1-9` | Toggle tag in view |
| `Mod + Shift + 1-9` | Move window to tag |
| `Mod + Ctrl + Shift + 1-9` | Toggle tag on window |
| `Mod + 0` | View all tags |
| `Mod + Shift + 0` | Show window on all tags |
| `Mod + ,` / `.` | Focus previous / next monitor |
| `Mod + Shift + ,` / `.` | Send window to previous / next monitor |
| `Mod + Shift + q` | Quit dwm |

### Mouse (dwm)

| Action | Result |
|--------|--------|
| `Mod + Left drag` | Move window |
| `Mod + Middle click` | Toggle floating |
| `Mod + Right drag` | Resize window |
| Click tag | View tag |
| Right click tag | Toggle tag in view |
| Click layout symbol | Cycle layout |
| Right click layout symbol | Monocle |

### st

**Mod = Alt**, **TERMMOD = Ctrl + Shift**

| Keys | Action |
|------|--------|
| `Ctrl + Shift + c` | Copy |
| `Ctrl + Shift + v` | Paste |
| `Ctrl + Shift + y` / `Shift + Insert` | Paste selection |
| `Ctrl + Shift + PgUp` / `PgDn` | Zoom in / out |
| `Ctrl + Shift + Home` | Reset zoom |
| `Alt + drag` | Rectangular selection |

## Configuration notes

### dwm
- Top bar, 1 px borders, snap distance 32 px.
- Master area factor `0.55`, 1 master window, size hints respected in tiled mode.
- Fullscreen focus lock on, refresh rate 120.
- Window rules: GIMP always floats, Firefox opens on tag 9.
- dmenu is launched with the same font and colors as the bar.

### st
- `TERM=st-256color`, block cursor, bell disabled.
- 2 px border, 8 spaces per tab.
- Draw latency between 2 ms and 33 ms.
- Insecure window operations (`allowwindowops`) disabled.

### slstatus
- Updates every 1000 ms.
- Currently shows only the date and time (`%F %T`, e.g. `2026-10-08 14:47:30`).
- Edit the `args[]` array in `slstatus/config.h` to add battery, CPU, RAM, volume, Wi-Fi and more.

### dmenu
- Appears at the top, uses `monospace:size=10` by default.
- dwm passes `-fn` on launch, so the dwm font setting takes precedence.

## Customizing

Every tool is configured by editing its `config.h` and rebuilding:

```sh
cd <tool>
sudo make clean install
```

Restart dwm (or log out and back in) to apply changes to dwm and slstatus.

## License

The suckless tools are released under the MIT/X license. See the `LICENSE` file in each directory. My configuration files in this repo are released under the same terms.
