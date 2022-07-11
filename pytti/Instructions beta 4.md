`text_prompts:` Descriptions of scenes you want generated, separated by `||`. Each scene can contain multiple prompts, separated by `|`.

  

*Example:* `Winter sunrise | icy landscape || Winter day | snowy skyline || Winter sunset | chilly air || Winter night | clear sky` would go through several winter scenes.

  

**Advanced:** weight prompts with `description:weight`. Higher `weight` values will be prioritized by the optimizer, and negative `weight` values will remove the description from the image. The default weight is $1$.

  

*Example scene:* `blue sky:10|martian landscape|red sky:-1` would try to turn the martian sky blue.

  

**Advanced:** stop prompts once the image matches them sufficiently with `description:weight:stop`. `stop` should be between $0$ and $1$ for positive prompts, or between $-1$ and $0$ for negative prompts. Lower `stop` values will have more effect on the image (remember that $-1<-0.5<0$). A prompt with a negative `weight` will often go haywire without a stop.

  

*Example scene:* `Feathered dinosaurs|birds:1:0.87|scales:-1:-.9|text:-1:-.9` Would try to make feathered dinosaurs, lightly like birds, without scales or text, but without making 'anti-scales' or 'anti-text.'

  

**Advanced:** apply directional weights by using `weight_dir` for your `weight`. Valid `dir` values are:

  

* `u`: the top half of the image

* `d`: the bottom half of the image

* `l`: the left half of the image

* `r`: the right half of the image

  

*Example scene:* `Forest:3_l|Desert:3_r|sky:3_u|ground:3_d`

  

**Advanced:** change where the directional prompts begin and end with `weight_dir_cutoff`. `cutoff` should be between $0$ and $1$. The default `cutoff` value is 0.5, which puts the threshold at the center of the image. For vertical `dir` values (`u` or `d`) a `cutoff` of $0$ puts the threshold all the way at the top of the image, so `1_d_0` selects the whole image, while `1_u_0` selects nothing. Similarly, `1_d_1` selects nothing, and `1_u_1` selects the entire image. For horizontal `dir` values (`l` and `r`), a cutoff of $0$ is the left side the image and $1$ is the right.

  

*Example scene:* `blue sunset:4_u_0.1|purple sunset:4_u_0.2|red sunset:4_u_0.3|orange sunset:4_u_0.4|yellow sunset:4_u_0.5|green sea:4_d_0.5|sailboats:4_d_0.6|seagulls:4_d_0.1` would put `blue sunset` in only the top tenth of the image, but would put `seagulls` in the the bottom nine tenths, since they both have a `cutoff` of $0.1$, but `blue sunset` goes **u**p while `seagulls` goes **d**own from that `cutoff`.

  

**NEW Advanced:** *All* `weight`, `stop`, and `cutoff` values in prompts, init weights, and stabilization weights can be functions of $t$.

  

---

  

`prefix_style:` text prepended to the beginning of each scene.

  

*Example:* `Trending on Arstation|`

  

`suffix_style:` text appended to the end of each scene.

  

*Example:* ` by James Gurney`

  

`interpolation_steps:` number of steps to spend smoothly transitioning from the last scene at the start of each scene. $200$ is a good default. Set to $0$ to disable.

  

`steps_per_scene:` total number of steps to spend rendering each scene. Should be at least `interpolation_steps`. This will indirectly control the total length of an animation.

  

---

  

`direct_image_prompts:` paths or urls of images that you want your image to look like in a literal sense, along with `weight` and `stop` values, separated by `|`.

  

`latent_image_prompts:` paths or urls of images that you want your image to look like in a literal sense, as seen by the `image_model`, along with `weight` and `stop` values, separated by `|`. This works much better than `direct` when using `VQGAN` as the `image_model`.

  

`semantic_image_prompts:` paths or urls of images that you want your image to look like in a figurative sense, along with `weight` and `stop` values, separated by `|`. Directional `weight` values work too. Think of these as really detailed descriptions of the images.

  

---

  

`init_image:` path or url of start image. Works well for creating a central focus.

  

