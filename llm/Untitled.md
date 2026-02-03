  
!!! Exception during processing !!! 'AdmPureModule' object has no attribute 'dtype' Traceback (most recent call last): File "D:\design tools\ComfyUI_windows_portable\ComfyUI\execution.py", line 518, in execute output_data, output_ui, has_subgraph, has_pending_tasks = await get_output_data(prompt_id, unique_id, obj, input_data_all, execution_block_cb=execution_block_cb, pre_execute_cb=pre_execute_cb, v3_data=v3_data) ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ File "D:\design tools\ComfyUI_windows_portable\ComfyUI\execution.py", line 329, in get_output_data return_values = await _async_map_node_over_list(prompt_id, unique_id, obj, input_data_all, obj.FUNCTION, allow_interrupt=True, execution_block_cb=execution_block_cb, pre_execute_cb=pre_execute_cb, v3_data=v3_data) ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ File "D:\design tools\ComfyUI_windows_portable\ComfyUI\execution.py", line 303, in _async_map_node_over_list await process_inputs(input_dict, i) File "D:\design tools\ComfyUI_windows_portable\ComfyUI\execution.py", line 291, in process_inputs result = f(**inputs) ^^^^^^^^^^^ File "D:\design tools\ComfyUI_windows_portable\ComfyUI\custom_nodes\manual_unet_loader.py", line 175, in load_unet model = config.get_model(sd, "") ^^^^^^^^^^^^^^^^^^^^^^^^ File "D:\design tools\ComfyUI_windows_portable\ComfyUI\custom_nodes\manual_unet_loader.py", line 170, in get_model return comfy.model_base.BaseModel(self, device=device, unet_model=AdmPureModule) ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ File "D:\design tools\ComfyUI_windows_portable\ComfyUI\comfy\model_base.py", line 148, in __init__ logging.info("model weight dtype {}, manual cast: {}".format(self.get_dtype(), self.manual_cast_dtype)) ^^^^^^^^^^^^^^^^ File "D:\design tools\ComfyUI_windows_portable\ComfyUI\comfy\model_base.py", line 216, in get_dtype return self.diffusion_model.dtype ^^^^^^^^^^^^^^^^^^^^^^^^^^ File "D:\design tools\ComfyUI_windows_portable\python_embeded\Lib\site-packages\torch\nn\modules\module.py", line 1965, in __getattr__ raise AttributeError( AttributeError: 'AdmPureModule' object has no attribute 'dtype'. Did you mean: 'type'?

Thought for 1s

Edited

manual_unet_loader.py

+1-0

Thought for 1s

I've fixed the 

```
AttributeError: 'AdmPureModule' object has no attribute 'dtype'
```

 by adding the required 

```
dtype
```

 field to the module. ComfyUI's model base uses this to keep track of the model's precision.

Here is the updated project summary for your next session. It includes this latest fix and the shift to the **Diffusers-style** architecture.

---

# Project Handover: ADM Pixel-Space Diffusion (Updated)

### **Project Goal**

Load and run the 

**512x512_diffusion_comfy.safetensors** (unconditional pixel-space ADM) model within ComfyUI.

### **1. Model Architecture (Verified)**

The model uses a **Diffusers-style** naming convention (e.g., 

```
down_blocks[i].resnets[j]
```

).

- **Key Fact**: The model has **ZERO attention layers**. It is a pure CNN.
- **Structure**:
    - **Down**: 
        
        ```
        [3, 6, 6, 5]
        ```
        
         Resnets
    - **Mid**: 
        
        ```
        2
        ```
        
         Resnets
    - **Up**: 
        
        ```
        [6, 6, 6, 3]
        ```
        
         Resnets (matching skip-connections)
- **Input/Output**: 3-channel RGB in, 6-channel out (sliced to 3 internally).
- **Precision**: Must be **FP32** to avoid 
    
    ```
    NaN
    ```
    
     results.

### **2. Current Implementation (

manual_unet_loader.py)**

- **
    
    AdmPureModule**: Reconstructs the exact block-by-block structure found in your weight file. It handles skip-connections and forces 
    
    ```
    float32
    ```
    
     for stability.
- **
    
    ```
    Empty Pixel Latent
    ```
    
    **: Generates a 3-channel 512x512 tensor (No VAE used).
- **
    
    ```
    Pixel Latent to Image
    ```
    
    **: Extracts the image and applies **Auto-Range Normalization** to visualize results even if values are abnormal.

### **3. Fixes Applied**

- ✅ **Unified Loader**: Removed complex UI sliders to focus on the specific architecture of the 
    
    ```
    512...comfy.safetensors
    ```
    
     file.
- ✅ **Dtype Fix**: Added 
    
    ```
    self.dtype = torch.float32
    ```
    
     to the module to prevent ComfyUI startup crashes.
- ✅ **Stability Guards**: Added spatial resizing for skip-connections and 
    
    ```
    nan_to_num
    ```
    
     emergency recovery during sampling.

### **4. Instructions for Next Session**

- **Sampling**: Use **DDIM** or **UniPC** with 50+ steps. Unconditional models often fail to converge with simple Euler at low step counts.
- **Static/Noise**: If the output is still colorful static, the "Missing Keys" in the terminal will be the primary clue. Refer to 
    
    list_keys.py in your scripts folder for weight inspection.