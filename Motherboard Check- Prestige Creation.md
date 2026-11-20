# 30-Day Validation & Burn-In Checklist 

> **Motherboard:** MSI Prestige X570 Creation (E-ATX, 305 mm × 272 mm)  
> **Core:** AMD Ryzen 7 3800X | 64GB (4×16GB) G.Skill Ripjaws V DDR4-3200 | MSI MAG A1000GL 1000W  
> **GPUs:** RTX 5060 Ti 16GB (`PCI_E2`) + RTX 5060 8GB (`PCI_E5`) + RTX 2060 6GB (`PCI_E7`)  
> **Storage:** Samsung 990 Pro 2TB Factory Heatsink (`M2_1`) + SK Hynix Gold P31 512GB (`M2_2`)  
> **Chassis:** NZXT H710i (272 mm max E-ATX clearance)  

---

## Phase 1: Unboxing, Physical Inspection & Bench Prep (No Power)
- [x] **Static-Safe Bench Surface:** Place the motherboard strictly on bare, untaped corrugated cardboard (flip the shipping box over, fold flaps out, or lay plain printer paper over any packing tape). Never rest the board on the conductive exterior of the anti-static bag or directly on static-charged packing tape.
- [x] **Socket Pin Inspection:** Under bright light and magnification, verify all 1,331 AM4 pin holes are unobstructed with no bent contacts, sheared gold pins, or debris.
- [x] **Backside PCB & Trace Audit:** Check the reverse PCB around the CPU cutout and VRM stages for gouges, severed copper traces, or dark/scorched solder mask.
- [x] **Slots & Headers Check:** Verify all three steel-armored PCIe x16 latches (`PCI_E2`, `PCI_E5`, `PCI_E7`) and four DIMM latches click firmly, M.2 standoffs (`M2_1`, `M2_2`) are intact, and all fan, USB 3.0/Type-C, and audio header pins are straight.
- [x] **Socket & Backside Cleanup:** Wipe dried white thermal paste off the exterior AM4 socket latch shelf (sweeping away from pin holes) and any flux haze off the backside CPU cutout using a lint-free swab with 91%+ or 99% isopropyl alcohol; air-dry for 2 minutes.
- [x] **Install Spare AM4 Backplate:** Mount your spare metal AM4 backplate to the rear of the motherboard.
- [x] **Chipset Fan Check:** Spin the black X570 chipset fan gently by finger to confirm smooth rotation without bearing grind, wobble, or shroud scraping.
- [x] **CR2032 CMOS Battery Check:** Measure cell voltage with a multimeter; swap in a fresh CR2032 battery if reading below `2.95V`.

---

## Phase 2: Bare-Board Power Delivery & Flash BIOS Button Recovery
- [x] **Bare-Board Power Hookup:** Connect **only** the 24-pin `ATX_PWR1` and both 8-pin `CPU_PWR1` / `CPU_PWR2` cables from the MSI MAG A1000GL PSU (leave CPU, RAM, NVMe, and GPUs uninstalled).
- [x] **Stage BIOS Flash Media:** Format an empty USB 2.0 flash drive (≤32GB) to **FAT32 (MBR)** and copy the latest non-beta MSI Prestige X570 Creation BIOS renamed strictly to `MSI.ROM` into the root directory.
- [x] **Execute Flash BIOS Button:** Insert the USB drive into the dedicated rear **Flash BIOS Port**, flip the PSU rocker switch on, and press the rear **Flash BIOS Button**.
- [x] **Verify Flash Completion:** Confirm the red LED blinks slowly (~15–20s), blinks rapidly for 4–6 minutes, and shuts off automatically. *(If it stops after 3–5 blinks or stays solid, reformat a different ≤32GB USB 2.0 drive as MBR/FAT32 and repeat).*
- [x] **Purge Prior Owner CMOS:** Turn off the PSU switch and press/hold the rear I/O **Clear CMOS** button for 10 seconds (or short `JBAT1` pins) to clear any residual settings from the previous owner.
- [x] **Stage Custom NVIDIA Utilities:** Download `NVCleanstall_1.19.0.exe` (TechPowerUp) and `nvidiaProfileInspector.zip` (GitHub `Orbmu2k/nvidiaProfileInspector`) onto your validation USB drive so they are ready offline on first Windows boot.

---

