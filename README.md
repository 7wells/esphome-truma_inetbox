# Minimal Truma ESPHome Repo

Minimal ESPHome setup for a Smartavan-style ESP32 controller that talks to a Truma CP Plus through the `truma_inetbox` component.

## Upstream And References

This repo is based on Fabian Schmidt's `esphome-truma_inetbox` project:

- [Fabian Schmidt - esphome-truma_inetbox](https://github.com/Fabian-Schmidt/esphome-truma_inetbox)

Helpful background and protocol references:

- [danielfett - inetbox.py](https://github.com/danielfett/inetbox.py)
- [mc0110 - inetbox2mqtt](https://github.com/mc0110/inetbox2mqtt)
- [muccc - WomoLIN](https://github.com/muccc/WomoLIN)

Current target:

- Arduino framework
- ESPHome 2025.9.3
- no Home Assistant
- local web interface only
- OTA updates
- room heating
- hot water

## Repo Layout

- `components/`
  - local component code based on Fabian Schmidt's `esphome-truma_inetbox`
- `configs/`
  - local machine-specific configuration files
  - intentionally excluded from Git, except `*.example`

## Local Config

Use these local files as the starting point:

- `configs/truma.yaml.example`
- `configs/secrets.yaml.example`

Create your own local copies:

- `configs/truma.yaml`
- `configs/secrets.yaml`

These real config files are ignored by Git.

## Build Setup

This project is currently pinned to:

- ESPHome `2025.9.3`

If a newer ESPHome version exists, it is recommended to create a dedicated virtual environment for this repo instead of upgrading blindly.

Example setup on Windows PowerShell:

```powershell
py -3.12 -m venv .venv-esphome-2025
.\.venv-esphome-2025\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install esphome==2025.9.3
```

Activate the environment before building, flashing, or reading logs:

```powershell
.\.venv-esphome-2025\Scripts\Activate.ps1
```

Common commands:

```powershell
python -m esphome compile .\configs\truma.yaml
python -m esphome upload .\configs\truma.yaml --device COM3
python -m esphome logs .\configs\truma.yaml --device COM3
```

## Scope

This repo is intentionally minimal.

Not included in the first target setup:

- Home Assistant integration
- MQTT
- timer logic
- clock sync
- air conditioning
- Alde support
- extra demo configs
- legacy examples and tests

## Notes

The current goal is a small, understandable, stable baseline first.
Further cleanups and protocol fixes can be added later in a controlled way.

Current known limits:

- Room heating is exposed through a climate card. Water control is exposed through a discrete mode select.
- Water control maps to Off, Eco 40 C, High 60 C, and Boost 80 C.
- Standalone ventilation without heating is not exposed in the current minimal setup.
