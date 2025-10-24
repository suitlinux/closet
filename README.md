# 🚪 Closet - Arch Linux Package Repository

Closet is a custom package repository for Arch-based Linux distributions, providing curated packages that complement the official Arch Linux repositories.

## 🌐 GitHub Pages

Visit our package repository at: [https://suitlinux.github.io/closet/](https://suitlinux.github.io/closet/)

## 📦 Adding the Repository

To use this repository, add the following to your `/etc/pacman.conf` file:

```ini
[closet]
Server = https://suitlinux.github.io/closet/$arch
SigLevel = Optional TrustAll
```

Then update your package database:

```bash
sudo pacman -Sy
```

## 🔧 Installing Packages

Once the repository is added, you can install packages using:

```bash
sudo pacman -S package-name
```

## 📋 Available Packages

The repository currently includes the following packages:

- **awesome-luajit** - Highly configurable framework window manager
- **colloid-gtk-theme-git** - Modern GTK theme
- **dragon-drop** - Simple drag-and-drop source/sink for X
- **filesystem** - Base filesystem
- **i3lock-color** - Improved screenlocker with color functionality
- **light** - Program to control backlight controllers
- **luajit-lgi** - Lua bindings to GObject libraries
- **udiskie-dmenu-git** - Dmenu integration for udiskie

## 🔨 Maintaining the Repository

To rebuild the repository database after adding new packages:

```bash
cd x86_64
./mkrepo closet
```

This will regenerate the `closet.db` and `closet.files` databases.

## 📚 Architecture

- **x86_64**: Main architecture supported

## 🤝 Contributing

To contribute packages to this repository:

1. Build your package following Arch Linux packaging guidelines
2. Add the `.pkg.tar.zst` file to the `x86_64` directory
3. Rebuild the repository database using the `mkrepo` script
4. Submit a pull request

## 📄 License

This repository contains packages with various licenses. Check individual package information for specific licensing details.

## 🔗 Links

- [GitHub Repository](https://github.com/suitlinux/closet)
- [Package Repository](https://suitlinux.github.io/closet/)