## Phase 3: Core POST, 4-DIMM Memory & CMOS Persistence
- [x] **Minimal Out-of-Case Assembly:** Install Ryzen 7 3800X, apply thermal paste, mount cooler, seat one 16GB DDR4 stick in `DIMMA2` (2nd slot from CPU), and seat RTX 5060 Ti 16GB in `PCI_E2` with a monitor attached.
- [x] **First Boot & Debug Codes:** Power on via the onboard `POWER1` button (bottom-right PCB). Confirm EZ Debug LEDs (`CPU` → `DRAM` → `VGA` → `BOOT`) clear sequentially and the 2-digit Debug Code LED settles on `AA` or `00` (not stalled on `0d` or `55`).
- [x] **Populate All 4 DIMM Slots:** Power down and install all four 16GB sticks (`DIMMA1`, `DIMMA2`, `DIMMB1`, `DIMMB2`).
- [x] **Configure UEFI Memory & FCLK:** Enter Click BIOS 5 (`Delete`), 
	- [x] verify all `65,536 MB` (64GB) registers at baseline JEDEC speeds, 
	- [x] enable **A-XMP Profile 1** (`3200 MHz, 16-18-18-38 @ 1.35V`), and 
	- [x] manually set **FCLK (Infinity Fabric)** to `1600 MHz` (1:1 ratio).
- [x] **MemTest86 Cold-Boot Validation:** Boot a UEFI MemTest86 USB drive before loading the OS and complete **4 full passes across all 13 tests** with strictly **0 errors**.
- [x] **CMOS Persistence Check:** Turn off the PSU rocker switch for 60 seconds, restore power, and enter BIOS to verify the system clock and A-XMP profile survived the AC cut.

---

## Phase 4: Triple-GPU Bifurcation & NVMe Lane Audit
- [x] **Populate NVMe Drives:** Install the factory-heatsink Samsung 990 Pro 2TB in bare `M2_1` (CPU PCIe 4.0 x4) and SK Hynix Gold P31 512GB in `M2_2` under the silver Shield Frozr cover (chipset PCIe 4.0 x4). Confirm both appear in BIOS `Board Explorer`.
- [x] **Install Dual 50-Series GPUs:** Seat RTX 5060 Ti 16GB in `PCI_E2` (top armored slot) and RTX 5060 8GB in `PCI_E5` (middle armored slot) using dedicated, non-daisy-chained PCIe power cables.
- [x] **Configure BIOS PCIe Settings:** Navigate to `Settings \ Advanced \ PCI Subsystem Settings` and set:
  - [x] **PCIe Lane Configuration:** `x8 / x8`(x8 / x4 / x4)
  - [x] **PCIe Link Speed:** `Gen 4`
  - [x] **Above 4G Decoding:** `Enabled`
  - [x] **Re-Size BAR Support:** `Enabled`
- [x] **NVCleanstall & Profile Inspector Tuning:**
  - [x] Install stripped NVIDIA driver via NVCleanstall (keep **NVIDIA Container**, strip GeForce Experience/Telemetry/Shield, check **Enable Message Signaled Interrupts (MSI)** with `Interrupt Policy: Default` and `Interrupt Priority: Normal / Undefined`).
- [x] **Verify Dual-Card Bifurcation Under Load:** open two instances of **GPU-Z**, run the built-in PCIe Render Test (`?` button) on both simultaneously (or check `nvidia-smi -q`), and verify both sustain `PCIe x8 4.0 @ x8 4.0`.
- [x] **Install Third GPU (`PCI_E7`):** Power down, seat RTX 2060 6GB in `PCI_E7` (bottom armored slot), boot into Windows, and run GPU-Z Render Test on Card 3.
- [ ] **Confirm Full Bus Integrity:**
  - [ ] `PCI_E7` (RTX 2060) sustains `PCIe x4 3.0 @ x4 3.0`.
  - [ ] Both NVMe drives remain mounted in Disk Management (zero chipset lane collision).
  - [ ] Device Manager reports zero Code 43 errors across all three GPUs. *(Initiate eBay return immediately if `PCI_E2` or `PCI_E5` drops to x4/x2/x1 under load).*

---

## Phase 5: Thermal, Bus Saturation, VRM & WHEA Torture Testing

- [ ] **NVMe Bus Saturation (`M2_1`):** Run CrystalDiskMark (Admin, 5-pass 64 GiB) on Samsung 990 Pro 2TB; confirm ~`7,000–7,450 MB/s` Sequential Read.
- [ ] **NVMe Bus Saturation (`M2_2`):** Run CrystalDiskMark (Admin, 5-pass 16 GiB) on SK Hynix Gold P31 512GB; confirm ~`3,500 MB/s` Sequential Read without dropouts.
- [ ] **60-Minute Combined VRM & GPU Torture:** Launch HWiNFO64 (*Sensors Only*), Prime95 (*Small FFTs*), and two concurrent FurMark 2 instances (RTX 5060 Ti + RTX 5060) for 60 minutes:
  - [ ] **VRM MOS Temp:** Stabilizes under `75°C–85°C` on open air.
  - [ ] **Chipset (PCH) Temp:** Remains under `70°C–75°C` with steady fan RPM.
  - [ ] **12V Rail Stability:** Holds between `11.80V` and `12.20V`.
  - [ ] **WHEA Hardware Errors:** Reads strictly `0` at the bottom of HWiNFO64.

  - [ ] Set **Prefer No Sysmem Fallback** in NVIDIA Profile Inspector.
