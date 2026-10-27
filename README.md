# MANABIT

[![tests](https://github.com/the-real-bench/manabit-public/actions/workflows/tests.yml/badge.svg)](https://github.com/the-real-bench/manabit-public/actions/workflows/tests.yml)

A cozy builder-battler roguelite. You're an Artificer: you crack open coffers of sleeping scrap, assemble a wind-up toy construct called a **Manabit** from six parts (head, core, two arms, legs, back), bind it, then spar, wager it in bouts, or carry it down a branching venture road. Lose a fight and the victor salvages your parts; lose your core on the road and the Manabit is gone. Win and you loot theirs.

- A catalog of bits across 17 style families, each with its own stats and abilities, most with procedurally built low-poly 3D models
- Turn-based, part-targeted combat: break an arm and it falls off; aim for the core to end it
- Two-currency economy (Scrap and Glimmer) with a broker, daily finds and a melt/distill loop
- Procedurally synthesized sound effects, ambience and a four-stem adaptive music box
- Saves to JSON, with additive save-version migrations

## Run it

Requires [Godot 4.7](https://godotengine.org/) (4.6 also works).

```bash
godot --path .                  # play
godot --headless --path . --import   # first run on a fresh clone: registers class names
```

## Tests

16 headless gates cover the data contract, builder, persistence, broker economy, combat, bouts, the run loop, catalog integrity, the free-kit roller and its power bands, layout budgets, the 3D stage, combat beat timing, audio wiring and the stalemate breaker.

```powershell
powershell -ExecutionPolicy Bypass -File run/gates.ps1   # all gates, exit 0 = green
```

```bash
godot --headless --path . -s res://tests/smoke_combat.gd   # any single gate
```

Note: the persistence gate writes the game's save file (`user://manabit_save.json`); back it up if you have a save you care about.

## Tools

- `tools/sim/`: measurement instruments: roster/ladder Monte Carlo sims and an economy sim used to balance numbers before changing them.
- `tools/audio/make_sfx.py`: seeded, byte-reproducible synthesis of every sound effect, ambience bed and music stem.

## Layout

```
combat/    turn-based, part-targeted combat resolver + enemy logic
economy/   pack/box rollers, broker
manabits/  the build session (assemble/equip rules)
meta/      player state, save manager, run state
parts/     the bit catalog
ui/        every screen, the 3D stage, tokens (see DESIGN.md)
audio/ art/  generated sounds, meshes, icons
```

## License

History was squashed into a single commit for the public release.

Copyright © ptbench Studios. All rights reserved. The code is public to read; no license is granted to copy, modify or distribute it.
