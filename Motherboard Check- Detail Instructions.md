1. Open **PowerShell** or **Command Prompt** as Administrator.
2. Query the active PCIe link generation and width for both cards:
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

