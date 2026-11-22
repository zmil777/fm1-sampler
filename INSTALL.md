# Install the FM-1 Sampler

The phone runs the sampler, slicing, loop recording, and effects. The FM-1 supplies the keys, buttons, encoders, screen, LEDs, and audio output.

## Before flashing

The v0.37 firmware has not been verified on the newer FM-1 flash chip. This fork's firmware package uses a bundled V15 SDK/loader and does not report the flash JEDEC ID. **If your FM-1 is a newer unit, do not flash the current v0.37 Workbench page.** Wait for a build that identifies and supports your chip, or stay on the official firmware.

For a confirmed compatible release, download the APK and the Workbench HTML from the *same* GitHub release. The Workbench page is for a computer; use desktop Chrome or Edge. It needs Web MIDI and SysEx access.

## Firmware setup

1. Close other FM-1 update pages, MIDI tools, and DAWs that might hold the USB MIDI port.
2. Connect the FM-1 to the computer with a USB data cable and open the downloaded Workbench HTML in Chrome or Edge. Avoid an attachment preview.
3. In **Firmware update**, select **Connect device** and allow the browser's MIDI/SysEx request for the FM-1.
4. Use **Projects & sounds** to export anything you need to keep. Project and sample data may not survive firmware migration.
5. Return to **Firmware update**, check the backup confirmation, then start the update. Keep the FM-1 powered and connected until the page reports completion.
6. If the page cannot identify the device or reports a compatibility mismatch, stop. Do not force-flash an unverified hardware revision.

## Android setup

1. Transfer the matching APK to the Android phone and open it. Allow Android to install apps from the file manager or browser used to open the APK.
2. Connect the FM-1 to the phone with a USB-C OTG adapter or data-capable USB-C cable. Accept Android's USB/MIDI prompt if it appears.
3. Launch FM-1 Sampler. The app detects the FM-1's USB MIDI and USB audio devices; plug headphones or speakers into the FM-1 output.
4. Import a sample with the folder control, record a sample with the microphone control, then play the FM-1 keys. Use the FM-1 buttons and encoders to select tracks, modes, and effect pages.

## If the phone does not connect

- Confirm the cable supports data and the phone supports USB host/OTG.
- Disconnect and reconnect the FM-1, then reopen the app and accept the USB prompt.
- Close other apps that may have claimed the MIDI connection.
- If the display or controls do not match the phone app, check that the exact matching firmware and APK release are installed.

## New-chip support status

The project port tracker is in [`docs/NEW-FM1-PORT.md`](docs/NEW-FM1-PORT.md). It lists the required chip checks and the validation still needed before a new-chip firmware release can be called compatible.
