# Armbian Kernel Builds for Odroid HC4

Automated kernel builds for the Odroid HC4 using the Armbian Build Framework.

## What This Does

This repository automatically builds Armbian kernels for the Odroid HC4 board using GitHub Actions. The built kernel packages (`.deb` files) are published as GitHub Releases.

## Supported Configurations

- **Board:** Odroid HC4 (meson-sm1/meson64 family)
- **Kernel Branches:**
  - `current` - Stable mainline kernel (default)
  - `edge` - Latest mainline kernel
  - `legacy` - Vendor/legacy kernel (if available)
- **Releases:**
  - `jammy` - Ubuntu 22.04 LTS (default)
  - `noble` - Ubuntu 24.04 LTS
  - `bookworm` - Debian 12
  - `trixie` - Debian 13

## How to Build

### Automatic Builds

- **Weekly:** Automatically builds every Monday at 2 AM UTC
- **On Push:** Builds when changes are pushed to main/master branch

### Manual Build

1. Go to the [Actions tab](../../actions)
2. Click "Build Armbian HC4 Kernel"
3. Click "Run workflow"
4. Select your preferred kernel branch and release
5. Click "Run workflow" to start the build

## Installation

1. Download the kernel `.deb` packages from the [Releases page](../../releases)
2. Install on your Odroid HC4:

```bash
# Transfer the files to your HC4
scp linux-*.deb user@odroidhc4:/tmp/

# SSH into your HC4
ssh user@odroidhc4

# Install the kernel packages
cd /tmp
sudo dpkg -i linux-image-*.deb
sudo dpkg -i linux-headers-*.deb
sudo dpkg -i linux-dtb-*.deb

# Update initramfs
sudo update-initramfs -u -k all

# Reboot to use the new kernel
sudo reboot
```

## Built Packages

Each build produces the following packages:

- `linux-image-*` - Kernel image
- `linux-headers-*` - Kernel headers for building modules
- `linux-dtb-*` - Device tree binaries
- `linux-libc-dev-*` - Kernel headers for userspace development

## Customization

To customize the build:

1. Fork this repository
2. Add custom patches in `userpatches/kernel/meson64-current/`
3. Modify kernel config in `userpatches/config-kernel.conf`
4. Commit and push - the workflow will run automatically

## Advanced Configuration

Edit `.github/workflows/build-kernel.yml` to:

- Change build frequency (modify `schedule:` section)
- Add custom extensions (`armbian_extensions:` parameter)
- Modify compression format (`armbian_compress:` parameter)
- Add custom build parameters

## Links

- [Armbian Build Framework](https://github.com/armbian/build)
- [Odroid HC4 Documentation](https://docs.armbian.com/User-Guide_Getting-Started/)
- [Armbian Forum](https://forum.armbian.com/)

## License

This repository uses the Armbian Build Framework, which is licensed under GPL-2.0.
