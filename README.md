<div align="center">

# 🌸 dotfiles

**A clean, minimal, and beautiful Hyprland setup on Arch Linux**

*Liquid glass waybar · Catppuccin Mocha · 144hz · Dual GPU optimized*

---

![Hyprland](https://img.shields.io/badge/Hyprland-0.54.3-blue?style=for-the-badge&logo=linux&logoColor=white)
![Arch Linux](https://img.shields.io/badge/Arch_Linux-1793D1?style=for-the-badge&logo=arch-linux&logoColor=white)
![Waybar](https://img.shields.io/badge/Waybar-Latest-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

</div>

---

## 📸 Preview

> *Add your screenshots here*

---

## 🖥️ System Info

| Component | Details |
|-----------|---------|
| **OS** | Arch Linux |
| **WM** | Hyprland 0.54.3 |
| **Bar** | Waybar (liquid glass) |
| **Launcher** | Rofi-wayland |
| **Terminal** | Kitty |
| **Shell** | Bash |
| **Theme** | Catppuccin Mocha |
| **Icons** | Papirus-Dark |
| **Font** | JetBrainsMono Nerd Font |
| **Wallpaper** | swww |
| **Display** | 1920x1080 @ 144hz |
| **GPU** | AMD Radeon (iGPU) + GTX 1650 |
| **Bootloader** | systemd-boot |

---

## ✨ Features

- 🪟 **Hyprland** — fluid animations with custom bezier curves, rounded corners, blur and transparency
- 🍫 **Catppuccin Mocha** — consistent color theme across everything
- 🔮 **Liquid Glass Waybar** — macOS Tahoe inspired floating pills with water-on-glass effect
- 🚀 **Rofi** — clean dark app launcher matching the theme
- 🖼️ **swww** — smooth wallpaper transitions
- 🔋 **Battery optimized** — charge limit, VRR disabled for stability
- 🎮 **Dual GPU** — AMD iGPU for compositor, GTX 1650 available via `prime-run`
- 📋 **Clipboard manager** — cliphist with rofi picker
- 🔔 **Dunst** — minimal notification daemon
- 🌐 **Dual boot** — Windows 11 + Arch via systemd-boot
- 💡 **144hz** — properly configured for smooth experience

---

## 📦 Dependencies

### Core
```bash
sudo pacman -S hyprland hyprpaper waybar rofi-wayland kitty
```

### System utilities
```bash
sudo pacman -S brightnessctl playerctl wl-clipboard cliphist
sudo pacman -S network-manager-applet blueman pavucontrol
sudo pacman -S dunst libnotify
```

### Fonts and themes
```bash
sudo pacman -S ttf-jetbrains-mono-nerd papirus-icon-theme nwg-look
```

### Optional but recommended
```bash
sudo pacman -S btop fastfetch swww lf
```

---

## 🚀 Installation

### 1. Clone the repo
```bash
git clone https://github.com/yourusername/dotfiles.git
cd dotfiles
```

### 2. Install dependencies
```bash
sudo pacman -S hyprland waybar rofi-wayland kitty brightnessctl \
  wl-clipboard cliphist network-manager-applet blueman pavucontrol \
  dunst ttf-jetbrains-mono-nerd papirus-icon-theme nwg-look swww btop
```

### 3. Copy configs
```bash
# Backup your existing configs first
cp -r ~/.config/hypr ~/.config/hypr.backup
cp -r ~/.config/waybar ~/.config/waybar.backup
cp -r ~/.config/rofi ~/.config/rofi.backup

# Copy new configs
cp -r config/hypr ~/.config/
cp -r config/waybar ~/.config/
cp -r config/rofi ~/.config/
cp -r config/kitty ~/.config/
cp -r config/dunst ~/.config/
```

### 4. Set wallpaper
```bash
swww-daemon &
swww img ~/Pictures/wallpaper.jpg
```

### 5. Reload Hyprland
```bash
hyprctl reload
```

---

## ⌨️ Keybindings

### General
| Keybind | Action |
|---------|--------|
| `Super + Return` | Open terminal (Kitty) |
| `Super + Space` | Open app launcher (Rofi) |
| `Super + Q` | Close window |
| `Super + E` | Open file manager |
| `Super + V` | Toggle floating |
| `Super + F` | Toggle fullscreen |
| `Super + L` | Lock screen |
| `Super + Shift + V` | Clipboard history |
| `Super + grave` | Show empty workspace |
| `Alt + Escape` | Switch to previous workspace |

### Window management
| Keybind | Action |
|---------|--------|
| `Super + Arrow keys` | Move focus |
| `Super + Shift + Arrow keys` | Move window |
| `Super + 1-9` | Switch workspace |
| `Super + Shift + 1-9` | Move window to workspace |

### Media & system
| Keybind | Action |
|---------|--------|
| `Fn + F7` | Brightness down |
| `Fn + F8` | Brightness up |
| `Fn + F10` | Mute audio |
| `Fn + F11` | Volume down |
| `Fn + F12` | Volume up |
| `Print` | Screenshot |

---

## 🎨 Customization

### Change wallpaper
```bash
swww img /path/to/wallpaper.jpg --transition-type fade
```

### Change theme colors
All colors follow **Catppuccin Mocha** palette. Main colors used:

| Color | Hex | Usage |
|-------|-----|-------|
| Mauve | `#cba6f7` | Active borders, accents |
| Blue | `#89b4fa` | Inactive borders, clock |
| Text | `#cdd6f4` | Main text |
| Base | `#1e1e2e` | Backgrounds |

### Change opacity/blur
Edit `~/.config/hypr/hyprland.conf` under `decoration`:
```ini
decoration {
    active_opacity = 0.85      # 0.0 invisible → 1.0 solid
    inactive_opacity = 0.65
    blur {
        size = 8
        passes = 2
    }
}
```

### Change animations speed
Edit bezier curves in `hyprland.conf`:
```ini
animation = workspaces, 1, 4, overshot, slide  # lower number = faster
```

---

## 🖥️ GPU Setup (Dual GPU laptops)

This setup forces AMD iGPU for Hyprland (better Wayland support) while keeping Nvidia for gaming:

```ini
# In hyprland.conf env section
env = WLR_DRM_DEVICES,/dev/dri/card0    # AMD iGPU
env = AQ_DRM_DEVICES,/dev/dri/card0
env = WLR_NO_HARDWARE_CURSORS,1
```

To run apps on Nvidia GPU:
```bash
prime-run game
prime-run steam
```

---

## 🔋 Battery Care

Charge limit set to 80% for longevity. To change:
```bash
# Check current limit
cat /sys/class/power_supply/BAT1/charge_control_end_threshold

# Change limit (survives reboot via udev rule)
echo 'SUBSYSTEM=="power_supply", KERNEL=="BAT1", ATTR{charge_control_end_threshold}="80"' | sudo tee /etc/udev/rules.d/battery.rules
sudo udevadm control --reload-rules && sudo udevadm trigger
```

---

## 🌐 Dual Boot (Windows 11 + Arch)

Using **systemd-boot**. Windows entry at `/boot/loader/entries/windows.conf`:
```
title   Windows 11
efi     /EFI/Microsoft/Boot/bootmgfw.efi
```

---

## 🔧 Troubleshooting

**Waybar not starting**
```bash
killall waybar && waybar 2>&1
```

**Brightness keys not working**
```bash
sudo pacman -S brightnessctl
# Check keybinds in hyprland.conf
```

**Screen flickering**
```bash
# Disable VRR if flickering on laptop display
hyprctl keyword misc:vrr 0
# Make permanent in hyprland.conf: vrr = 0
```

**Apps not launching**
```bash
# Check if package is installed
which appname
# Install if missing
sudo pacman -S appname
```

**After Hyprland update breaks config**
```bash
# Check what changed
hyprctl reload 2>&1
# Common fix: remove deprecated options that show as errors
```

---

## 📁 File Structure

```
dotfiles/
├── config/
│   ├── hypr/
│   │   └── hyprland.conf        # Main Hyprland config
│   ├── waybar/
│   │   ├── config.jsonc         # Waybar modules and layout
│   │   └── style.css            # Waybar liquid glass theme
│   ├── rofi/
│   │   └── config.rasi          # Rofi launcher theme
│   ├── kitty/
│   │   └── kitty.conf           # Terminal config
│   └── dunst/
│       └── dunstrc              # Notification config
└── README.md
```

---

## 💡 Tips

- Run `hyprctl reload` after every config change instead of restarting
- Back up your configs before updating Hyprland (`sudo pacman -Syu`)
- Use `btop` for system monitoring
- Use `lf` for terminal file management
- Check `https://wiki.hypr.land` for latest config syntax — it changes between versions
- Join r/hyprland and r/unixporn for inspiration

---

## 🙏 Credits

- [Hyprland](https://github.com/hyprwm/Hyprland) — the compositor
- [Catppuccin](https://github.com/catppuccin/catppuccin) — color scheme
- [Waybar](https://github.com/Alexays/Waybar) — status bar
- [r/unixporn](https://reddit.com/r/unixporn) — inspiration

---

<div align="center">

**Made with ❤️ on Arch Linux**

*If this helped you, consider giving it a ⭐*

</div>
