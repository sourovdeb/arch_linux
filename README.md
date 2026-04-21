# 🐧 Arch Linux Automated Setup (Aeon Writer OS)

**A comprehensive automation suite for setting up Arch Linux/EndeavourOS optimized for heavy writing workloads and neurodivergent accessibility.**

## 🎯 Project Overview

This repository contains complete automation for:
- **Aeon Writer OS**: A personalized Linux environment designed for writing 100+ pages daily
- **Podcast Production Setup**: Audio tools and recording environment
- **Accessibility Features**: ADHD/neurodivergent-friendly customizations
- **VirtualBox Integration**: Pre-configured VMs for safe testing

## 📁 Repository Structure

```
├── automate_arch_setup.sh    # Main automation script
├── packages.txt              # Complete package list
├── partition_ssd.sh          # SSD partitioning automation  
├── post_install.sh           # Post-installation configuration
├── ArchOS.vdi               # VirtualBox disk image
├── ArchSSD.vmdk             # Physical SSD access VM
└── virtualbox/              # VM configurations
```

## 🚀 Quick Start

### Method 1: Physical SSD Boot (Recommended)
```bash
# Boot from external SSD with EndeavourOS
# Connect via SSH from Windows
./automate_arch_setup.sh
```

### Method 2: VirtualBox Testing
```bash
# Import ArchOS.vdi or ArchSSD.vmdk
# Run automation scripts in VM environment
```

## 🛡️ Safety Features

- **NVIDIA Optimus Support**: Automatic nomodeset configuration
- **Hardware Detection**: Intel i5-12450H + RTX 3050 optimized
- **Network Drivers**: MediaTek MT7922 WiFi support
- **Rollback Capability**: All changes reversible

## 📝 Target Use Case

Optimized for:
- ✍️ **Heavy Writing**: 100+ pages daily with LaTeX/Markdown
- 🎙️ **Podcast Production**: Audio recording and editing
- 🧠 **Neurodivergent Accessibility**: ADHD-friendly interface
- 🔧 **Development Work**: Programming and automation tools

## ⚡ Hardware Requirements

- **CPU**: Intel i5-12450H (or compatible)
- **GPU**: NVIDIA RTX 3050 (Optimus configuration)
- **Storage**: 512GB+ SSD (external preferred)
- **Network**: MediaTek MT7922 WiFi or Ethernet

## 📞 Support

This is a personal automation project for specific hardware. Adapt scripts for your system configuration.

---
**🎯 Goal**: Transform any compatible laptop into "Aeon Writer OS" - the ultimate writing and podcast production environment.

### Windows
1. **Rufus** for USB creation
2. **External SSD** (fresh, no data)
3. **Spare USB drive** (2GB+)

### System Requirements
- UEFI firmware with Secure Boot **disabled**
- Boot order set to USB first
- Internet connection for package downloads

## 📝 Installation Phases

1. **Phase 1**: Download Arch Linux ISO
2. **Phase 2**: Create bootable USB (Rufus/`dd`)
3. **Phase 3**: Boot into Arch Linux live environment
4. **Phase 4**: Automated SSD partitioning & base install (`automate_arch_setup.sh`)
5. **Phase 5**: Post-installation setup (`post_install.sh` runs automatically)
6. **Phase 6**: First login — change password, pull Ollama model

## 🛠️ Configuration

The setup configures:

- **Bootloader**: systemd-boot for UEFI
- **Desktop**: Xfce (lightweight and accessible) + i3 available
- **Shell**: bash with sensible defaults
- **User**: `sourov` (change in the script if needed)
- **Timezone**: Asia/Dhaka
- **Services**: Ollama AI service, NetworkManager, PipeWire audio

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## 📄 License

MIT License — see the root LICENSE file for details.

## 🙏 Acknowledgments

- Arch Linux community and the [ArchWiki](https://wiki.archlinux.org/)
- All open-source tool developers included in this setup

---

**Note**: This setup is designed for writers with ADHD/autism but works for anyone wanting a portable, reproducible Arch Linux environment with writing tools.
