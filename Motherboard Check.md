# AM4 Motherboard 30-Day RMA Stress-Test Protocol

Execute this hardware validation protocol on an open bench before building inside the NZXT H710i chassis. Complete all phases within the 30-day seller return window to identify broken PCB traces, failed PCIe redrivers, damaged DIMM slots, or degraded VRM power stages.

---

## Phase 1: Unboxing, Physical Inspection & Out-of-Case POST

- [ ] **1.1 Socket & Trace Inspection**
  - Use high-intensity light and magnification to inspect the AM4 pin receptacle holes for bent pins, thermal paste contamination, or foreign debris.
  - Check the back of the PCB around the CPU socket backplate and VRM areas for gouges, severed copper traces, or dark/scorched solder pads.
- [ ] **1.2 Expansion Slots & Physical Headers**
  - Verify PCIe x16 retention clips are unbroken and have firm mechanical tension.
  - Inspect M.2 standoff threads; ensure standoffs and mounting screws are not stripped, missing, or cross-threaded.
  - Verify all onboard fan headers, USB 3.0/Type-C front-panel pins, and front-panel audio headers are straight.
- [ ] **1.3 Bench Test Setup**
  - Place the motherboard on its original cardboard box (never on anti-static bags, which have conductive outer coatings).
  - Install only:
    - AMD Ryzen 7 3800X CPU + cooler.
    - One 16GB G.Skill DDR4 stick in slot `DIMMA2` (2nd slot from CPU).
    - MSI MAG A1000GL 24-pin ATX + dual 8-pin EPS CPU power cables.
    - RTX 2060 or a single 5060 in PCIe Slot 1 for basic display output.
- [ ] **1.4 BIOS Recovery & AGESA Update**
  - Boot into UEFI or utilize the rear BIOS FlashBack button with a FAT32 USB flash drive.
  - Flash to the latest stable non-beta BIOS to ensure modern AGESA microcode, PCIe bifurcation stability, and Resizable BAR support.
  - Clear CMOS (short the CLRTC pins or remove the CR2032 battery for 5 minutes) to wipe any previous user overclocking profiles.

---

## Phase 2: Memory Controller & 4-DIMM Channel Verification

- [ ] **2.1 Populate All Memory Slots**
  - Install all four 16GB G.Skill Ripjaws V DDR4 modules (`DIMMA1`, `DIMMA2`, `DIMMB1`, `DIMMB2`) to fully load both memory channels and test the traces to all four slots.
- [ ] **2.2 UEFI Configuration**
  - Enter UEFI and verify all 64GB (65,536 MB) is recognized at baseline JEDEC speeds (2133/2400 MHz).
  - Enable **DOCP / XMP Profile 1** (3200 MHz, 16-18-18-38 @ 1.35V).
  - Set `FLCK` (Infinity Fabric) manually to `1600 MHz` (1:1 ratio with 3200 MT/s RAM).
- [ ] **2.3 MemTest86 Cold-Boot Pass**
  - Boot into a UEFI MemTest86 USB drive before loading any operating system.
  - Run **4 complete passes** across all 13 tests.
  - **Pass Criteria:** Strictly **0 errors**. Any error indicates cold solder joints under the AM4 socket, broken DIMM slot traces, or weak memory trace signal integrity.

---

## Phase 3: PCIe Bifurcation & Multi-GPU Lane Negotiation

- [ ] **3.1 Storage & GPU Populated Layout**
  - Install the **Samsung 990 Pro 2TB** into Slot `M.2_1` (CPU direct lanes, top slot).
  - Install the **SK Hynix P31 500GB** into Slot `M.2_2` (Chipset lanes).
  - Install the **RTX 5060 Ti 16GB** into PCIe Slot 1 (`PCI_E1`).
  - Install the **RTX 5060 8GB** into PCIe Slot 2 (`PCI_E2` / `PCI_E3` bifurcated x8 slot).
  - Connect separate, dedicated PCIe power cables from the MSI A1000GL to each card (no daisy-chain pigtails).
- [ ] **3.2 BIOS Bifurcation Settings**
  - Navigate to: `Advanced` > `PCI Subsystem Settings` (or chipset specific lane configuration).
  - Set `PCIe_1 / PCIe_2 Lane Configuration` from `Auto` to **`x8 / x8`**.
  - Set `PCIe Link Speed` manually to **`Gen 4`**.
  - Enable **`Above 4G Decoding`** and **`Re-Size BAR Support`**.
