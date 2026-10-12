# GT3 DevRAM Patcher

A Windows tool for enabling the 128 MiB development memory configuration in the PAL/EU version of Gran Turismo 3.

It can also optionally increase the course buffer for testing larger custom courses.

The tool does not include any Gran Turismo 3 game files. You must provide your own `CORE.GT3`.

## Current status

This project is still experimental.

The DevRAM patch and course buffer changes have been extensively checked against the known PAL/EU executable layout, but not every possible modified CORE can be guaranteed to work.

If you are using a modified `CORE.GT3`, run the compatibility scan first.

## Features

- Enables the 128 MiB DevRAM configuration
- Optional extended course buffer
- Supports the original PAL/EU CORE layout
- Can accept some previously modified CORE files
- Checks important patch locations before modifying anything
- Preserves unrelated compatible modifications
- Refuses to patch files when known conflicts are detected
- Does not modify the original input file
- GUI and command-line versions are included

## Requirements

- Windows 10 or Windows 11
- Your own Gran Turismo 3 PAL/EU `CORE.GT3`
- PCSX2 configured to use 128 MiB development memory
- A backup of your original files

No game files are included with this project.

## Usage

1. Download the latest release.
2. Extract the ZIP somewhere on your PC.
3. Run `GT3DevRAM.exe`.
4. Select your `CORE.GT3`.
5. Run the compatibility scan.
6. Select the options you want.
7. Build the patched output.

The original input file is left untouched.

### Modified CORE files

A CORE does not have to be completely untouched to work.

The compatibility mode allows some modified PAL/EU CORE files as long as the parts of the game required by the DevRAM patch still use the expected layout.

For example, unrelated changes elsewhere in the executable may be preserved.

The tool will reject files when it detects changes to important startup, memory-management or course-loading code that could make the patch unsafe.

Passing the compatibility scan does not guarantee that every combination of GT3 modifications will work together at runtime.

## Extended course buffer

The course buffer option is intended for custom course testing.

Different capacities can be selected depending on the course being tested.

Larger settings use considerably more EE memory and should not automatically be considered better. The highest settings are experimental.

If you only want DevRAM, leave the extended course buffer option disabled.

## Important note about the output

The current tool produces a patched direct-boot ELF.

It does not currently rebuild a normally signed replacement `CORE.GT3` for use through the original game boot process.

## PCSX2

The patched game expects PCSX2 to be configured with the development memory size required by the patch.

Using the patched executable without the correct memory configuration is not supported.

## Compatibility

At the moment this project targets the PAL/EU GT3 executable layout used during development.

Other regions should be considered unsupported unless support for them is specifically added in a future release.

Modified PAL/EU files may work when they retain the required executable layout and pass the compatibility scan.

## What this does not change

This patch increases available EE memory.

It does not increase the PS2's GS VRAM, remove every internal GT3 buffer limit, or automatically make every large course or car compatible with the game.

Those are separate limitations.

## Backups

Always keep your original files.

The program writes its result separately, but you should still keep an untouched copy of your original `CORE.GT3`.

## Bug reports

If you find a file that you believe should be compatible but the tool rejects it, open an Issue and include:

- The version of the tool
- Whether the CORE was modified
- Which options you selected
- The compatibility/error message shown by the program

Do not upload copyrighted game files when reporting an issue.

## Disclaimer

This is an unofficial fan-made modding tool and is not affiliated with or endorsed by Sony Interactive Entertainment or Polyphony Digital.

Gran Turismo and related names are trademarks of their respective owners.

No copyrighted Gran Turismo game files are distributed with this project.
