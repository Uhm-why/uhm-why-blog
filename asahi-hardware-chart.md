# Asahi Linux Distribution Compatibility Table

Last Updated: November 2025

**Recent Changes:**
- November 2025: Fedora Asahi KDE confirmed working on M2 after community feedback
- See [investigation article]() for details on why initial testing showed different results

## M2 MacBook Pro Compatibility

| Distribution | Desktop Environment | GPU Rendering | TouchBar | Audio | WiFi | Bluetooth | Installation Difficulty | Overall Stability | Notes |
|--------------|---------------------|---------------|----------|-------|------|-----------|------------------------|-------------------|-------|
| **Arch Asahi ALARM** | KDE Plasma | ✅ Out of box | ✅ Out of box | ✅ | ✅ | ✅ | ⭐⭐ Easy | ⭐⭐⭐⭐⭐ Excellent | Hardware rendering and TouchBar work immediately after installing `asahi-base` package. |
| **Fedora Asahi Remix** | KDE Plasma | ✅ Out of box | ✅ Out of box | ✅ | ✅ | ✅ | ⭐⭐ Easy | ⭐⭐⭐⭐⭐ Excellent | **RECOMMENDED**: Flagship Distro. Hardware rendering and TouchBar work immediately. |
| **Ubuntu Asahi** | GNOME | ⚠️ Requires custom kernel | ❓ Not tested | ✅ | ✅ | ✅ | ⭐⭐⭐⭐⭐ Very Hard | ⭐⭐ Poor | GPU rendering only works after custom compiling latest kernel with Rust + apple_drm support. **All Snap apps have severe graphical bugs** (only lower-left quarter renders). |
| **Void Linux** | N/A | ❌ Never booted | ❌ Never booted | ❌ Never booted | ❌ Never booted | ❌ Never booted | ⭐⭐⭐⭐⭐ Very Hard | ❌ Failed | Installation completes but system won't boot past blinking cursor. Contradictory documentation for chroot install. |

## Legend

### Status Indicators
- ✅ **Works out of box** - No configuration needed
- ⚠️ **Requires manual configuration** - Works but needs extra steps
- ❌ **Does not work** - Feature unavailable or broken
- ❓ **Not tested** - No data available

### Installation Difficulty
- ⭐ **Very Easy** - Graphical installer, automated
- ⭐⭐ **Easy** - Simple CLI, clear documentation
- ⭐⭐⭐ **Moderate** - Some manual steps required
- ⭐⭐⭐⭐ **Hard** - Significant troubleshooting needed
- ⭐⭐⭐⭐⭐ **Very Hard** - Expert knowledge required

### Overall Stability
- ⭐⭐⭐⭐⭐ **Excellent** - Daily driver ready
- ⭐⭐⭐⭐ **Very Good** - Minor issues
- ⭐⭐⭐ **Good** - Usable with workarounds
- ⭐⭐ **Poor** - Significant problems
- ⭐ **Unusable** - Not production ready

## Detailed Configuration Notes

### Arch Asahi ALARM + KDE
**Tested:** November 2025  
**Kernel Version:**  6.17.7-1-3-ARCH
**Mesa Version:** 25.2.6

**Installation Steps:**
1. Run Arch Asahi ALARM install script
2. Choose KDE Install
3. Run system upgrade: `pacman -Syu`
4. Reboot - GPU acceleration and TouchBar work immediately

**Known Issues:**
- Aggressive kernel hardening (AppArmor + sysctl + boot params simultaneously) can brick the system
- Suggest testing hardening changes incrementally

### Fedora Asahi Remix + KDE
**Tested:** November 2025  
**Kernel Version:** 6.16.8-400.asahi.fc42.aarch64+16k
**Mesa Version:** 25.2.4 (Installed Automatically)

**Installation Steps:**
1. Run official Asahi install script from asahilinux.org
2. Choose Fedora Asahi Remix + KDE

**Known Issues:**
- None so far

### Fedora Asahi Remix + GNOME 

**Status**: Needs Update (as of November 2025)

I am happy with my current install and don't want to wipe it. If you are willing to test, please create a pull request after you update this section.

**Needs to be retested**

**Installation Steps:**
**Used the official Asahi Installer and select the option with GNOME**

**Known Issues:**
**Unknown:** **Needs to be retested**

### Ubuntu Asahi + GNOME
**Tested:** October 2025  
**Kernel Version:** 6.17
**Mesa Version:** 25.0.3

**Installation Steps:**
1. Install Ubuntu Asahi via install script
2. **All Snap applications will have graphical bugs at this stage**
3. Compile latest stable kernel with: `linux/scripts/config` enabling Rust + apple_drm
4. Install custom kernel
5. Reboot - GPU rendering now works

**Known Issues:**
- **CRITICAL**: Snap apps render only lower-left quarter of window
- Affects snap-store, making it nearly unusable
- PRs submitted to snapd and canonical app-center (pending)
- Based on older Debian kernel without upstream Asahi hardware support

### Void Linux
**Tested:** November 2025

**Installation Steps:**
1. Follow official Void Linux Apple Silicon documentation
2. Use chroot install method
3. Copy kernel from live image
4. Configure basic system

**Known Issues:**
- System never boots past blinking cursor
- Documentation has contradicting statements about partition structure
- Multiple install attempts failed identically

## Testing Methodology

All tests performed on:
- **Hardware:** MacBook Pro M2
- **RAM:** 8 GB
- **Storage:** 256 GB

Each distribution tested with:
1. Fresh install using official install scripts
2. System updates applied before testing
3. Default desktop environment (where applicable)
4. Standard use cases: web browsing, terminal work, development

## Contributing

Found different results? Please submit a PR with:
- Your hardware specs (M1/M2/M3, RAM, model)
- Kernel version
- Mesa version (for GPU testing)
- Desktop environment
- Date of testing
- Detailed steps to reproduce

## Additional Resources

- [Full blog post with detailed experience](https://uhmwhy.substack.com/p/asahi-linux-the-current-state)
- [Official Asahi Linux documentation](https://asahilinux.org)
- [Asahi Linux community support](https://asahilinux.org/community/)

## License

This compatibility data is licensed under the MIT License. See LICENSE file for details.
