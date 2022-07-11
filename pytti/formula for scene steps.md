[[toc links]] 

#colab #googlecolab #art 

`steps_per_scene = T * frames_per_second * steps_per_frame`

working on skipping steps in scene creation to help speed it up

`frame_n = min((i - params.pre_animation_steps)*params.frame_stride//params.steps_per_frame, len(video_frames) - 1) next_frame_n = min(frame_n + params.frame_stride, len(video_frames) - 1) next_step_pil = Image.fromarray(video_frames.get_data(next_frame_n)).convert('RGB').resize(img.image_shape, Image.LANCZOS) for j, optical_flow in enumerate(optical_flows): old_frame_n = frame_n - (2**j + 1)*params.frame_stride`