`init_mask:` path or url of a mask to control which parts of the `init_image` are left unchanged. Specifically, the `init_mask` is applied to the `direct` and `latent` `init_weight`.

  

`init_mask_inverted:` check this box to preserve the dark parts of `init_mask`, uncheck to preserve the light parts.

  

`direct_init_weight:` Defaults to $0$. Put a `weight` or a `weight:stop` here to add the init image as a direct image prompt with those parameters.

  

`latent_init_weight:` Defaults to $0$. Put a `weight` or a `weight:stop` here to add the init image as a latent image prompt with those parameters.

  

`semantic_init_weight:` Defaults to $0$. Put a `weight` or a `weight:stop` here to add the init image as a semantic image prompt with those parameters. Directional `weight` values work too.

  

---

  

`width`, `height:` image size. Set one of these $-1$ to derive it from the aspect ratio of the init image.

  

`pixel_size:` integer image scale factor. Makes the image bigger.

  

`smoothing_weight:` makes the image smoother. Defaults to $0$ (no smoothing). Can also be negative for that deep fried look.

  

`image_model:` select how your image will be represented.

  

`vqgan_model:` select your VQGAN version (only for `image_model: VQGAN`)

  

`random_initial_palette:` if checked, palettes will start out with random colors. Otherwise they will start out as grayscale. (only for `image_model: Limited Palette`)

  

`palette_size:` number of colors in each palette. (only for `image_model: Limited Palette`)

  

`palettes:` total number of palettes. The image will have `palette_size*palettes` colors total. (only for `image_model: Limited Palette`)

  

`gamma:` relative gamma value. Higher values make the image darker and higher contrast, lower values make the image lighter and lower contrast. (only for `image_model: Limited Palette`). $1$ is a good default.

  

`hdr_weight:` how strongly the optimizer will maintain the `gamma`. Set to $0$ to disable. (only for `image_model: Limited Palette`)

  

`show_palette:` check this box to see the palette each time the image is displayed. (only for `image_model: Limited Palette`)

  

---

  

`animation_mode:` select animation mode or disable animation.

  

`sampling_mode:` how pixels are sampled during animation. `nearest` will keep the image sharp, but may look bad. `bilinear` will smooth the image out, and `bicubic` is untested :)

  

`infill_mode:` select how new pixels should be filled if they come in from the edge.

* mirror: reflect image over boundary

* wrap: pull pixels from opposite side

* black: fill with black 

* smear: sample closest pixel in image

  

`pre_animation_steps:` number of steps to run before animation starts, to begin with a stable image. $250$ is a good default.

  

`steps_per_frame:` number of steps between each image move. $50$ is a good default.

  

`frames_per_second:` number of frames to render each second. Controls how $t$ is scaled.

  

`direct_stabilization_weight: ` keeps the current frame as a direct image prompt. For `Video Source` this will use the current frame of the video as a direct image prompt. For `2D` and `3D` this will use the shifted version of the previous frame.

  

`latent_stabilization_weight: ` keeps the current frame as a latent image prompt. For `Video Source` this will use the current frame of the video as a direct image prompt (NOTE: for `Limited Palette` and `Unlimited Palette` modes the resulting enode will slow down animation). For `2D` and `3D` this will use the shifted version of the previous frame, which won't slow down the palette modes.

  

`semantic_stabilization_weight: ` keeps the current frame as a semantic image prompt. For `Video Source` this will use the current frame of the video as a direct image prompt. For `2D` and `3D` this will use the shifted version of the previous frame.

  

`depth_stabilization_weight: ` keeps the depth model output somewhat consistent at a *VERY* steep performance cost. For `Video Source` this will use the current frame of the video as a direct image prompt. For `2D` and `3D` this will use the shifted version of the previous frame.

  

`edge_stabilization_weight: ` keeps the images contours somewhat consistent at very little performance cost. For `Video Source` this will use the current frame of the video as a direct image prompt. For `2D` and `3D` this will use the shifted version of the previous frame.

  

`flow_stabilization_weight: ` used for `animation_mode: 3D` and `Video Source` to prevent flickering. Comes with a slight performance cost for `Video Source`, and a great one for `3D`, due to implementation differences.

  

---

