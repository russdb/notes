1. Open **PowerShell** or **Command Prompt** as Administrator.
2. Query the active PCIe link generation and width for both cards
```sh
nvidia-smi --query-gpu=index,name,pstate,pcie.link.gen.current,pcie.link.gen.max,pcie.link.width.current,pcie.link.width.max --format=csv
```  

- **`pcie.link.gen.current`**: The real-time generation (will report `1` if idling, `4` under load).
- **`pcie.link.gen.max`**: The maximum supported on this platform (`4`).
- **`pcie.link.width.current`**: The active lane count (should report `8`).  

3. Enable Persistence Mode to keep the driver kernel module loaded and prevent aggressive ASPM sleep states on both cards:

```sh
nvidia-smi -pm 1
```  

If you want to place a load on both GPUs to force the PCIe links to train up to Gen 4 without opening a GUI, run

```sh
nvidia-smi dmon
```

On Windows 11 LTSC IoT, the modern DCH Control Panel is missing because the OS lacks the Microsoft Store framework by default. You can bypass the GUI entirely using `nvidia-smi` to manage clocks and verify PCIe bus states, or sideload the Control Panel package directly via PowerShell.

1. **Enable Driver Persistence Mode**: Open an Administrator Command Prompt or PowerShell and lock the driver kernel into memory

```
nvidia-smi -pm 1
```

2. **Lock GPU Clocks to Force Active PCIe States**: Idle GPUs drop to PCIe Gen 1.1 to conserve power. You can force both cards into their active 3D performance state (`P0`) by temporarily locking their core clocks:

```
nvidia-smi -lgc 1500,2000
```
_(This locks the minimum and maximum graphics clocks between 1500 MHz and 2000 MHz, immediately forcing the PCIe controller out of ASPM idle)._  

3. **Stream Real-Time PCIe Link Status**: Run a 1-second continuous telemetry loop:

```
nvidia-smi --query-gpu=index,name,pstate,clocks.gr,pcie.link.gen.current,pcie.link.width.current --format=csv -l 1
```
*Pass criteria under lock/load:* Both RTX 5060 cards should report:   `pcie.link.gen.current: 4` and `pcie.link.width.current: 8`

`nvidia-smi --query-gpu=index,name,pcie.link.gen.current,pcie.link.width.current --format=csv`

4. **Reset Clocks Back to Normal**: Once validation is complete, restore standard dynamic clocking:
```
nvidia-smi -rgc
```  

5. **Device Manager Audit**: Run `devmgmt.msc` and expand **Display adapters** to confirm all three GPUs are listed cleanly with zero error flags (Code 43).

If you want to manage 3D driver settings (like forcing Prefer Maximum Performance or disabling CUDA P2 State) without any UWP or DCH packages at all:

1. Download the standalone, open-source NVIDIA Profile Inspector.

It is a single, zero-install portable .exe that hooks directly into NVIDIA's driver API (nvapi64.dll).    

2. Scroll down to Common

- Set Power management mode to Prefer maximum performance.
- Set CUDA - Force P2 State to Off (ensures compute tasks hit full clocks).

2. Click **Apply Changes** in the top right corner. The settings apply to the driver immediately without any Control Panel running.

Expected output at Idle:
```sh
index, name, pci.bus_id, pcie.link.gen.current, pcie.link.width.current
0, NVIDIA GeForce RTX 2060, 00000000:04:00.0, 1, 8
1, NVIDIA GeForce RTX 5060, 00000000:05:00.0, 1, 8
2, NVIDIA GeForce RTX 5060, 00000000:0A:00.0, 1, 4
```

Expected output at Load:
```sh
index, name, pci.bus_id, pcie.link.gen.current, pcie.link.width.current
0, NVIDIA GeForce RTX 2060, 00000000:04:00.0, 3, 8
1, NVIDIA GeForce RTX 5060, 00000000:05:00.0, 4, 8
2, NVIDIA GeForce RTX 5060, 00000000:0A:00.0, 4, 4
```

To test and saturate the secondary card's PCIe link independently without display routing interference, use command-line targeting via `nvidia-smi` or run a dedicated CUDA bus test.

