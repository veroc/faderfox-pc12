# Faderfox PC12 Web Editor

A browser-based configuration editor for the [Faderfox PC12](http://www.faderfox.de) MIDI controller. Edit control assignments, channels, value ranges, and modes — then send setups directly to the device over USB via Web MIDI.

## Requirements

- **Browser**: Chrome or Edge (Web MIDI with SysEx support required)
- **Connection**: Faderfox PC12 connected via USB

> Firefox and Safari do not support Web MIDI. Use a Chromium-based browser.

## Getting Started

1. Open `index.html` in Chrome or Edge
2. Allow MIDI access when prompted (the browser will ask for SysEx permission)
3. Select the PC12 from the **MIDI In** and **MIDI Out** dropdowns (auto-detected if the name contains "Faderfox")

## Receiving a Setup from the PC12

1. Click **Receive from Device** in the toolbar
2. On the PC12, enter **Setup Mode**: hold the red **Shift** button and press the **blue** button
3. Select the setup you want to dump using **Taste 1** (encoder to choose Setup 1–30)
4. Press and hold **Taste 7** (Send):
   - **Sndc** — sends the currently selected setup
   - **SndA** — sends all 8 setups (use encoder to toggle, then hold the button until the progress bars complete)
5. The editor grid will populate automatically when the SysEx dump is received

## Editing Controls

The grid mirrors the physical layout of the PC12:

| Section | Description |
|---------|-------------|
| **Rows A–F** | 72 potentiometers (12 per row) |
| **Row G** | 12 green buttons with LEDs |
| **Enc** | Push-encoder and encoder push button |

Click any cell in the grid to open the parameter editor on the right side.

### Parameters per Control

| Parameter | Description |
|-----------|-------------|
| **Command Type** | CC Absolute, CC Relative, Note, Program Change, Pitchbend, Aftertouch, CC 14-bit |
| **MIDI Channel** | Channel 1–16 |
| **CC / Note Number** | Controller or note number 0–127 |
| **Lower Value** | Minimum value (poti start / button release) |
| **Upper Value** | Maximum value (poti end / button press) |
| **Mode** | Potis: Jump or Snap · Buttons: Momentary or Toggle · Encoder: Acceleration 0–3 |
| **Display Scale** | OFF, Standard (0–127), Bipolar (-63 to 63), or External (buttons) |

### Batch Editing

- **Copy to Row** — copies the selected control's settings across all 12 positions in the same row (CC numbers increment automatically)
- **Copy to Column** — copies settings down the column across rows A–F

## Sending a Setup to the PC12

1. On the PC12, enter **Setup Mode** (hold red Shift + press blue)
2. Press and hold **Taste 8** (Receive) until the display shows `rc00`
3. In the editor, click **Send to Device**
4. The PC12 display will show progress (`rc01`...`rc99`) and return to normal when done

> If the display shows `Err`, press the red Shift button and re-enter Receive mode to try again.

## File Import / Export

| Action | Format | Description |
|--------|--------|-------------|
| **Export .syx** | Binary SysEx | Standard `.syx` file, compatible with MIDI librarian tools (Bome SendSX, Snoize SysEx Librarian) |
| **Export JSON** | JSON | Human-readable dump with all control parameters and raw hex data |
| **Import** | `.syx`, `.json`, `.bin` | Load a previously saved setup into the editor |

## Factory Reset

Click **Reset Setup** to restore the current setup to factory defaults:

- Potis: CC 1–72 across rows A–F, channel 1, CC Absolute, Jump mode, range 0–127
- Buttons: CC 73–84 on row G, toggle mode
- Encoder: CC 85 (absolute), Encoder push: CC 86 (note, momentary)

This only resets the editor data. To reset the PC12 itself, use Setup Mode → Taste 6 on the device.


## Project Files

| File | Purpose |
|------|---------|
| `index.html` | The editor application (single-file, no build step) |

## License

This is an unofficial community tool. Faderfox is a trademark of Mathias Fuchß Software-Entwicklung, Hamburg, Germany.
