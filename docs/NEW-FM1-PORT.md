# Newer FM-1 Hardware Port

## Product goal

Keep the sampler on the phone: import or record audio, trim and slice it, play it, and apply the sampler and loop effects there. The FM-1 remains the hands-on controller: keys, buttons, encoders, LEDs, screen, and audio output.

## What the current fork already does

The v0.37 codebase already has that split. `engine/` owns sampling, slicing, effects, and looping; `android/` owns phone audio, USB MIDI, and the app UI; `firmware/` turns the FM-1 into the matching controller. The phone app and FM-1 firmware share `PROTOCOL.md`.

The current release is not a verified new-hardware build. The upstream README says the v0.37 redesign was host-tested but was not tested on a real phone or FM-1. The Android package and matching flash page are separate release assets.

## New flash-chip target

An open-source FM-1 firmware implementation identifies the original Puya P25Q80 as JEDEC ID `0x856014` and the newer UC25HQ80 as `0xB36014`, and handles both IDs. See its [flash ID header](https://github.com/Cosmo-K-444/lowtide-fm1/blob/main/firmware/hal/fm1_flash_id.h). Treat the ID reported by the actual device as authoritative; do not infer it from purchase date or seller listing.

This fork currently bundles an FM-1 V15 package and binary SDK. Its application uses the SDK flash API for saved projects and sample data. The SDK and updater loader are binary components, and the application source does not explicitly identify either flash-chip ID. That means support for `0xB36014` is **unverified**; the presence of generic flash functions is not proof that reads, writes, erase, or firmware updates work on the newer part.

## Port work

1. Record the device's actual flash JEDEC ID and installed firmware/loader versions. Preserve the official recovery path before testing.
2. Build against a matching FM-1 SDK and update loader that explicitly support the reported chip, or replace the app's storage calls with a reviewed driver that supports both known parts. Keep the sampler's storage layout and upgrade package format intact.
3. Add a workbench preflight that reports the detected device and firmware, blocks unknown hardware, and offers a clear recovery route. Keep the sampler's MIDI/SysEx protocol versioned separately from the flash driver.
4. Produce one release bundle with the matching Android APK, flash page, concise install steps, and checksums. The install page should verify the device before writing and clearly report each completed step.
5. Validate on the actual newer FM-1: USB MIDI controls, screen and LEDs, USB audio to the FM-1 output, sample/project save across power cycles, update, and return to official firmware.

## Acceptance criteria

- The phone handles sample import/recording, slicing, playback, and effects; the FM-1 supplies the physical controls.
- Both `0x856014` and `0xB36014` are recognized and tested, or the installer clearly supports only the tested one.
- Unknown chips are detected before erase/write and are not flashed.
- A first-time user can follow one release page and one guided install flow without finding matching files across separate instructions.
- The release records which phone, Android version, FM-1 flash ID, and firmware/loader versions were tested.

## Current status

This branch records the port target and acceptance criteria. It does not yet claim new-chip compatibility or change the firmware image. The next firmware change depends on a known-good SDK/loader for the device's reported chip; the current bundled binary SDK is not enough to safely certify that change.
