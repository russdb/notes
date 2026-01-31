Yes, this is the best way to start. Because **Flux** is much more complex than older models, manually wiring the nodes (UNET + Dual CLIPs + VAE) is a pain for beginners.

Below is the complete **Flux Dev (FP8)** workflow. I have designed this specifically for your **8GB VRAM** limit by using the efficient "FP8" text encoders to prevent your system RAM from choking.

### Part 1: Download The Essential Files

Before loading the workflow, you need these 4 files. If you try to run the workflow without them, it will error out.

**1. The Brain (UNET)**

- **File:** `flux1-dev-fp8.safetensors` (approx 12GB)
    
- **Location:** `ComfyUI\models\unet\`
    
- **Download:** [HuggingFace - Kijai/flux-fp8](https://huggingface.co/Kijai/flux-fp8/tree/main) (Look for `flux1-dev-fp8.safetensors`)
    

**2. The Text Encoders (CLIPs)**

- **File A:** `t5xxl_fp8_e4m3fn.safetensors` (approx 4.9GB - _Crucial for 8GB cards_)
    
- **File B:** `clip_l.safetensors` (approx 246MB)
    
- **Location:** `ComfyUI\models\clip\`
    
- **Download:** [HuggingFace - comfyanonymous/flux_text_encoders](https://huggingface.co/comfyanonymous/flux_text_encoders/tree/main)
    

**3. The Translator (VAE)**

- **File:** `ae.safetensors` (approx 335MB)
    
- **Location:** `ComfyUI\models\vae\`
    
- **Download:** [HuggingFace - FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev/tree/main)
    

---

### Part 2: The Workflow (Copy & Paste)

I have generated the JSON code for you.

1. **Copy** the code block below.
    
2. **Paste** it into a standard text editor (Notepad).
    
3. **Save** the file as `flux_workflow.json` (make sure it's `.json` and not `.txt`).
    
4. **Drag and drop** that file directly into your ComfyUI window.
    

JSON

```
{
  "last_node_id": 9,
  "last_link_id": 14,
  "nodes": [
    {
      "id": 1,
      "type": "UNETLoader",
      "pos": [14, 137],
      "size": [315, 82],
      "flags": {},
      "order": 0,
      "mode": 0,
      "inputs": [],
      "outputs": [
        { "name": "MODEL", "type": "MODEL", "links": [1] }
      ],
      "properties": { "Node name for S&R": "UNETLoader" },
      "widgets_values": ["flux1-dev-fp8.safetensors", "fp8_e4m3fn"]
    },
    {
      "id": 2,
      "type": "DualCLIPLoader",
      "pos": [13, 335],
      "size": [315, 106],
      "flags": {},
      "order": 1,
      "mode": 0,
      "inputs": [],
      "outputs": [
        { "name": "CLIP", "type": "CLIP", "links": [2] }
      ],
      "properties": { "Node name for S&R": "DualCLIPLoader" },
      "widgets_values": ["clip_l.safetensors", "t5xxl_fp8_e4m3fn.safetensors", "flux", "default"]
    },
    {
      "id": 3,
      "type": "VAELoader",
      "pos": [15, 532],
      "size": [315, 58],
      "flags": {},
      "order": 2,
      "mode": 0,
      "inputs": [],
      "outputs": [
        { "name": "VAE", "type": "VAE", "links": [3] }
      ],
      "properties": { "Node name for S&R": "VAELoader" },
      "widgets_values": ["ae.safetensors"]
    },
    {
      "id": 4,
      "type": "EmptyLatentImage",
      "pos": [436, 442],
      "size": [315, 106],
      "flags": {},
      "order": 3,
      "mode": 0,
      "inputs": [],
      "outputs": [
        { "name": "LATENT", "type": "LATENT", "links": [4] }
      ],
      "properties": { "Node name for S&R": "EmptyLatentImage" },
      "widgets_values": [1024, 1024, 1]
    },
    {
      "id": 5,
      "type": "CLIPTextEncode",
      "pos": [433, 30],
      "size": [425, 180],
      "flags": {},
      "order": 4,
      "mode": 0,
      "inputs": [
        { "name": "clip", "type": "CLIP", "link": 2 }
      ],
      "outputs": [
        { "name": "CONDITIONING", "type": "CONDITIONING", "links": [5] }
      ],
      "properties": { "Node name for S&R": "CLIPTextEncode" },
      "widgets_values": ["A cinematic shot of a futuristic robot painting a canvas, 8k resolution, highly detailed, dramatic lighting"]
    },
    {
      "id": 6,
      "type": "CLIPTextEncode",
      "pos": [435, 240],
      "size": [425, 180],
      "flags": {},
      "order": 5,
      "mode": 0,
      "inputs": [
        { "name": "clip", "type": "CLIP", "link": 2 }
      ],
      "outputs": [
        { "name": "CONDITIONING", "type": "CONDITIONING", "links": [6] }
      ],
      "properties": { "Node name for S&R": "CLIPTextEncode" },
      "widgets_values": ["blur, distortion, low quality, ugly"]
    },
    {
      "id": 7,
      "type": "KSampler",
      "pos": [923, 151],
      "size": [315, 262],
      "flags": {},
      "order": 6,
      "mode": 0,
      "inputs": [
        { "name": "model", "type": "MODEL", "link": 1 },
        { "name": "positive", "type": "CONDITIONING", "link": 5 },
        { "name": "negative", "type": "CONDITIONING", "link": 6 },
        { "name": "latent_image", "type": "LATENT", "link": 4 }
      ],
      "outputs": [
        { "name": "LATENT", "type": "LATENT", "links": [7] }
      ],
      "properties": { "Node name for S&R": "KSampler" },
      "widgets_values": [123456789, "randomize", 20, 1.0, "euler", "simple", 1]
    },
    {
      "id": 8,
      "type": "VAEDecode",
      "pos": [1287, 152],
      "size": [210, 46],
      "flags": {},
      "order": 7,
      "mode": 0,
      "inputs": [
        { "name": "samples", "type": "LATENT", "link": 7 },
        { "name": "vae", "type": "VAE", "link": 3 }
      ],
      "outputs": [
        { "name": "IMAGE", "type": "IMAGE", "links": [8] }
      ],
      "properties": { "Node name for S&R": "VAEDecode" },
      "widgets_values": []
    },
    {
      "id": 9,
      "type": "SaveImage",
      "pos": [1533, 152],
      "size": [315, 270],
      "flags": {},
      "order": 8,
      "mode": 0,
      "inputs": [
        { "name": "images", "type": "IMAGE", "link": 8 }
      ],
      "outputs": [],
      "properties": { "Node name for S&R": "SaveImage" },
      "widgets_values": ["ComfyUI"]
    }
  ],
  "links": [
    [1, 1, 0, 7, 0, "MODEL"],
    [2, 2, 0, 5, 0, "CLIP"],
    [2, 2, 0, 6, 0, "CLIP"],
    [3, 3, 0, 8, 1, "VAE"],
    [4, 4, 0, 7, 3, "LATENT"],
    [5, 5, 0, 7, 1, "CONDITIONING"],
    [6, 6, 0, 7, 2, "CONDITIONING"],
    [7, 7, 0, 8, 0, "LATENT"],
    [8, 8, 0, 9, 0, "IMAGE"]
  ],
  "groups": [],
  "config": {},
  "extra": {},
  "version": 0.4
}
```

### Pro Tip for your RTX 5070 (8GB VRAM)

If you find the above workflow is slow (taking >45 seconds per image) or crashing, it is because the 12GB FP8 model is overflowing your 8GB VRAM and using your system RAM.

**The Fix: Switch to GGUF (The "Magic" Format)** GGUF models compress the 12GB file down to ~6GB with almost zero quality loss, allowing it to fit _entirely_ inside your 5070.

1. **Download:** `flux1-dev-Q4_0.gguf` (Search "Flux GGUF" on Civitai/HuggingFace).
    
2. **Install Node:** Open Manager -> Install Custom Nodes -> Search **"ComfyUI-GGUF"** -> Install.
    
3. **Swap Node:** In the workflow above, delete the `UNETLoader` node and replace it with `UnetLoaderGGUF`. Select your new GGUF file.
    

This will make your generations **2x faster**.