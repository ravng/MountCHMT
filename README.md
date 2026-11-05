# MountCHMT

<img width="1098" height="662" alt="Screenshootulp" src="https://github.com/user-attachments/assets/15937391-5478-47d5-bd6e-fab04b75d853" />

MountCHMT is a custom EAGLE ULP script for exporting top-layer SMD placements to a Charmhigh-compatible `.dpv` placement file.

## Requirements

- Autodesk EAGLE (tested on version 7.7.0 on linux).
- A directory containing at least one Charmhigh reel table `.dpv` file.
(If you don't have one create it with the CHMT SmtMain software first).

## Usage

The script will read newest modified dpv file to get current Reel setup.
It will try to guess what reel to use for each component. It will get better for each board you do.


1. Open your board in EAGLE.
2. Run `mountCHMT.ulp`.
3. On first run, select your reel-table directory when prompted. This is a directory holding your dpv file(s).
5. Review auto-assigned stations in the dialog, specially:
   - set **Station (Reel)**
   - set **Head** (1 or 2)
6. Click **OK** to generate output.
7. File is stored in board working directory as .dpv file.

Note about **Reel angle** and **Angle**:
Reel angle let's you adjust any orientation mismatch between physical part on reel and the part in eagle.
Angle is auto set from board and is not supposed to be adjusted unless something spesific for this board.

## Learning behavior

`mountCHMT.cfg` stores:

- `Profile,<station-id>,<head>,<reel-rotation>`
- `Learn,<token>,<station-id>,<head>,<reel-rotation>,<count>`

This allows future runs to improve station/head/reel suggestions based on previous confirmations.

## Notes

- Only populated **top-layer SMD** elements are included.
- If no board is open, no station rows are found, or no top-layer SMD parts exist, the script exits with a message.
