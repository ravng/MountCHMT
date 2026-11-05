# EaglePNP

EaglePNP contains a custom EAGLE ULP script for exporting top-layer SMD placements to a Charmhigh-compatible `.dpv` placement file.

## What is included

- `mountCHMT.ulp` – ULP script that:
  - reads a Charmhigh reel table (`.dpv`) from a configured directory
  - lets you assign parts to feeder stations, head, and reel rotation
  - auto-detects likely station matches from prior selections
  - writes a placement output `.dpv` for the current board
- `mountCHMT.cfg` – persisted learning/profile data used by the script

## Requirements

- Autodesk EAGLE (tested target noted in script: 7.7.0)
- A board (`.brd`) open in EAGLE
- A directory containing at least one Charmhigh reel table `.dpv` file

## Usage

1. Open your board in EAGLE.
2. Run `mountCHMT.ulp`.
3. On first run, select your reel-table directory when prompted.
4. Review auto-assigned stations in the dialog:
   - set **Station**
   - set **Head** (1 or 2)
   - set **Angle** and **Reel angle** as needed
5. Click **OK** to generate output.

The script writes a board-level output file with `.dpv` extension (same base name as the board).

## Learning behavior

`mountCHMT.cfg` stores:

- `Profile,<station-id>,<head>,<reel-rotation>`
- `Learn,<token>,<station-id>,<head>,<reel-rotation>,<count>`

This allows future runs to improve station/head/reel suggestions based on previous confirmations.

## Notes

- Only populated **top-layer SMD** elements are included.
- If no board is open, no station rows are found, or no top-layer SMD parts exist, the script exits with a message.
