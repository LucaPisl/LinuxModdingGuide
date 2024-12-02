# **How to install mods for Steam games on Linux using Vortex Mod Manager and SteamTinkerLaunch**

This guide assumes you already have a functional Steam installation with **Steam Play** enabled (for Proton compatibility). We'll be using **[Steam Tinker Launch (STL)](https://github.com/sonic2kk/steamtinkerlaunch)** to install and integrate [**Vortex Mod Manager**](https://www.nexusmods.com/about/vortex/), which will handle mod management. The most important thing is that I'll cover basically everything, including the symbolic link configurations required to ensure everything works seamlessly-ish.

You can follow this guide with *almost* **0 terminal usage* and very little Linux knowledge**. You just need to be patient, read everything and to think everything through.

> We will need to install some dependencies, but you just need to paste and press enter several times.

---

## **Step 1: Installing Steam Tinker Launch**

### **Method 1: Using ProtonUp-Qt (Recommended)**

The easiest way to install Steam Tinker Launch is through **ProtonUp-Qt**, a GUI tool that simplifies managing compatibility layers like Proton and STL.

1. **Install ProtonUp-Qt**:

Use your distribution’s package manager or Flatpak:

```bash
flatpak install flathub net.davidotek.pupgui2
```

2. **Add Steam Tinker Launch**:
- Open **ProtonUp-Qt**.

- Click **Add Version** and select **Steam Tinker Launch** from the list.

- Choose the desired version and install it.

> **Note :** While this installs STL easily, it does not handle dependencies, which you must install separately.

To install STL dependencies, see https://github.com/sonic2kk/steamtinkerlaunch/wiki/Installation#hard-dependencies

**Commands:**

**Debian/Ubuntu:**

```
sudo apt install awk bash git make procps-ng unzip wget xdotool xorg-xprop xorg-xrandr vim xorg-xwininfo yad
```

**Arch Linux:**

```
sudo pacman -S --needed awk bash git make procps-ng unzip wget xdotool xorg-xprop xorg-xrandr vim xorg-xwininfo yad
```

**Fedora/Nobara:**

```
sudo dnf install awk bash git make procps-ng unzip wget xdotool xorg-xprop xorg-xrandr vim xorg-xwininfo yad
```

---

> **Note :** It is also possible to install STL using the package manager on some distros, like ArchLinux. **THIS IS NOT RECOMMENDED!** If you do, please consult the AUR, or the equivalent for your distro, as you might need to run some commands after installation.

---

## **Step 2: Initializing Steam Tinker Launch**

**You will need to run the game with your chosen Proton Version at least once.**

I recommend Proton-GE (9.0+, preferably latest) or the unmodified Proton, provided by Valve. 

I assume that there are people here that are using Proton-GE, that know how to download, install and manage Proton versions. That being said, I want this guide to be as simple as possible and 100% noob friendly. You can use Proton-GE in this guide, just skip to the section **Initializing STL** and follow the rest of the steps.

For the purpose of what I said above, I will be explaining how to download and use Valve's unmodified Proton. 

There are two ways of doing this. I do not recommend the second one.

#### Method 1:

1. Open Steam and right-click on a chosen game in your Library.

> **Note :** I recommend doing this on a freshly-installed game that you did not run with another Proton version. We just need to do this to make sure that we downloaded Proton, so you can just download a small game, something like Brawlhalla. We'll just open it and close it.

2. Select **Properties** > **Compatibility**.

3. Check **Force the use of a specific Steam Play compatibility tool** and select **Proton-9.0-3** (or whatever the latest version is, I have not tried experimental).

4. Launch the game.

5. You might have to wait for the Proton version to be downloaded.
- It might get stuck on **Downloading... 0%**. If that happens, press the big blue **Stop** button, and press Play again.

