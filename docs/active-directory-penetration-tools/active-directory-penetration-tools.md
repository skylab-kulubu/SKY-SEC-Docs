---
sidebar_label: 'Intro'
sidebar_position: 1
---

# Active Directory Penetration Tools

This repository is a rewritten version of the existing Active Directory penetration testing tools, using lower-level and more stable versions.

## Building From Source

### Ubuntu/Debian

#### Dependecies

```bash
sudo apt update -y
sudo apt install -y \
  build-essential \
  cmake \
  libssl-dev \
  pkg-config \
  libboost-all-dev
```

#### Building

```bash
cd $ROOT 
scripts/build.sh
```

### Nix-Shell

```bash
cd path/to/Active-Directory-Penetration-Tools
```

```bash
nix-shell 
buildproj
```

or

```bash
nix-shell --command "buildproj"
```

## Publishing Release

### From CLI

#### Dependecies

You have to build it from source

```bash
sudo apt install gh jq -y
```

```bash
scripts/release.sh
```
