![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/dariogriffo/rgrc-debian/total)
![GitHub Downloads (all assets, latest release)](https://img.shields.io/github/downloads/dariogriffo/rgrc-debian/latest/total)
![GitHub Release](https://img.shields.io/github/v/release/dariogriffo/rgrc-debian)
![GitHub Release Date](https://img.shields.io/github/release-date/dariogriffo/rgrc-debian)

<h1>
   <p align="center">
     <a href="https://lazywalker.github.io/rgrc/"><img src="https://github.com/dariogriffo/rgrc-debian/blob/main/rgrc.svg" alt="rgrc Logo" width="128" style="margin-right: 20px"></a>
     <a href="https://www.debian.org/"><img src="https://github.com/dariogriffo/rgrc-debian/blob/main/debian-logo.png" alt="Debian Logo" width="104" style="margin-left: 20px"></a>
     <br>rgrc for Debian
   </p>
</h1>
<p align="center">
 rgrc, the Rusty Generic Colouriser: just like grc, but fast.
</p>

# rgrc for Debian

This repository contains build scripts to produce the _unofficial_ Debian packages
(.deb) for [rgrc](https://github.com/lazywalker/rgrc/) hosted at [deb.griffo.io](https://deb.griffo.io)

Currently supported Debian distros are:
- Bookworm (v12)
- Trixie (v13)
- Forky (v14)
- Sid (testing)

Currently supported Ubuntu distros are:
- Jammy (22.04)
- Noble (24.04)
- Questing (25.10)
- Resolute (26.04)

Supported architectures:
- amd64 (x86_64) - All distributions
- arm64 (aarch64) - All distributions
- armhf (ARM hard float) - All distributions
- i386 (x86 32-bit) - Debian only

Upstream publishes no armel or riscv64 binaries, so those architectures are
not available. All binaries are the statically linked (musl) upstream builds,
so the package has no dependencies.

The packages include:
- the `rgrc` binary
- the `rgrc(1)` man page
- `/etc/rgrc.conf` (the command to config mapping, kept as a conffile)
- the per-command configs in `/usr/share/rgrc/conf.*`
- shell completions for bash, fish and zsh

rgrc is not packaged by Debian or Ubuntu. It can be installed alongside
Debian's `grc` package; they share no files.

> ℹ️ Aliases are **not** enabled by default. To colorize commands like `ping`,
> `df` or `docker` automatically, add this to your `~/.bashrc` or `~/.zshrc`:
>
> ```sh
> eval "$(rgrc --aliases)"
> ```
>
> Or use it directly: `rgrc ping -c 4 debian.org`, `df -h | rgrc -c df`.

This is an unofficial community project to provide a package that's easy to
install on Debian. If you're looking for the rgrc source code, see
[rgrc](https://github.com/lazywalker/rgrc/).

## Install/Update

📖 **Step-by-step install guide:** [Debian](https://deb.griffo.io/install-latest-rgrc-in-debian.html) · [Ubuntu](https://deb.griffo.io/install-latest-rgrc-in-ubuntu.html)

### The Debian way

> ⚠️ **apt access requires a yearly subscription**
> ([deb.griffo.io](https://deb.griffo.io)). To use this tool for free, download
> the .deb from the [Releases](https://github.com/dariogriffo/rgrc-debian/releases) page
> and install it manually (see below).

```sh
sudo install -d -m 0755 /etc/apt/keyrings
curl -fsSL https://deb.griffo.io/EA0F721D231FDD3A0A17B9AC7808B4DD62C41256.asc | sudo gpg --dearmor --yes -o /etc/apt/keyrings/deb.griffo.io.gpg
echo "deb [signed-by=/etc/apt/keyrings/deb.griffo.io.gpg] https://deb.griffo.io/apt $(lsb_release -sc 2>/dev/null) main" | sudo tee /etc/apt/sources.list.d/deb.griffo.io.list
sudo apt update
sudo apt install -y rgrc
```

### Manual Installation

1. Download the .deb package for your Debian version available on
   the [Releases](https://github.com/dariogriffo/rgrc-debian/releases) page.
2. Install the downloaded .deb package.

```sh
sudo dpkg -i <filename>.deb
```
## Updating

To update to a new version, just follow any of the installation methods above. There's no need to uninstall the old version; it will be updated correctly.

## Building

### Build for single architecture
```sh
./build.sh <rgrc_version> <build_version> <architecture>
# Example: ./build.sh 0.6.35 1 arm64
```

### Build for all architectures
```sh
./build.sh <rgrc_version> <build_version> all
# Example: ./build.sh 0.6.35 1 all
```

## Roadmap

- [x] Produce a .deb package on GitHub Releases
- [x] Set up a debian mirror for easier updates
- [x] Multi-architecture support (amd64, arm64, armhf, i386)

## Disclaimer

- This repo is not open for issues related to rgrc. This repo is only for _unofficial_ Debian packaging.
