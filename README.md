# GT3 DevRAM Patcher

A Windows tool that patches a compatible PAL/EU Gran Turismo 3 `CORE.GT3` to use 128 MiB development RAM in PCSX2. There is also an optional larger course buffer for custom tracks.

You supply the CORE. The tool writes a separate, patched `.elf` and leaves your input alone. No game files are included.

## Download

Get the Windows ZIP from this repository's **Releases** section, extract it and run `GT3DevRAM.exe`. `GT3DevRAM-CLI.exe` is included for command-line use.

## Before starting

You need 64-bit Windows, your own supported PAL/EU CORE, a matching GT3 ISO, and a working PCSX2 setup with your own BIOS. Use a PCSX2 build that offers **Enable 128MB RAM (Dev Console)**.

Keep your original files. This tool builds a direct-boot ELF; it does not make a replacement signed `CORE.GT3` for the normal disc boot process.

## Make the ELF

1. Open `GT3DevRAM.exe` and select your CORE.
2. Choose a new output folder inside an existing writable folder.
3. For normal ISO play, select **Asset source: disc**. Use **host** only with a prepared, extracted GT3 `data` folder. **preserve** leaves the input's existing choice unchanged.
4. Leave the course option unchecked for RAM-only, or enter the course capacity you need.
5. Click **Scan compatibility**, then **Create new patched ELF**.

The output folder includes the ELF, `BUILD_REPORT.json` and `BOOT_INSTRUCTIONS.txt`.

## Run it in PCSX2

These steps use the desktop/Qt interface. Menu wording may differ slightly between builds.

1. Keep the generated `.elf` in a permanent folder. In PCSX2, open **Settings → Game List** and add that folder to the search directories. Enable recursive scanning if the ELF is in a subfolder, then refresh the list.
2. Right-click the **ELF entry** → **Properties → Summary**. Set **Disc Path** to your matching PAL/EU GT3 ISO. Adding the ISO to the list on its own is not enough.
3. Enable **Tools → Show Advanced Settings**. Open the ELF's **Properties → Advanced** and enable **Enable 128MB RAM (Dev Console)**. A build with a memory-size selector needs **128 MB**.
4. Stop any running emulation, then start the **ELF entry**, not the normal ISO entry. Do not load an old save state for this boot. Normal memory-card saves can still be used.

For HostFS, put the ELF **beside** your prepared `data` folder, enable the ELF's **Properties → Emulation → Enable Host Filesystem**, and keep the ISO associated. The patcher does not extract or prepare the game assets.

See [PCSX2_SETUP.txt](PCSX2_SETUP.txt) for the full instructions, folder examples and troubleshooting. The same guide is written beside each generated ELF. There is also a **PCSX2 setup...** button in the program.

## Course capacity

The optional course patch accepts 13–80 MiB. Use a setting that fits the course without spending more memory than needed. Courses, cars and other game allocations share memory; 128 MiB does not mean a course can use all 128 MiB. The 80-MiB setting is experimental.

This does not increase GS VRAM or remove the separate car and renderer limits. Recheck the PCSX2 settings whenever you build a different ELF.

## Modified CORE files

Enable **Allow modified EU inputs** for a CORE that has already been edited. It must still have the layout and code needed by this patch. Unrelated compatible edits are kept; conflicting hooks or changed dependencies are rejected.

A passing scan is not a guarantee that every combination of mods will work in-game. Start with a stock course, then test your intended course, cars and mode.

## Problems

Open an Issue with the tool version, PCSX2 version, selected settings and the error text. Do not upload your CORE, ELF, ISO or BIOS.

