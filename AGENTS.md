# AGENTS.md

ZMK firmware config for Daniel's roBa split keyboard (Seeed XIAO BLE, trackball via PMW3610). Builds run in GitHub Actions; there is no local toolchain.

## Layout

| Path | Role |
| --- | --- |
| `config/roBa.keymap` | The keymap — layers, combos, behaviors. Most edits go here. Often edited via keymap-editor (bot commits). |
| `config/roBa_L.keymap`, `config/roBa_R.keymap` | Per-half keymaps |
| `config/boards/shields/roBa/` | Shield definition: `roBa.dtsi`, `roBa_L/R.overlay`, `roBa_L/R.conf`, Kconfig |
| `config/west.yml` | Pinned modules: ZMK `v0.3.0`, `zmk-pmw3610-driver`, `zmk-rgbled-widget`, `prospector-zmk-module v2.0.0` |
| `build.yaml` | GitHub Actions build matrix: `roBa_R` (with `studio-rpc-usb-uart`), `roBa_L`, `settings_reset` |
| `model/` | Case and keycap 3D models |

## Workflow

- Push → `.github/workflows/build.yml` builds `.uf2` artifacts; flash by copying to the XIAO in bootloader mode.
- `roBa_R` is the central half (ZMK Studio over USB).
- Keep devicetree syntax valid — a broken keymap only fails in CI. Check bindings against ZMK v0.3.0 docs, not newer `main`.
- Hardware design lives in the separate upstream `roBa/` repo (not Daniel's).
