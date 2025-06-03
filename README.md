# LonganPi 3H DTS for Tina Linux 5.4 + Apollo_P2 (Android 12)

This repo is a no-BS, hard-earned, open record of the device tree bring-up process for the **LonganPi 3H**, based on the **Allwinner H618** SoC.

It spans the Allwinner Tina Linux 5.4 BSP, the Android 12 `apollo_p2` build, U-Boot, and even live dumps from booted firmware — because that’s what it took. No shortcuts. No guessing. Just brute-force learning, failure, and a mission to turn this opaque platform into something *usable and open*.
I have left a few old itterations so (if you are interested you can see my struggles and changes.) When I tell you I have never attemped to play with creating or reversing dts files or playing with embeded before I tell you just for context if you feel the need to critique you can email me I am not hard to find....
---

## 🧠 Context: The Long Road

This has been my **love-hate project** since **December 2024**. I’m self-taught. I didn’t come into this with formal training, a team, or a company badge. Just a stubborn streak, a debugger, and a need to make this board useful **without spyware, bloat, or box-UI nonsense**.

What started as a DTS edit turned into a multi-month odyssey:

- Unpacking and reverse-engineering **Allwinner Android firmware**
- Figuring out what was even bootable and what was just vendor trapware
- Rebuilding `build.sh` logic, boot chains, and kernel arguments
- Decoding how Allwinner's `p2` config in Tina Linux maps to their Android builds
- Pulling **real live DTs** off working devices just to diff what they *actually* use

And somewhere in the middle of all this, I realized: **they weren’t going to document it.** So I did.

---

## 💬 Disclaimer

I don’t work for Allwinner. I don’t endorse them. I’m not responsible for their broken blobs, weird daemons, or junk system services. What you see here is the result of **painstaking manual analysis**, done for the purpose of creating an **open and usable baseline** for real developers and hackers — not vendors.

---

## 📂 What’s In This Repo?

| Path         | Contents |
|--------------|----------|
| `board/`     | Board-level DTS files for kernel and U-Boot |
| `sourcedts/` | Decompiled or pulled live from booted Android/Tina images |
| `include/`   | Platform includes like `sun50iw9.dtsi` |
| `p2_config/` | Original Allwinner build config for `p2` (Tina BSP path: `device/config/chips/h618/configs/p2`) |

---
### look change the model name if you want it just makes it easier if you leave it sun50iw9 ###

## 🔧 How To Use

### For Tina Linux 5.4:

1. Place files in:
   ```bash
   target/linux/sunxi/files-5.4/arch/arm64/boot/dts/

2. Then build with:

./build.sh autoconfig -i h618 -o android -n default -a arm64 -k linux-5.4 -b p2

3. ./build.sh 


For U-Boot:
rename it to uboot-board.dts and drop it in to your p2 dir 
or do something like this 
cp board/uboot-board.lpi3h.dts u-boot/arch/arm/dts/
Add it to your U-Boot Makefile or config.

## Look I understand there are probably way easier ways to do this and that there is a full a$$ Mainline Sdk with all the mainline dts files but when I reached out to the sunxi-linux guys for help I didnt hear back lol So I did this by trial and error and a $12 debugger.    
🧪 Notes + Real World
dtb_267800.dts is a clean dump from a booted Android 12 system.

dtbo.dts and modified_failed_boot.dts exist so you don’t have to repeat those mistakes.

longanpi3h.board.dts is the cleanest form I’ve tested for Tina.

p2_config/ maps to the exact logic used in build.sh and shows how Allwinner ties the kernel, bootloader, and DTS together — both in Tina and Android 12.

🔥 Final Word
This repo is still a work in progress, but it’s also a real foundation for anyone trying to make sense of Allwinner’s H618 BSP. If you're working with the LonganPi 3H, the Apollo_P2 board, or just trying to strip Android TV UI off a dev kit — this is for you.

Open it. Fork it. Diff it. Use it. Just don’t ask me why Allwinner does what they do — I’m just the guy who wouldn’t quit.

🙌 Maintainer
Made by @johnohhh1 —
A stubborn, self-taught builder who believes firmware should be free and knowable.

✊ #longanpi3h #h618 #tinalinux #apollo_p2 #aosp12 #devmode


---

## 🔁 Next step
cry when you try to figure out android..... if any of you aosp guys wanna share me a clean tablet ux for the bsp I will happily share my favorite parts with you.
