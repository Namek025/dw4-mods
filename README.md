# Digimon World 4 Mods

Patches for **Digimon World 4** (PS2, USA) that change EXP, weapon skill, death, evolution and
loading times, plus tools to edit character textures and export models.

This repository contains no game data. You need your own copy of the game.

## Install the patches

**Only for the USA PS2 release** (`SLUS-20836`, CRC `B871C1D0`). Other regions and the GameCube
version will not work.

1. Copy [`patches/SLUS-20836_B871C1D0.pnach`](patches/SLUS-20836_B871C1D0.pnach) to PCSX2's `patches` folder.
2. In PCSX2, open the game's properties, go to **Patches** and enable the ones you want.
3. Close the game completely and start it again.

Back up your save first. To turn a patch off, disable it and boot the game fresh: stopping it in
the menu does not restore the code, and save states keep the patched memory.

## Patches

| Patch | What it does | Tested |
|---|---|---|
| EXP per group | Each player gets 100% / 80% / 60% / 50% of a kill's EXP with 1 / 2 / 3 / 4 players, with no killer bonus | PCSX2, 2 players |
| EXP x2 | Every enemy gives double EXP. Can be combined with EXP per group | PCSX2, 2 players |
| Faster weapon skill | At levels 1-36, the level 1 skill cap takes ~200 hits instead of ~980 | PCSX2 |
| Death: recover your chip with X | Pick up your own backup chip with X to get back all bits and lost EXP, with no Recovery Disk | In game |
| Evolutions: shared level | All forms share level, EXP, weapon skills and UPCNT, so evolving no longer goes back to level 1 | In game |
| Loading: music requests bigger blocks + music buffer x4 | Use both: a stage transition goes from ~16.5 s to ~9 s | PCSX2 |
| Loading: 4-byte memmove | Faster string handling during loads. With the two above it adds little (8-9 s) | PCSX2 |
| Loading: 512 KB read requests | Experimental: no measured result yet | Experimental |
| Debug: all evolutions unlocked | Unlocks the 16 forms. **It stays in your save**, so use a test save | No test recorded |

None of them have been tested on a real PS2.

## Tools

Python 3. Install the dependencies, then run from this folder, with the disc files in `disc/`:

```sh
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
```

| Tool | Use |
|---|---|
| `tools/afs_names.py --name p_agumon` | Find a file's AFS entry by its real path |
| `tools/afs.py extract disc/NDMW.AFS out --entry 849` | Extract one AFS entry (without `--entry`, all of them) |
| `tools/igbtex.py export FILE.igb DIR` | Export an IGB's textures to PNG |
| `tools/igbtex.py import FILE.igb DIR OUT.igb` | Put edited PNGs back (same size) |
| `tools/igb2gltf.py FILE.igb OUT.glb` | Export a character to glTF for Blender (no animations yet) |
| `tools/igb.py FILE --db` | Print the game's database tables |
| `tools/luadis.py` | Disassemble compiled Lua 4.0 scripts |
| `tools/modiso.py IN.iso OUT.iso NDMW.AFS:ENTRY=FILE` | Write a copy of the ISO with replaced entries |

`data/meta.json` holds the class and field names the IGB tools need, because IGB files do not
store them.

## How the game works

Notes from reverse engineering the game. They cite addresses and function names.

- [Controls](docs/controls.md)
- [Death and backup chips](docs/death.md)
- [Difficulty](docs/difficulty.md)
- [Evolution](docs/evolution.md)
- [EXP](docs/exp.md)
- [Stats and GameRam](docs/gameram.md)
- [Weapon skill](docs/skill.md)
- [Loading times](docs/loading.md)
- [Models and textures](docs/models.md)
- [Trader Hall](docs/trader_hall.md)

## Related projects

- [dw4-gc](https://github.com/ivanno4317/dw4-gc): decompilation of the GameCube version (USA)
- [DigiAtlas](https://github.com/crashbashash/DigiAtlas): maps, drops and calculators
- [DW4 Crown Mod](https://github.com/crashbashash/DW4_Crown_Mod): disc patcher for several regions and consoles
- [DW4 Developer Stage](https://crashbashash.github.io/dw4-dev-stage/): guide to the hidden debug stage

## Contact

Open an issue on this repository, or find me on Discord: `namek`.

## License and legal

The code in `tools/` is under the [MIT License](tools/LICENSE). No license is granted for
`patches/`, `docs/` or `data/`.

Unofficial fan project, not affiliated with the game's rights holders. Digimon, Digimon World 4
and related names belong to their respective owners.
