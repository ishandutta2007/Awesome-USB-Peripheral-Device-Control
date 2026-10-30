# Awesome-USB-Peripheral-Device-Control

# Top USB & Peripheral Device Control Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Endpoint Port Control, Removable Media Encryption & Self-Hosted USB Authorization*  
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **USB & Peripheral Device Control**. These tools enable organizations to enforce policies over which USB devices, removable media, and peripheral ports can connect to endpoints—preventing data exfiltration, blocking malware vectors, and maintaining compliance without completely locking down user productivity.

**Examples** include CrowdStrike Falcon Device Control, CoSoSys Endpoint Protector, Symantec Device Control, McAfee Device Control, DriveLock, Sophos Device Control, Ivanti Device Control, ManageEngine Device Control Plus, Microsoft Intune Device Control, and Safend (the category leaders).

**Open-source emphasis**: USB & Peripheral Device Control is a domain where open-source tooling is **remarkably thin and narrowly focused**. The standout project is **USBGuard**, a Linux-only USB device authorization framework that implements allowlisting (default-deny) policies—the closest open-source equivalent to commercial endpoint device control . **usb-helper** provides Python-based device monitoring and profile-based filtering, useful for building custom authorization scripts . **usb-remote** enables USB-over-network sharing, a different use case entirely . **Fleet** (PostHog) offers cross-platform device management with MDM capabilities, but it is a full endpoint management platform rather than a dedicated USB control tool . The critical gap: **no open-source project provides cross-platform (Windows/macOS/Linux) USB control with removable media encryption, content inspection, or centralized policy management** comparable to Endpoint Protector or Safend. USBGuard solves the Linux allowlisting problem; Windows and macOS control remain commercial territory.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-products)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[CrowdStrike Falcon Device Control](https://www.crowdstrike.com/)**  
  USB device control built on the Falcon platform; combines visibility and granular control to ensure only approved devices are used, with searchable history and logs of USB usage including files written to devices when paired with Falcon Insight . Features source code exfiltration detection across 40+ languages and ZIP archive introspection .

- **[CoSoSys Endpoint Protector](https://www.endpointprotector.com/)**  
  Multi-OS DLP with device control across Windows, macOS, and Linux . Granular policies by device type, brand, and serial number; supports read-only access, encryption, and file tracing . Samsung R&D Institute uses it for peripheral control and data transfer monitoring in a multi-OS environment .

- **[Symantec Device Control](https://www.broadcom.com/)**  
  Device Control policy rules within Symantec Endpoint Protection; blocks or allows devices by GUID (device class) or device ID (specific device), disabling blocked devices in Windows Device Manager . Includes a built-in hardware device list and supports regex matching for device IDs.

- **[McAfee Device Control](https://www.mcafee.com/)**  
  Prevents data loss through removable media (USB, iPods, Bluetooth, CD/DVD); classifies devices by product ID, vendor ID, serial number, device class, and name; supports block, read-only, or content-based encryption policies . Centralized management via McAfee ePO.

- **[DriveLock](https://www.drivelock.com/)**  
  Whitelist-based device control—all devices blocked by default, with rules allowing specific devices by class, bus, hardware ID, or device collection . Rules can be scoped by computer, network connection, user, and time. Includes automatic USB encryption and file transfer logging .

- **[Sophos Device Control](https://www.sophos.com/)**  
  Device control within Sophos endpoint protection; manages removable storage and peripheral access through central policies.

- **[Ivanti Device Control](https://www.ivanti.com/)**  
  Whitelist/default-deny approach for removable devices and ports; supports per-user file type restrictions, daily data copy limits, forced encryption, and shadowing (capturing copied files) . Gartner reviewers note granular control but cite complexity and usability concerns .

- **[ManageEngine Device Control Plus](https://www.manageengine.com/)**  
  USB and peripheral control for Windows and Mac; prioritizes access levels as Allowed > Trusted > Blocked . Supports temporary access, file type/size restrictions, and audit reports. Gartner reviewers note outdated interface but broad service offering .

- **[Microsoft Intune Device Control](https://learn.microsoft.com/)**  
  Device control policies via Intune for Windows endpoints; configures Defender device control with Allow/Deny policies, default enforcement, and device type targeting (RemovableMedia, CdRom, Wpd, Printer) . Note: SID-based user exceptions require matching device identifiers—blanket deny does not auto-override for user allow rules .

- **[Safend Protector](http://www.safend.com/)**  
  Endpoint data protection controlling USB, FireWire, PCMCIA, SD, eSATA, and wireless interfaces; blocks, allows read-only, or encrypts removable storage . Includes anti-bridging (blocking WiFi/Bluetooth on wired LAN) and compliance reporting for PCI/HIPAA/SOX.

## Open-Source GitHub Projects

### Linux USB Authorization (Allowlisting)

- **[USBGuard](https://github.com/USBGuard/usbguard)**  
  The most mature open-source **USB device authorization framework** available, but **Linux-only** (GPLv2+) . Implements allowlisting/default-deny policies via a daemon (`usbguard-daemon`) and CLI (`usbguard`) . Features: `generate-policy` to create an initial ruleset from currently connected devices (critical to avoid locking out keyboard/mouse), allow/block/reject device commands, rule persistence, and LDAP support. **The definitive open-source answer for Linux USB control**—but it does not address Windows or macOS endpoints, and lacks encryption or content inspection.

### Device Monitoring & Scripting

- **[usb-helper](https://pypi.org/project/usb-helper/)**  
  Python library and CLI for **USB device monitoring and profile-based filtering** . Features `--listen` mode emitting JSONL events (init, plug, unplug) designed for piping into automation or AI agents; TOML profiles for named device match rules (VID/PID, serial, name); and a Python API (`USBMonitor`, `DeviceMatchRule`). **Useful for building custom authorization scripts** or monitoring USB activity—but it is a detection/monitoring tool, not an enforcement mechanism.

- **[usb-remote](https://github.com/epics-containers/usb-remote)**  
  FOSS client-server software for **sharing USB devices over a network** using USB/IP (PyPI, Docker) . Positioned as a free alternative to Digi's AnyWhereUSB; server runs on a Raspberry Pi or standard hardware; clients attach remote USB devices as if locally connected. **Different use case**—this is USB-over-network sharing, not endpoint device control or policy enforcement.

### Endpoint Management (Broader Scope)

- **[Fleet](https://github.com/PostHog/fleet)**  
  Open-source **device management platform** (MIT for free tier, built on osquery) for IT and security teams managing Linux, macOS, Windows, Chromebooks, and mobile devices . Provides MDM, patch management, software deployment, and compliance reporting. **Not a dedicated USB control tool**—but it offers endpoint visibility and policy enforcement capabilities that can complement a USB control strategy. Used in production by organizations managing 400,000+ hosts.

### Additional Strong Open-Source Options

- **No cross-platform open-source USB control exists** — The commercial products (Endpoint Protector, Safend, Ivanti) provide Windows/macOS/Linux control with encryption and centralized management. USBGuard covers Linux authorization; no open-source project replicates the full cross-platform feature set.
- **OSQuery (foundation for Fleet)** — Open-source endpoint visibility agent (Apache 2.0) that can query USB device state via SQL-like queries; **visibility only**, not enforcement.

**Frameworks for building custom systems**: For **Linux endpoints**, USBGuard provides production-grade allowlisting . For **custom monitoring/automation**, usb-helper enables event-driven scripting . For **cross-platform endpoint visibility** (not USB-specific enforcement), Fleet provides a foundation . No open-source project delivers **Windows/macOS USB control with encryption and centralized policy**—organizations requiring that should evaluate commercial platforms like Endpoint Protector or Safend.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- USB device control tools enforce endpoint security policies; **misconfiguration can lock out users from keyboards and mice**, rendering systems inaccessible. USBGuard's documentation explicitly warns to generate an initial policy before starting the daemon . Commercial tools like Intune require careful Allow/Deny policy design—overlapping rules can produce unexpected results .
- **Open-source USB control is essentially Linux-only**—USBGuard provides mature authorization for Linux, but **no open-source project offers cross-platform (Windows/macOS) enforcement with encryption and centralized management**. Organizations requiring enterprise-wide USB control should evaluate commercial platforms; those standardizing on Linux can deploy USBGuard with confidence.
- Verify license terms for commercial use; USBGuard uses GPLv2+ , usb-helper is a PyPI package, and Fleet uses MIT for its free tier .

---

**Made for endpoint security engineers, IT administrators, and compliance teams enforcing device control policies.**  
Let's make USB and peripheral control more open, but with clear eyes about the cross-platform enforcement gap that commercial platforms still fill.