1. **Identify the GPU Index**: Run `nvidia-smi` to see which index corresponds to which card:
```
nvidia-smi --query-gpu="index,name,pci.bus_id" --format="csv"
```

2. **Lock Clocks on the Specific Card**: Target only the card that was idling (for example, GPU index `1`)
```
nvidia-smi -i 1 -lgc "1500,2000"
```
_(This immediately forces GPU 1 out of ASPM power-saving and locks it into an active performance state)._

3. **Monitor Link Training in Real Time**: Open a separate PowerShell window and poll GPU 1 every second:
```
nvidia-smi -i 1 --query-gpu="index,name,pstate,pcie.link.gen.current,pcie.link.width.current" --format="csv" -l 1
```

- **Verification**: `pcie.link.gen.current` should immediately report `4`, and `pcie.link.width.current` should report `8`.
- **Release Clocks When Finished**: Restore default dynamic power states:

```
nvidia-smi -i 1 -rgc
```

If you want actual data moving across the PCIe bus rather than just clock-state verification, use NVIDIA’s official CUDA `bandwidthTest` utility. Unlike DirectX render tests, CUDA targets device IDs directly without Windows display subsystem redirection.

1. Locate or download `bandwidthTest.exe` (part of the NVIDIA CUDA Samples / GPU Deployment Kit).
2. Run a device-to-host and host-to-device memory copy sweep explicitly targeting device `1`
```
bandwidthTest.exe --device=1 --memory=pinned --mode=shmoo
```

**Expected Throughput Values**:

- **PCIe 4.0 x8 (Slot 1 or Slot 2)**: Sustained transfers between **12.5 GB/s and 14.5 GB/s**.
- **PCIe 4.0 x4 (Slot 3 via Chipset)**: Sustained transfers between **6.2 GB/s and 7.2 GB/s**.
- _(If the link drops to Gen 1.1 or Gen 2 during transfers, throughput will collapse below 3 GB/s, confirming a physical bus or signaling issue)._  

> using 1500,2000 neither card gets over 2,8

Locking GPU core clocks with -lgc forces the graphics engine out of sleep, but it generates zero data traffic across the PCIe bus, leaving the link controller in an intermediate Gen 2 (5 GT/s) power-saving state.

On an AMD X570 platform like the ASUS ROG Crosshair VIII Dark Hero, holding at Gen 2 x8 across both slots under a clock clamp points to one of three specific causes: lack of actual bus transfer activity, motherboard hardware-level ASPM overriding the OS, or high-frequency signal attenuation.


### Temporarily Move the Display Cable

If you want to use GPU-Z's visual render test specifically on that second card:

1. Shut down the PC.
2. Move your monitor's DisplayPort/HDMI cable directly to the output ports of the second card.
3. Boot into Windows. That card will now register as the active WDDM display adapter, forcing GPU-Z's DirectX render test to execute directly on its silicon.

### 1. Generate Actual PCIe Bus Traffic

NVIDIA's PCIe PHY controllers will not step up to Gen 4 (16 GT/s) without active host-to-device memory transactions. To test link speeds under genuine load without a GUI

1. **Run a CUDA Bus Bandwidth Saturation Test**: Download the standalone `bandwidthTest.exe` binary (from the CUDA Toolkit) and run a continuous transfer loop:
```
bandwidthTest.exe --device=0 --memory=pinned --mode=shmoo
```

2. **Monitor Real-Time Link Speed While Traffic Moves**: In a second terminal window, monitor the link generation while `bandwidthTest` is actively pushing data
```
nvidia-smi -i 0 --query-gpu="index,pcie.link.gen.current,pcie.link.gen.max,pcie.link.width.current" --format="csv" -l 1
```
_If the card jumps to `4, 4, 8` while transferring data, the bus is fully functional and the Gen 2 reading was purely dynamic power gating._


### 2. Disable Hardware ASPM in the ASUS Dark Hero UEFI

If the bus refuses to negotiate beyond Gen 2 even under active memory transfer, the motherboard’s native PCIe power management is restricting the link states.