- [ ] **48-Hour AI Workload Burn-In:** Run a continuous 2+ hour ComfyUI batch + Ollama multi-GPU model split across all three GPUs and keep the system running for 48 hours with **0 WHEA errors**.

---

## Phase 6: 10GbE Networking, I/O Sweep, Headless Setup & Chassis Install
- [ ] **Dual-NIC Throughput & Ping Test:** Test both rear Ethernet ports individually (Marvell Aquantia AQC107 10GbE and Intel I211AT 1GbE) via `iperf3` / SMB transfer and a 10-minute ping (`ping 1.1.1.1 -t -l 1000`) with `0%` packet loss.
- [ ] **Wi-Fi 6 & Bluetooth Check:** Thread spare RP-SMA antennas onto the rear brass SMA posts and confirm Intel Wi-Fi 6 AX200 and Bluetooth connect cleanly without Code 10/43 errors.
- [ ] **Rear USB Array & Audio Ground Check:** Test a USB 3.2 Gen 2 drive across every rear Type-C and Type-A port individually; plug headphones into the green 3.5 mm jack during a GPU render to verify zero electrical hiss or ground-loop buzz.
- [ ] **Configure Headless Boot, WOL & Remote Access:**
  - [ ] In BIOS (`Settings \ Advanced \ Power Management Setup`), set **Restore after AC Power Loss** to `[Power On]`.
  - [ ] In BIOS (`Settings \ Advanced \ Wake Up Event Setup`), set **Resume By PCI-E Device** to `[Enabled]` for Wake-on-LAN.
  - [ ] In BIOS (`Settings \ Boot`), lock Samsung 990 Pro as **Boot Option #1**.
  - [ ] In Windows 11, enable **Remote Desktop (RDP)** and **OpenSSH Server** (`Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.5.0`).
  - [ ] Unplug the monitor from RTX 5060 Ti, reboot, and confirm headless POST (white `VGA` debug LED staying lit is normal) plus SSH, RDP, and ComfyUI (`--listen 0.0.0.0 --port 8188`) reachability. *(Insert a $5 HDMI dummy plug into `PCI_E2` only if using Sunshine/Moonlight/Parsec desktop streaming).*
- [ ] **NZXT H710i Chassis Transfer:**
  - [ ] Loosen the retention screws on the H710i vertical cable management bar and slide it to the rightmost mounting slot (or remove it) to clear the 272 mm E-ATX width.
  - [ ] Pre-route both 8-pin EPS cables through the top-left case cutout before lowering the board onto the standoffs (verify no extra standoffs touch the silkscreened `Case standoff keep out zone` circles on the rear PCB).
  - [ ] Support the overhanging right edge of the PCB from underneath with two fingers while latching the right-angle 24-pin ATX power plug and right-angle USB 3.0 front-panel headers.
  - [ ] Install all three GPUs, confirming the full 3-slot intake air gap between `PCI_E2` and `PCI_E5`.

---

## Final Validation Sign-Off

| Metric | Target / Requirement | Observed Value | Status (Pass/Fail) |
| :--- | :--- | :--- | :--- |
| **BIOS Version** | Latest Non-Beta Release (`MSI.ROM`) | | |
| **MemTest86** | 4 Full Passes / 64GB DDR4 @ 3200 MHz (1600 FCLK) | | |
| **`PCI_E2` (RTX 5060 Ti)** | Active Load via GPU-Z: `PCIe x8 4.0 @ x8 4.0` | | |
| **`PCI_E5` (RTX 5060)** | Active Load via GPU-Z: `PCIe x8 4.0 @ x8 4.0` | | |
| **`PCI_E7` (RTX 2060)** | Active Load via GPU-Z: `PCIe x4 3.0 @ x4 3.0` | | |
| **Samsung 990 Pro (`M2_1`)** | CrystalDiskMark Seq Read: `~7,000+ MB/s` | | |
| **SK Hynix P31 (`M2_2`)** | CrystalDiskMark Seq Read: `~3,500 MB/s` | | |
| **HWiNFO64 WHEA Errors** | 60-Min Torture + 48-Hr Burn-In: Strictly `0` | | |
| **VRM MOS / PCH Temps** | Peak Load: VRM `< 85°C` / PCH `< 75°C` | | |
| **10GbE & 1GbE NICs** | Full Link Throughput / `0%` Packet Loss | | |
| **Headless Boot & AC Loss** | Auto-Power-On & SSH/RDP/ComfyUI Reachable | | |
| **30-Day Return Expiry** | **Deadline Date:** `2026-12-17` | **Tested Date:** | |