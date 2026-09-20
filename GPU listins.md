### 📋 PROJECT SYSTEM STATE: AM4 Dual/Tri-GPU AI & Adobe Workstation

**1. Hardware Inventory**

* **CPU:** AMD Ryzen 7 3800X (AM4 Socket)
* **RAM:** 64GB G.Skill Ripjaws V DDR4-3200
* **PSU:** MSI MAG A1000GL (1000W)
* **Storage:** Samsung 990 Pro 2TB (PCIe 4.0), SK Hynix Gold P31 500GB (PCIe 3.0)
* **Case:** NZXT H710i
* **Primary GPUs:** 1x RTX 5060 Ti 16GB, 1x RTX 5060 8GB (Blackwell Architecture - 24GB Pool)
* **Legacy GPU:** 1x RTX 2060 6GB (Turing Architecture)

**2. The Workload & OS Constraints**

* **Adobe Creative Cloud Dependency:** A stable Windows 11 environment is required for Photoshop. Linux via VM passthrough or community Wine patches remains too unstable for daily production work.
* **Windows WDDM Limitation:** Splitting multi-GPU setups across CPU root lanes and Chipset controller lanes triggers a fatal "Error 43" driver initialization halt.
* **AI Architecture Bottlenecks:** Mixing the Turing-based RTX 2060 with Blackwell RTX 50-series cards in the same inference pipeline cripples generation speed, disables FlashAttention, and lacks native FP8/BF16 precision support needed for models like Flux-FP8 and Qwen 32B.

**3. The Two-Phase Rollout Strategy**

* **Phase 1 (Current):** Run a clean **2-GPU setup** (5060 Ti + 5060) natively in Windows. This provides an unthrottled 24GB VRAM pool for ComfyUI and local LLMs, full Adobe stability, and mounts cleanly inside the chassis without PCIe riser ribbons.
* **Phase 2 (Future):** When transitioning production workflows over to Linux (Krita, GIMP), add the RTX 2060 into the bottom x4 chipset slot strictly for monitor display output. `CUDA_VISIBLE_DEVICES` will isolate the two 5060s as a 24GB headless compute pool, keeping the 2060 invisible to PyTorch.

**4. Motherboard Selection Criteria**

* **Mandatory Requirement:** The motherboard must feature hardware multiplexers/redrivers supporting true CPU lane bifurcation into an **x8 / x8** split on the primary PCIe slots to ensure Windows driver stability.
* **Disqualified Hardware:** Standard consumer B550/X570 boards (wired for x16 CPU / x4 Chipset), the Gigabyte B550 AORUS Master (bifurcates lanes to M.2 instead of PCIe slots), and all AM5/DDR5 boards.
* **Retail Guidance:** Avoid third-party liquidation listings on Amazon due to high return and RMA failure rates on out-of-production AM4 stock; prioritize authorized vendors (B&H, Newegg) or vetted hardware recyclers with socket photos and return coverage.

---

### Approved for 3-Card Setups (x8 / x8 CPU + x4 Chipset)

These motherboards provide the x8/x8 CPU lane split for dual 50-series cards in Windows, while providing a dedicated bottom x4 chipset slot for the RTX 2060 in Linux without disabling primary NVMe drives.

| Motherboard                                | Chipset | PCIe Layout  | M.2 Slots   | Standout Feature                                                  |
| ------------------------------------------ | ------- | ------------ | ----------- | ----------------------------------------------------------------- |
| **MSI MEG X570 UNIFY**                     | X570    | x8 / x8 / x4 | 3x PCIe 4.0 | Robust VRM cooling, onboard Q-Code readout                        |
| **MSI MEG X570 ACE**                       | X570    | x8 / x8 / x4 | 3x PCIe 4.0 | Sibling to UNIFY; high-end VRM, onboard Q-Code LED                |
| **ASUS ROG Crosshair VIII Hero**           | X570    | x8 / x8 / x4 | 2x PCIe 4.0 | Flagship 14+2 VRM, physical Q-Code readout, extreme build quality |
| **ASUS ProArt X570-Creator WIFI**          | X570    | x8 / x8 / x4 | 3x PCIe 4.0 | Dual Thunderbolt 4 ports, 10GbE + 2.5GbE LAN                      |
| **ASUS ROG Strix X570-E Gaming / WiFi II** | X570    | x8 / x8 / x4 | 2x PCIe 4.0 | Onboard Q-Code diagnostics, built-in Wi-Fi 6                      |
| **Gigabyte X570 AORUS Master**             | X570    | x8 / x8 / x4 | 3x PCIe 4.0 | 14-phase VRM; 3rd M.2 disables SATA, not PCIe                     |
| **ASUS Prime X570-Pro**                    | X570    | x8 / x8 / x4 | 2x PCIe 4.0 | Balanced baseline workstation layout                              |

---

### Approved for Dual-Card Only (x8 / x8 CPU Bifurcation)

If you commit strictly to running the RTX 5060 Ti and RTX 5060 without adding a third card, these motherboards provide the required x8/x8 CPU lane split without needing a 3-slot X570 design. *(Any board in the 3-card table above also functions here by leaving the third slot unpopulated).*

| Motherboard | Chipset | PCIe Layout | M.2 Slots | Standout Feature |
| --- | --- | --- | --- | --- |
| **ASUS ProArt B550-Creator** | B550 | x8 / x8 | 1x Gen 4, 1x Gen 3 | Dual Thunderbolt 4 ports, dual 2.5GbE LAN |
| **ASUS ROG Strix B550-E Gaming** | B550 | x8 / x8 | 1x Gen 4, 1x Gen 3 | 14+2 VRM, Q-Code display, built-in Wi-Fi 6 |
| **Gigabyte B550 VISION D / D-P** | B550 | x8 / x8 | 1x Gen 4, 1x Gen 3 | Dual Thunderbolt 3 (Titan Ridge), creator-focused I/O |
| **ASRock B550 Taichi / Razer Edition** | B550 | x8 / x8 | 1x Gen 4, 1x Gen 3 | 16-phase power delivery, physical POST display |
| **Gigabyte X570S AERO G** | X570S | x8 / x8 | 4x PCIe 4.0 | Fanless passive chipset, VisionLINK USB-C |
| **MSI MPG X570S Carbon MAX WiFi** | X570S | x8 / x8 | 4x PCIe 4.0 | Fanless passive chipset, 4x shielded M.2 heatsinks |
| **ASRock X570 Creator** | X570 | x8 / x8 | 2x PCIe 4.0 | Dual Thunderbolt 3, AQUANTIA 10GbE LAN |