1. Reboot and enter the UEFI BIOS (**Del** or **F2**).
2. Switch to **Advanced Mode** (**F7**).
3. Navigate to **Advanced** -> **Platform Misc Configuration**:
	- Set **PCI Express Native Power Management** to **Disabled**.
	- Set **Native ASPM** to **Disabled**.
	- Set **DMI Link ASPM Control** to **Disabled**.
	- Set **PEG - ASPM** to **Disabled**.
4. Navigate to **Advanced** -> **AMD PBS**:
	- Confirm **PCIEX16_1 Link Mode** is set to **GEN 4**.
	- Confirm **PCIEX16_2 Link Mode** is set to **GEN 4**.
5. Press **F10** to save and reboot into Windows.

### 3. Physical Signaling and Mechanical Interference

If hardware ASPM is disabled and active bus traffic still results in a hard cap at Gen 2, the PCIe link training protocol is failing high-frequency eye-diagram tests and dropping back to 5 GT/s to prevent packet corruption.

- **PCIe Riser Cables**: If either card is mounted using a vertical bracket or riser extension, Gen 3 or low-quality riser cables will fail Gen 4 handshakes and fall back directly to Gen 2. Both cards must be slotted directly into the motherboard slots for baseline verification.

- **AM4 Cooler Mounting Torque**: The PCIe root complex resides entirely on the Ryzen CPU's I/O Die (IOD). Uneven or excessive mounting pressure from the CPU cooler compresses socket pins unevenly, degrading the high-frequency differential pairs responsible for Gen 4 signaling. Loosening the CPU cooler screws by a half-turn and retorquing them in an even, diagonal pattern frequently restores Gen 4 signal integrity across both CPU-attached slots.

> however, the 8gb card is displaying 2,8.. so that is a good sign, no?

That is a very good sign.

Seeing **`2, 8`** confirms the most critical and difficult physical hurdle of your setup: the **lane width (`8`)** is fully trained and electrically sound.

Here is what that reading tells us:

### 1. Physical Bifurcation is Working  (`x8`)

The `8` confirms that the motherboard’s PCIe lane switches, the AM4 socket pin contacts, and the physical slot solder traces are all functioning properly. If there were damaged socket pins, severe cooler warping, debris on the gold fingers, or a blown PCIe multiplexer chip, the slot would drop down to `x4`, `x2`, or `x1`. Maintaining all 8 lanes rules out physical lane drop failures.

### 2. Link Training is Responding (`Gen 2`)

Moving up from `Gen 1.1` (2.5 GT/s) to `Gen 2` (5.0 GT/s) proves that the PCIe PHY controller is actively scaling power states in response to your clock lock.

The reason it stops at Gen 2 instead of jumping straight to Gen 4 comes down to PCIe power management:

- **Gen 1 (2.5 GT/s):** Deep ASPM idle (power-saving state when the GPU core is parked).
- **Gen 2 (5.0 GT/s):** Intermediate performance state. Locking the GPU clocks forces the silicon awake, but because there is **no actual data moving across the PCIe bus**, the PCIe root complex stays in a low-power link state to prevent wasting energy.
- **Gen 4 (16.0 GT/s):** High-speed performance state. The root complex and GPU link controller will only negotiate up to 16 GT/s when sustained Direct Memory Access (DMA) transactions are actively saturating the bus, or if ASPM/PCIe native power management is explicitly disabled in the motherboard firmware.

### How to Trigger the Jump from `2, 8` to `4, 8`

To push the controller from Gen 2 up to its full Gen 4 speed:
1. **Push Real Data Across the Bus**: Run a memory copy payload (such as CUDA `bandwidthTest.exe --device=X --memory=pinned`) or an active compute workload (like an inference model or synthetic stress test). The moment host-to-device memory traffic spikes, the controller will automatically renegotiate the bus to Gen 4.
2. **Firmware ASPM Override (Optional)**: If you want the link locked at Gen 4 permanently regardless of bus load, disable **Native ASPM** and **PEG - ASPM** in the BIOS under **Advanced** -> **Platform Misc Configuration**.