- You might get a pop-up regarding the updating of the wine prefix.
6. The game should now open and work. If it does not, you might need to uninstall the game and [nuke the prefix](https://www.reddit.com/r/linux_gaming/comments/wzztwq/comment/im5adn2/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button).

7. Close the game and restart Steam.

#### Method 2 (not recommended):

This method can only be done after configuring STL. Follow the guide regarding configuring, then jump back here.

In the STL Main Menu:

- Click on **Download custom Proton**.

- You will get a pop-up asking you which version to download.

- Open this link in your browser: https://github.com/ValveSoftware/Proton/releases

- Find the latest release (right now Proton 9.0-3) and scroll down until you see **Assets**

- Right click on **Source Code (tar.gz)** and select **Copy Link** [Picture](https://imgur.com/3cZ1WBo)

- Paste the link inside the pop-up from STL, and press **OK** [Picture](https://imgur.com/PhF2agX)

### **Initializing STL:**

1. **Enable STL for Your Game:**
- Open Steam and right-click on the game in your Library.

- Select **Properties** > **Compatibility**.

- Check **Force the use of a specific Steam Play compatibility tool** and select **Steam Tinker Launch**.
2. **Launch the Game with STL:**

**When starting the game with STL, the STL interface/overlay will launch, which will hide itself after 2 seconds, unless you press the Main Menu button.** [Picture](https://user-images.githubusercontent.com/7917345/231898092-86a0441e-c82e-4ec1-aff1-15de236fbf56.png)

- Start the game

- When you see the STL pop-up, quickly press **Main Menu**

- You are now in the STL Main Menu interface. Press **Game Menu**, it's in the lower half of the interface

- Scroll down to **Proton Version** and make sure the Proton Version is the one you configured, change it if needed (in our guide, Proton 9.0-3)

- Click **Save and Play**
  
  - Optional: You can also adjust other settings here, such as launch arguments, using gamescope, etc.

- The game should launch and work properly. Close it.

---

## **Step 3: Initializing Vortex and Managing the Quirks of STL and Vortex (the beefy part)**

In this section, I'll address the actual hard part of the guide, that covers stuff such as symbolic links and configuration adjustments, necessary for proper integration between Steam Tinker Launch and Vortex.

1. Open the game you configured STL for

2. Open the STL **Main Menu**

3. Click on the **Vortex** button

4. Click on **Download**. A pop-up will open briefly and it will download Vortex, you don't have to do anything, it will close itself.

5. Now, click on **Install**

6. You will get a pop-up asking what Proton Version to use for the installation

7. **Select the proton version we installed above, the unmodified one** (in our case, Proton 9.0-3)

8. Click **OK/Install**

9. The installation process should start. It might take a while
   
   - If you get a pop-up from .Net, just press OK/Next/Install
   
   - If you get an error pop-up from Vortex, [like this](https://imgur.com/1UZzv8D), just click **Ignore**

10. At this point, if you did everything well, the *Installing* pop-up should close, and Vortex should start
    
    - If Vortex does not start, manually start it from the STL Vortex window by pressing **Start**

11. You might get some pop-ups or notifications in the bottom right saying that Vortex needs to apply some fixes. Allow Vortex to fix itself and then to restart itself.

At this point we have a working Vortex installation. The problem is that *you can't actually mod anything yet.* STL tries to make modding as seamless as possible, but we still actually need to do some stuff ourselves. From this point, we will assume we're trying to mod Palworld, to make the guide simpler. The steps are identical for any game that you can mod using Vortex.

> **THERE WILL BE SOME COMMANDS BELOW. IF YOU NEED TO USE THEM, REPLACE <user> WITH YOUR PC USERNAME**

1. Create a folder in your /home/user/ directory called "Links"
   
   - We will be using this folder for symlinks, that Vortex will use to mod games
   
   - DO NOT DELETE IT!

2. Now, go to Steam, right click **Palworld** in the Library menu and click **Manage > Browse local files**

3. This will open your file manager in the location where you have the Palworld files, ex: /home/user/.local/share/Steam/steamapps/common/Palworld/
   
   - You will need to note this path, as we will need to create some symlinks
   
   - Some file managers, such as KDE's Dolphin, allow you to drag and drop for symlinking, which I highly recommend

4. Here, create a folder called `Vortex-staging-mods`

5. Now we will link the Palworld directory inside of ~/Links:
   
   - Using Dolphin (you can use other file managers, such as Nautilus; search on the Internet how to create symlinks in that file manager):
     
     - Drag the **Palworld** folder (from /home/user/.local/share/Steam/steamapps/common/, in our example) inside of **~/Links**
     
     - You will get a pop-up, click on **Link Here**
   
   - Using the terminal (I don't recommend it, but it is the universal method)
     
     - `ln -s /home/user/.local/share/Steam/steamapps/common/Palworld/ ~/Links/`

6. Now go back to Vortex (or open it again if you closed it, from **STL Main Menu > Vortex > Start**)

7. You will get a pop-up in the top-right *Notifications* section, saying you need to apply some fixes for Vortex. Press **[Fix](https://imgur.com/ReLJPCz)** 

8. A window will pop up saying you need to login. Press **Login**   [Picture](https://imgur.com/bn48JFo)

9. This will open a window in your browser (if it does not, you can manually copy the link), where you will need to login into your Nexus Mods account
   
   * Your browser might say it blocked a pop-up. You **must** allow it.

10. After you login, press **Fix** again

11. You will get a notification saying you need to [restart Vortex](https://imgur.com/BgRaHUU). Do that.

12. Now, go to **Games > (search for) Palworld > (click on) Manage**

13. You'll get a pop-up, press **Download**
    
    * Vortex might get stuck downloading forever here. Just press cancel and press manage and download again

14. Vortex will now restart and it'll say it can't find the path to Palworld and you'll need to manually select it. Click **[Continue](https://imgur.com/FsBFrYs)**

15. You'll get a very ugly and old looking file picker that is very limited. We're going to have to select the Palworld directory. In our example, we installed Palworld in the default Steam location, which is stored in `~/.local/share`, which we can't really access from this limited file picker. Instead, adjust the following location `Z:\home\user\.local\share\Steam\steamapps\common\Palworld\Vortex-staging-mods`, so it matches yours (your username), and paste it in the [file picker's bar (File name:)](https://imgur.com/9JPwzpF). **MAKE SURE YOU USE BACKWARDS SLASHES, OR IT WON'T WORK**
    
    * If you store your Steam games elsewhere, and that doesn't involve hidden paths (folders that start with a . ), then you can navigate to the path using the file picker. `Z:` is your root partition disk, go from there

16. Go to **[Settings > Workarounds](https://i.imgur.com/2lZ0nLp.png)** 

17. Toggle on **Allow Symlinks without elevation (old mechanism, pre Vortex v1.4.3)**. You'll get a pop-up, click **Create Task**

18. Toggle the one above it also. You'll get a pop-up, click **Give Privilege**

19. Close Vortex and open it again

20. Now, go to **Settings > Mods > Mod Staging Folder (Palworld)**

21. Here, we'll enter the folder we created above for staging, **BUT** we will use the path in Links : `Z:\home\user\Links\Palworld\Vortex-staging-mods`. Click **Apply**

22. Vortex will now do some stuff and you'll get another pop-up (shocker, I know). Thing is, you can't use your mouse to navigate it, because high quality development. [Instead press **Tab** on your keyboard until **Revert All Changes** is highlighted.](https://i.imgur.com/HHZbzFn.png) Press **Enter** on your keyboard. Press **Tab** until **Confirm** is highlighted and press **Enter**.

23. Now, on the same page go to **Deployment Method** and select **Hardlink Deployment** and click Apply. If you get a pop-up similar to the one above, do the same as above. If it brings a pop-up saying something like "This mod is already installed" just click "Replace this mod" and apply.





#### CONGRATULATIONS! YOU CAN NOW ADD MODS FROM NEXUS MODS AND PLAY MODDED PALWORLD (or any other game)!

> There are mods that may require additional setup.
> 
> **!!!DO NOT LAUNCH PALWORLD/ANY GAME FROM VORTEX!!!**

---

## **Step 4: Installing and Managing Mods via Vortex**

**[Installing your first mod with vortex](https://wiki.nexusmods.com/index.php/Installing_your_first_mod_with_vortex)**

If there's a need for it, I can actually fill this section, but I don't think it's necessary.

---

## I did something wrong or something failed. How do I restart the guide?

* If for whatever reason this happens, you **must delete everything inside of `~/.config/steamtinkerlaunch/vortex/`**

* You might also need to nuke the game prefix, and maybe uninstall the game from steam, but both are unlikely to be required.

* I'll maybe make a troubleshooting section

---

## Some important notes

* **If you want to mod another game**, you basically just need to make the symlink for the other game, and configure the staging directory, just like we did above for Palworld

* If you get a pop-up from Vortex saying its installation is corrupt, you should be able to safely ignore it.

* Please don't bother the developer/s of STL about Vortex/modding. It's a very niche thing that isn't really supported in the first place

* If you want to mod games like Skyrim, that require other tools outside ov Vortex, like SKSE, you will need to get that sorted out

* As always, ~~google~~ the Internet is your best friend. Don't be afraid to [search](https://search.brave.com/) for fixes for your problem. If you encounter common Proton/Wine errors or driver errors, this has nothing to do with this guide

---

## **Outro**

My brain hurts, can't wait for the [Nexus Mods App](https://github.com/Nexus-Mods/NexusMods.App). That's it, thanks for reading and have fun modding! 

Feedback is welcome! Check my bio for Discord, or create an issue here.

Video coming: idk, maybe never.