- [ ] **3.3 Windows 11 Lane Verification (GPU-Z)**
  - Boot into clean Windows 11 installation; install the latest NVIDIA Studio/Game Ready Driver.
  - Open two simultaneous instances of **GPU-Z** (one targeting Card 1, one targeting Card 2).
  - Click the **`?`** icon next to the "Bus Interface" box on both instances and start the built-in PCIe Render Test.
  - **Pass Criteria:**
    - Card 1 actively reports: `PCIe x8 4.0 @ x8 4.0`.
    - Card 2 actively reports: `PCIe x8 4.0 @ x8 4.0`.
    - *(If either drops to x4, x2, or Gen 1.1/2.0 while under load, the motherboard's PCIe redrivers or lane multiplexer chips are defective).*
- [ ] **3.4 Phase 2 Slot 3 Test (Chipset x4 Slot)**
  - Power down, keep the dual 50-series cards in place, and install the **RTX 2060** into the bottom physical PCIe x16 (wired as x4) chipset slot.
  - Boot into Windows; launch GPU-Z on Card 3.
  - Run the Render Test on the 2060.
  - **Pass Criteria:**
    - Card 3 actively reports: `PCIe x4 3.0 @ x4 3.0` (or `PCIe x4 4.0 @ x4 3.0`).
    - Both NVMe drives remain fully mounted in Windows Explorer and Disk Management (verifies no PCIe/SATA lane collision or chipset link dropouts).
    - Device Manager reports "This device is working properly" for all three cards with **zero Code 43 errors**.

---

## Phase 4: Full Thermal, VRM & WHEA Error Stress Testing

- [ ] **4.1 NVMe Bus Saturation Test**
  - Open **CrystalDiskMark** (Admin mode).
  - Target the Samsung 990 Pro 2TB (`M.2_1`): Run a 5-pass **64 GiB** Sequential Read/Write profile.
  - **Pass Criteria:** Sequential Read hits ~7,000–7,450 MB/s, confirming direct CPU PCIe 4.0 x4 communication without bus clipping.
  - Target the SK Hynix P31 500GB (`M.2_2`): Run a 5-pass **16 GiB** profile; verify ~3,500 MB/s Sequential Read without chipset dropouts.
- [ ] **4.2 Combined VRM & Bus Torture Test (60 Minutes)**
  - Launch **HWiNFO64** (Sensors Only).
  - Launch **Prime95** -> Select **Small FFTs** (maximum CPU package and VRM current load).
  - Launch **FurMark 2** -> Open two separate render instances, binding one to the RTX 5060 Ti and one to the RTX 5060.
  - Run both Prime95 and dual FurMark instances concurrently for **60 minutes**.
- [ ] **4.3 Telemetry Checks (During Load)**
  - **VRM MOS Temperature:** Must stabilize under **85°C** with baseline airflow.
  - **Chipset (PCH) Temperature:** Must stay under **75°C** (check active PCH fan on older X570 models).
  - **12V Rail Stability:** Must remain between **11.80V and 12.20V** under total combined draw.
- [ ] **4.4 WHEA Error Log Inspection**
  - Scroll to the absolute bottom of the HWiNFO64 sensor panel to: **Windows Hardware Errors (WHEA)**.
  - **Pass Criteria:** WHEA Total Errors must read strictly **0**.
  - *(Any number above 0 indicates uncorrectable PCIe bus parity errors, failing motherboard redrivers, or degraded VRM power filtering).*

---

## Phase 5: I/O, Networking & Peripheral Validation

- [ ] **5.1 Network Controller Throughput**
  - Plug an Ethernet cable into the onboard RJ-45 LAN port; run a continuous ping test (`ping 1.1.1.1 -t -l 1000`) for 10 minutes. Ensure 0% packet loss.
  - Test Wi-Fi/Bluetooth connectivity (if board is equipped) by pairing an audio device and transferring a file.
- [ ] **5.2 USB Port Array Verification**
  - Plug a fast USB 3.0 flash drive or external SSD into **every single USB port** on the rear I/O shield individually.
  - Confirm Windows mounts the drive at SuperSpeed without disconnect/reconnect loops (checks for damaged USB controller traces or blown polyfuses).
- [ ] **5.3 Audio DAC & Ground Plane**
  - Plug headphones into the rear green 3.5mm line-out jack.
  - Play an audio track while running a heavy GPU render.
  - Verify there is no electrical hiss, coil whine interference, or ground loop buzzing bleeding through the audio traces.

---

## Final Validation Sign-Off

| Metric                   | Target / Requirement             | Observed Value         | Status (Pass/Fail) |
| :----------------------- | :------------------------------- | :--------------------- | :----------------- |
| **BIOS Version**         | Latest Non-Beta Release          |                        |                    |
| **MemTest86**            | 4 Full Passes / 64GB DDR4 @ 3200 | 0 Errors               |                    |
| **PCIe Slot 1 Bus**      | Under Load via GPU-Z             | `PCIe x8 4.0 @ x8 4.0` |                    |
| **PCIe Slot 2 Bus**      | Under Load via GPU-Z             | `PCIe x8 4.0 @ x8 4.0` |                    |
| **PCIe Slot 3 Bus**      | Under Load via GPU-Z             | `PCIe x4 3.0 @ x4 3.0` |                    |
| **Samsung 990 Pro**      | CrystalDiskMark Seq Read         | ~7,000+ MB/s           |                    |
| **HWiNFO64 WHEA**        | 60-Min Prime95 + Dual GPU Load   | **0 Errors**           |                    |
| **VRM MOS Temp**         | 60-Min Peak Temperature          | < 85°C                 |                    |
| **30-Day Return Expiry** | Date: `____________________`     | Tested on Day:         |                    |