`video_path: ` path to mp4 file for `Video Source`

  

`reencode_each_frame: ` check this box to use each video frame as an `init_image` instead of warping each output frame into the init for the next. Cuts will still be detected and trigger a reencode.

  

`flow_direct_strength: ` For `Video Source` mode, there are two ways to prevent flickering. The direct way is to keep the output pixels as close as possible to their warped versions. This works well for pixel modes, but makes VQGAN blurry. The strength is relative to `flow_stabilization_weight`.

  

`flow_latent_strength: ` For `Video Source` mode, there are two ways to prevent flickering. The latent way is to keep the input latent parameters as close as possible to their warped versions. This works well for all image models. The strength is relative to `flow_stabilization_weight`.

  

`flow_long_term_samples: ` Sample multiple frames into the past for consistent interpolation even with disocclusion, as described by [Manuel Ruder, Alexey Dosovitskiy, and Thomas Brox (2016)](https://arxiv.org/abs/1604.08610). Each sample is twice as far back in the past as the last, so the earliest sampled frame is $2^{\text{long_term_flow_samples}}$ frames in the past. Set to $0$ to disable.

  

---

  

`translate_x:` horizontal image motion as a function of time $t$ in seconds.

  

`translate_y:` vertical image motion as a function of time $t$ in seconds.

  

`translate_z_3d:` forward image motion as a function of time $t$ in seconds. (only for `animation_mode:3D`)

  

`rotate_3d:` image rotation as a quaternion $\left[r,x,y,z\right]$ as a function of time $t$ in seconds. (only for `animation_mode:3D`)

  

`rotate_2d:` image rotation in degrees as a function of time $t$ in seconds. (only for `animation_mode:2D`)

  

`zoom_x_2d:` horizontal image zoom as a function of time $t$ in seconds. (only for `animation_mode:2D`)

  

`zoom_y_2d:` vertical image zoom as a function of time $t$ in seconds. (only for `animation_mode:2D`)

  

`lock_camera:` check this box to prevent all scrolling or drifting. Makes for more stable 3D rotations. (only for `animation_mode:3D`)

  

`field_of_view:` vertical field of view in degrees. (only for `animation_mode:3D`)

  

`near_plane:` closest depth distance in pixels. (only for `animation_mode:3D`)

  

`far_plane:` farthest depth distance in pixels. (only for `animation_mode:3D`)

  

---

  

`file_namespace:` output directory name.

  

`allow_overwrite:` check to overwrite existing files in `file_namespace`.

  

`display_every:` how many steps between each time the image is displayed in the notebook.

  

`display_scale:` image display scale in notebook. $1$ will show the image at full size. Does not affect saved images.

  

`save_every:` how many steps between each time the image is saved. Set to `steps_per_frame` for consistent animation.

  

`backups:` number of backups to keep (only the oldest backups are deleted). Large images make very large backups, so be warned. Set to `all` to save all backups. These are used for the `flow_long_term_samples` so be sure that this is at least $2^{\text{flow_long_term_samples}}+1$ for `Video Source` mode.

  

`show_graphs:` check this to see graphs of the loss values each time the image is displayed. Disable this for local runtimes.

  

---

  

`ViTB32, ViTB16, RN50, RN50x4:` select your CLIP models. These take a lot of VRAM.

  

`learning_rate:` how quickly the image changes.

  

`seed:` pseudorandom seed

  

---

  

`cutouts:` number of cutouts. Reduce this to use less VRAM at the cost of quality and speed.

  

`cutout_detail:` should be positive. Large values shrink cutouts, making the image more detailed, small values expand the cutouts, making it more coherent. $1$ is a good default.

  

`cutout_border:` should be between $0$ and $1$. Allows cutouts to poke out over the edges of the image by this fraction of the image size, allowing better detail around the edges of the image. Set to $0$ to disable. $0.25$ is a good default.

  

`border_mode:` how to fill cutouts that stick out over the edge of the image. Match with `infill_mode` for consistent infill.

  

* clamp: move cutouts back onto image

* mirror: reflect image over boundary

* wrap: pull pixels from opposite side

* black: fill with black 

* smear: sample closest pixel in image