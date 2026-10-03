+++
title = "The Sims 2 on Apple Silicon"
description = "About my blog"
date = "2026-04-11"
updated = "2026-08-14"
draft = false

[taxonomies]
categories = ["Guides"]
tags = ["guide","shenanigans","sims","ts2"]

[extra]
lang = "en"
toc = true
comment = false

+++
# Introduction
Since I got my M4 Mac mini I wanted to run Sims 2 UC on it. Tried a lot of things, different WINE forks or front-ends, Windows 11 and Linux VMs on VMware Fusion... Most of them failed or the game ran poorly, but eventually I did it.

This tutorial will show you how to run The Sims 2 on Apple Silicon using WINE. Some steps presented here were made with Bourbon/Whisky in mind but the tutorial also works with Crossover!

## NOTICE
If you use a lot of mods, and/or play with big hoods (big families, generation gameplay, etc.), this guide will not work for you. The reason is file descriptor limit that UNIX-like systems like MacOS or Linux use. Technically speaking file descriptor limit tells the system how many files can be loaded, it technically can be risen (MacOS on my Mac mini returns that the hardware limit [the actual maximum] is unlimited) BUT it MIGHT cause some issues, like making your system unstable. If you will be rising the file descriptor limit YOU ARE DOING IT AT YOUR OWN RISK. Be aware that with better hardware development and system updates the file descriptor limit will grow, meaning one day it might not be an issue unless you really force it.

## Update 14th August 2026
On frankea's Whisky version 3.6.1, overrides in winecfg section clear when running the game, so instead use the option inside of Bottle configuration in Whisky. If you will get "Direct3D returned an error: D3DERR_INVALIDCALL! The application will now termiate" error during the loading screen try removing the config folder from the game's folder in documents. You can also enable performance mode in Bottle configuration.

# Installation
## 1. Get the game's files on your Mac.
Do it however you want, if you are a Legacy Edition player then I can't help you, but I am guessing you would just install the game over Windows version of Steam or EA App running on WINE.

