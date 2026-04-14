[![Made in Ukraine](https://img.shields.io/badge/made_in-ukraine-ffd700.svg?labelColor=0057b7)](https://stand-with-ukraine.pp.ua)
[![Stand With Ukraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/badges/StandWithUkraine.svg)](https://stand-with-ukraine.pp.ua)

# My Setup For ComfyUI + Live Portrait Playground

#StandWithUkraine 💙💛
----

#RussiaInvadedUkraine on 24 of February 2022, at 5.00 AM the armed forces of the Russian Federation  attacked Ukraine. Please, Stand with Ukraine, stay tuned for updates on Ukraine’s official sources and channels in English and support Ukraine in its fight for freedom and democracy in Europe.

- 💵 [**Sternenko Community**](https://www.sternenkofund.org/en) — foundation is established to continuously provide Ukrainian Defense Forces with drones, primarily of the FPV type, as well as to promote the development of unmanned technologies.
- 💵 [**Come Back Alive**](https://savelife.in.ua/en/donate-en/) — funds used to buy equipment for frontline soldiers as well as territorial defense units.
- 💵 [**Ukrainian Red Cross**](https://redcross.org.ua/en/donate/) — provides humanitarian relief to Ukrainians affected by the war.

[![Stand With Ukraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/banner2-direct.svg)](https://stand-with-ukraine.pp.ua)

## Get Started (MacBook Air M1)

```shell
python3.12 -m venv .venv && source .venv/bin/activate
pip install --requirement requirements-cpu.txt
python3 ComfyUI.Runtime/main.py --listen 0.0.0.0 --base-directory ComfyUI.Data/
```

## Get Started (Gentoo + Nvidia GTX 1060 6GB)

```shell
python3.12 -m venv .venv && source .venv/bin/activate
pip install --requirement requirements-gpu.txt
python3 ComfyUI.Runtime/main.py --listen 0.0.0.0 --base-directory ComfyUI.Data/
```

## Overview

This setup is specifically tailored for the **[Live Portrait](https://liveportrait.github.io)** playground. It leverages Git submodules to lock original source code to specific commits and provides a curated `requirements.txt` with strictly pinned versions. The goal is to ensure **long-term reproducibility**, allowing the environment to be rebuilt reliably regardless of future updates to external libraries.

### Solving Dependency Management

A major challenge in the ComfyUI ecosystem is the lack of strict versioning in custom nodes. Most `requirements.txt` files do not pin package versions, frequently leading to "dependency hell" when new, breaking updates (such as the migration to **NumPy 2.x**) are released.

This repository addresses these issues by:

- **Version Pinning:** Every critical package is locked to a tested, compatible version.
- **Snapshot Consistency:** Using submodules to prevent breaking changes from upstream repository updates.
- **Streamlined Deployment:** Providing a stable foundation that eliminates the need for manual troubleshooting during setup.

## Developer Notes

### Sub-tree: `ComfyUI.Data/custom_nodes`

#### Initialize

```shell
git subtree add --prefix ComfyUI.Runtime origin "Comfy-Org.ComfyUI#master" --squash
git subtree add --prefix ComfyUI.Data/custom_nodes/kijai.ComfyUI-LivePortraitKJ origin "kijai.ComfyUI-LivePortraitKJ#main" --squash
git subtree add --prefix ComfyUI.Data/custom_nodes/kijai.ComfyUI-KJNodes origin "kijai.ComfyUI-KJNodes#main" --squash
git subtree add --prefix ComfyUI.Data/custom_nodes/pythongosssss.ComfyUI-Custom-Scripts origin "pythongosssss.ComfyUI-Custom-Scripts#main" --squash
git subtree add --prefix ComfyUI.Data/custom_nodes/cubiq.ComfyUI_Essentials origin "cubiq.ComfyUI_Essentials#main" --squash
git subtree add --prefix ComfyUI.Data/custom_nodes/Kosinkadink.ComfyUI-VideoHelperSuite origin "Kosinkadink.ComfyUI-VideoHelperSuite#main" --squash
```

#### Upgrade

```shell
git subtree pull --prefix ComfyUI.Runtime origin "Comfy-Org.ComfyUI#master" --squash
git subtree pull --prefix ComfyUI.Data/custom_nodes/kijai.ComfyUI-LivePortraitKJ origin "kijai.ComfyUI-LivePortraitKJ#main" --squash
git subtree pull --prefix ComfyUI.Data/custom_nodes/kijai.ComfyUI-KJNodes origin "kijai.ComfyUI-KJNodes#main" --squash
git subtree pull --prefix ComfyUI.Data/custom_nodes/pythongosssss.ComfyUI-Custom-Scripts origin "pythongosssss.ComfyUI-Custom-Scripts#main" --squash
git subtree pull --prefix ComfyUI.Data/custom_nodes/cubiq.ComfyUI_Essentials origin "cubiq.ComfyUI_Essentials#main" --squash
git subtree pull --prefix ComfyUI.Data/custom_nodes/Kosinkadink.ComfyUI-VideoHelperSuite origin "Kosinkadink.ComfyUI-VideoHelperSuite#main" --squash
```
