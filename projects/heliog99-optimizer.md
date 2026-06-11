---
title: Optimizer Helio-G99
description: Hard optimizer for Helio-G99 Arm64 Processor
type: project
layout: page
---

The [AI avatar companion](./aoi-ai-avatar-companion.md) currently heavy-rely on CPU and its optimizer for processing complex task. As per-current day it use 4 threads for processing the ``Qwen3 0.6B`` which still heavy on low-device like mine. The ideal state of processing that model has *3GB* of free RAM + higher CPU bench with *Vulkan* support. Better if the phone support *NPU* architecture. 


The model itself took 500MB + 160MB of STT-TTS model. Those just early implementation of the model without RAG and Agentic capability. To be honest, I think get a new brand phone is way easier than make everything over-engineered. Since at present day I still unemployeed and my balance is too painfull to see, this is the most realistic approach. Wish me luck guys, pls XD.


Due to all those restriction, I made the Helio-G99 hard optimizer. This optimizer push CPU-GPU, thread, UI, and removal bloatware to their peak. That resulting able play Genshin Impact with Highest graphic at 60fps and Honor of Kings with stable 60fps at Ultra graphic setting. Notably Genshin still need more research about their rendering process. This can happened after force CPU to 200%, GPU to 200%, Vulkan backend optimizer, and disable all Brand anoying bootloader. To be honst, what percentage of people actually use tool like XOS Folax? I never activate, what about you?


Since boost the CPU too highest state is not recommended for long period of time, the optimizer has two profiles and cleaner feature. The balance profile for normal state yet still able to use Vulkan backend to process rendering. This mode just like normal state, like literally. The beast one is performance/gaming mode. This mode, as I mentioned last paragraph, were hardware+OS specific optimization. All bloatware from XOS temporarily disable via ADB (which explained below section) and yes, temporarily, all state remain normal when phone restarted.


Repository [Optimizer Helio-G99](https://github.com/antinormies/optimizer-helio-g99-malig57) is an open-source, ready to use, ready to fork, or anything ready as a public repo. The future of his repo absolutely at the community hand. My reason same as my LinkedIn bio, to benefit more to more other people and tech should be help those who lack in resources. When you have poor device and really want to play heavy game, this repo might help you bro.


---

**Nerd-Technical-Approach**



``All state remain normal after phone restarted`` is a basic principal to this project. With no-root, I make sure to keep everything stay safe as its original state. The optimization area here is only **changing** the current configuration to **break** standard limitation. You can use CLI tools or repo-released android application to do your action. I recommend to use CLI if you connect to ADB with PC. If you prefer use the app, you need install [Shizuku](https://shizuku.rikka.app/) app and activate it which need extra step but more convenient for daily use. 


**Modules**

Modules mean the reinitialize-value area of phone that significantly impact in device performance. Those are **cpu.sh**, **gpu.sh**, **debloat.sh**, **display.sh**, and **memory.sh**. Each module **only** do their specific part.

Calling optimizer via CLI can be done by:

**Linux**

```shell
# define adb = path to your ADB 
export ADB=your_adb_path

# mode options are [balanced, performance]
sh cli/optimize.sh {mode} 

# preview/temporary changes use flag
--dry-run

# clear all optimization
sh 

```

**Windows**

```shell
# define adb = path to adb
$env:ADB=your_adb_path

# mode options are [balanced, performance] with optional --dry-run flag
sh cli/optimize.sh balanced --dry-run

```

More detailed about the execution at [cli/readme.md](https://github.com/antinormies/optimizer-helio-g99-malig57/blob/5a00154fbd00b8fc4703576e1e63210f59945a77/cli/README.md).


Process optimization is not merely direct execution for specific part. It need deep analyze first about the device. I use Infinix Note 40 as main device for all process to built this app. All analize process from start to end under ``docs/*`` and comprehensive test result at ``test`` folder. 

It seems I just rewrite things that already available, boring. I want to show you the best part of it- Vulkan backend custom performance. Mostly the mobile device not directly use Vulkan backend for some reason I didn't know yet. But it is real, my game default optimizer, XArena, only show <60% of GPU use even when I need more for rendering higher graphic. The first approach the app just configure threads, cpu max, memory allocation and strictly background process. The result still at the same state, even worse because force rendering all in GPU makes the game freezing. Now the config set both CPU and GPU allocation and give best rendering at Honor of Kings Global game. Then when it goes to Genshin Impact can render at high setting but not highest. This when Vulkan backend integration needs via Native C++ JNI bridging.

Vulkan here used as GPU warming up to trigger the game engine to able use Vulkan and its extension comprehensively. This way hard reinitialized GPU processing to use Vulkan. The process started from device information retrieval then write custom configuration to the init command. The GPU reinitialize itself with new Vulkan config. Read [app/readme.md](https://github.com/antinormies/optimizer-helio-g99-malig57/blob/5a00154fbd00b8fc4703576e1e63210f59945a77/app/README.md) for more detailed information.

This project still under construction and not even release the first version yet. The current release app at GitHub meant to early access as pre-release to gain community to join. Since I still beginner at microcontroller architecture and possible to make much mistake, please let me know more information to make this repository better by email me at [dani.zakaria@proton.me](mailto://dani.zakaria@proton.me). 

Work hard, gaming hard. Thank you!

Dani Zakaria.
