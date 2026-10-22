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
*Pass criteria under lock/load:* Both RTX 5060 cards should report `pcie.link.gen.current: 4` and `pcie.link.width.current: 8`.

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

3. Click **Apply Changes** in the top right corner. The settings apply to the driver immediately without any Control Panel running.