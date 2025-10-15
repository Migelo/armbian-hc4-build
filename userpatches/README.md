# User Patches

This directory contains custom patches and configurations that will be applied during the kernel build.

## Directory Structure

```
userpatches/
├── kernel/
│   └── meson64-current/         # Kernel patches for current branch
│       └── *.patch              # Your custom kernel patches
├── linux-meson64-current.config # Kernel configuration overrides
├── config-kernel.conf           # Kernel build configuration overrides
└── customize-image.sh           # Post-build customization script (for full images)
```

## Adding Kernel Patches

1. Place your `.patch` files in `userpatches/kernel/meson64-current/`
2. Patches are applied in alphabetical order
3. Use numeric prefixes for ordering: `0001-my-patch.patch`, `0002-another-patch.patch`

Example patch naming:
```
userpatches/kernel/meson64-current/
├── 0001-add-custom-driver.patch
├── 0002-enable-feature.patch
└── 0003-fix-something.patch
```

## Kernel Configuration Options

### Method 1: Kernel Config Fragment (Recommended)

Create or edit `userpatches/linux-meson64-current.config` to add/override specific kernel options:

```bash
# Example: Enable a specific feature
CONFIG_MY_FEATURE=y

# Example: Change default settings
CONFIG_ZRAM_DEF_COMP_ZSTD=y
CONFIG_ZRAM_DEF_COMP="zstd"
```

This file currently sets ZSTD as the default ZRAM compression algorithm.

### Method 2: Build Configuration

Create `userpatches/config-kernel.conf` to override kernel build settings:

```bash
# Enable verbose kernel build output
KERNEL_KEEP_CONFIG="yes"

# Customize kernel localversion
KERNELDIR="linux-mainline"
```

## Creating Patches

To create a kernel patch:

1. Build the kernel locally with `KERNEL_CONFIGURE=yes`
2. Make your changes in the kernel source
3. The build system will generate patches in `output/patch/`
4. Move patches to this directory

## More Information

See [Armbian Documentation](https://docs.armbian.com/Developer-Guide_Build-Preparation/) for detailed information on user patches.