## 2. Install your preferred WINE front-end.
I've used [Bourbon](https://github.com/leonewt0n/Bourbon) because Whisky is no longer maintained. Well, Bourbon isn't either BUT it uses a newer version of WINE, and has Liquid Glass UI. Most likely there might be a new Whisky/Bourbon fork at the time of you following this tutorial. (Now I recommend you use [Whisky fork by frankea]((https://github.com/frankea/Whisky), the game runs better than when I made this tutorial on Bourbon, also on it you can launch the game withh DXVK, but well some graphics are broken, one of them is that the loaded lot and everything on it is invisible)

## 3. Create a new Bottle and install the game.
Each WINE front-end will be different, some might not even have bottles, just be sure to use a separate Bottle/Prefix for The Sims 2, as its fixes might break other games. Make sure DXVK is disabled, if you get a dropdown list for Graphics, select Wine, WineD3, or Auto.

## 4. Patch WINE.
DXVK doesn't work as of time of making this tutorial, and clean WINED3D does not either, so we will need to patch WINED3D. Download newest release of TS2D3DFIX from [ttps://github.com/erfan2255/TS2D3DFIX/releases/](https://github.com/erfan2255/TS2D3DFIX/releases/) . Extract the downloaded .zip and run the .exe inside of the Bottle/Prefix you installed the game in. When prompted, select `WineD3D 3.18 - Native Patches` and hit Next. When the installation finishes, open WINE configuration utility (`winecfg`) and head to the Libraries tab. In the text box for new library overrides enter the following, while pressing Enter/Return after each one:

`d3d10`

`d3d10_1`

`d3d10core`

`d3d11`

`d3d8`

`d3d9`

`ddraw`

`dxgi`

`wined3d`

When entering `ddraw` and `wined3d` you might get prompted that overwriting these files might be risky, just press Yes to continue. Make sure that all of the rules that were entered are displayed as (Native, Built-in); if they aren't, change each one using the EDIT button.

## 6. Fix Family Portraits
Launch TS2D3DFIX.exe again. Now select "Fix Corrupted Family Thumbnails" and hit next. When prompted change `C:\users\xdroid\My Documents\EA Games\The Sims 2\Downloads` to `C:\users\[your mac username]\Documents\EA Games\The Sims 2\Downloads`. You can check `[your mac username]` by opening finder then from Menu bar choose Go > Go to Folder, then enter /Users , the folder with a house icon is your home folder, and its name is `[your mac username]`.

## 7. Registry fixes
Open Registry Editor `regedit.exe`. From menu bar select Registry > Import from file. Now navigate where you have TS2D3DFIX files, and select "Enable Performance (csmt-on).reg" and hit Open. You can close Registry Editor.

## 8. Install Graphics Rules Maker
Download Graphics Rules Maker from [https://www.simsnetwork.com/tools/graphics-rules-maker](https://www.simsnetwork.com/tools/graphics-rules-maker), and install it in the Bottle/Prefix in which you installed the game, then run it. From the game selection dropdown list choose The Sims 2 and press Auto-detect. UNCHECK `Disable Sim Shadows` - the game can render the Sim shadows properly so there is no need to disable them and install a Sim shadow fixing mod. Press Save Files… and if prompted about adding your GPU, you can select anything as the game will detect an NVIDIA GPU, not your Mac's GPU.

## 9. Link your Documents folder to the Bottle/Prefix (optional)
Open WINE configuration utility (`winecfg`). Head to Desktop Integration. Under Directories, select Documents, then hit the checkbox next to "Linked to:", now select your Documents folder on macOS, and press OK. 

## 10. Test-run the game!
Launch the game, then after you get to the Main Menu close it. Now go to `Documents/EA GAMES/The Sims 2/Logs`, open `[MAC_NAME]-config-log.txt` and check if the game detects the graphics card in the Database. If not, add it to `Video Cards.sgr`. I won't be explaining here how to do it, there is a bunch of tutorials online you can search for to help you. One thing, Graphics Rules Maker won't work as it detects your Mac's GPU, not the WineD3D GPU.

## 11. Launch the game!
Launch the game, and load a hood. Then set all the graphics settings to the highest possible (take a look at the screenshots), you can always lower them if your game lags.
![Screenshot of the settings no. 1](https://thumbs2.modthesims2.com/img/1/0/3/4/1/4/6/6/MTS_Micro856-2312127-Zrzutekranu2026-04-11o15.57.23.png)
![Screenshot of the settings no. 2](https://thumbs2.modthesims2.com/img/1/0/3/4/1/4/6/6/MTS_Micro856-2312129-Zrzutekranu2026-04-11o15.57.40.png)
![Screenshot of the settings no. 3](https://thumbs2.modthesims2.com/img/1/0/3/4/1/4/6/6/MTS_Micro856-2312128-Zrzutekranu2026-04-11o16.01.39.png)

## 12. You are DONE!
The game is playable now, be aware that it might slow down while your computer is also compiling TS2's shaders.

# Tips
- When the game launches, move it to a separate Virtual Desktop from Mission Control, this is just to copy the MacOS behavior of putting Fullscreen apps in separate Desktops.

# Bugs
- Cheats console does not always render properly, sometimes you might not see what you are typing, because the Cheats console opens as a small rectangle that fits 0 text

![Incorrectly rendering Cheats console](https://thumbs2.modthesims2.com/img/1/0/3/4/1/4/6/6/MTS_Micro856-2312130-cheatsconsole.png)

![Correctly rendering Cheats console (Sim shadows invisible, as I forgot to disable Disable Sim Shadows)](https://thumbs2.modthesims2.com/img/1/0/3/4/1/4/6/6/MTS_Micro856-2312131-cheatsconsole-proper.png)

- When Cmd-Tabbing or sometimes when loading a Lot, the screen can be mostly black, expect for UI and few Objects, just move your camera around to fix it.

![Cmd-Tab graphical bug](https://thumbs2.modthesims2.com/img/1/0/3/4/1/4/6/6/MTS_Micro856-2312133-image.png)

- When Cmd-Tabbing, the game's window might show a while and disappear, just click on the desktop then right click Sims 2 icon on the dock, and select The Sims™ 2 (Name of the latest DLC)

- When switching audio devices, your game might loose sound. You will need to relaunch it.

# Future-proofing
Because [Apple is discontinuing Rosetta](https://support.apple.com/en-us/102527?cid=mc-ols-rosetta-article_102527-macos_finder-52526201), the future of this way of running TS2 on Apple Silicon is unclear. We might get open-source emulators like FEX or Box64 on Mac, or maybe a built in translation layer/emulator for x86(_64) in wine. If VMware improves DirectX support (so that [this](https://www.reddit.com/r/sims2help/comments/17toigr/comment/k9f5x1j/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button) does not happen), or/and adds Vulkan (for running the game on DXVK without software rendering) support in the future, a better free alternative to running the game on Parallels will be VMware Fusion. We will see what the future brings.

# Some screenshots

![Screenshot no. 1](https://thumbs2.modthesims2.com/img/1/0/3/4/1/4/6/6/MTS_Micro856-2312134-Zrzutekranu2026-04-11o12.40.40.png)
![Screenshot no. 2](https://thumbs2.modthesims2.com/img/1/0/3/4/1/4/6/6/MTS_Micro856-2312135-Zrzutekranu2026-04-11o16.10.22.png)
![Screenshot no. 3](https://thumbs2.modthesims2.com/img/1/0/3/4/1/4/6/6/MTS_Micro856-2312132-Zrzutekranu2026-04-11o16.11.31.png)
