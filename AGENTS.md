# Respeaker Lite ESPHome Integration - Context for LLM Agents

This document provides essential context for any LLM agent assisting with this repository. Please read this file carefully to understand the project structure and your role.

## ⚠️ CRITICAL AGENT RULES AND DIRECTIVES ⚠️
- **NO COMPILING**: All debugging, compiling, and flashing must be done **manually by the user**. 
- **NO EXECUTION**: Do not attempt to run, compile, build, or analyze the firmware dynamically using shell commands.
- Focus strictly on code editing, giving advice, creating configurations, and explaining the logic conceptually.
- **NEVER attempt to flash or run ESPHome compilation commands yourself.**

## Project Overview
This project integrates the Seeed Respeaker Lite Voice Kit (equipped with a XIAO ESP32-S3) with ESPHome. It relies on the official Home Assistant Voice Preview Edition code but adds enhancements such as a 48kHz sample rate for improved music playback quality. The primary goal is functioning as a reliable voice assistant satellite for Home Assistant.

## Key Files and Directories

- **`config/common/respeaker-satellite-base.yaml`**: **CRITICAL FILE.** This is the most important file for making configuration changes. It is the base ESPHome YAML that defines the core behavior of the satellite. The actual device inherits this configuration. When configuring or modifying the device's ESPHome setup, make your changes here.
- **`config/respeaker-satellite-dashboard-example.yaml`**: The entry-point ESPHome configuration file that users compile and flash, which inherits the base file mentioned above.
- **`config/respeaker-satellite-testing.yaml`**: A unified testing configuration file that combines the base and dashboard YAML files for local compilation. **When making changes to `config/common/respeaker-satellite-base.yaml`, those same changes must also be applied to this file.** The user uses this file to quickly compile and test code locally without pushing changes.
- **`esphome/components/respeaker_lite/`**: This directory contains important custom component nodes (C++ and Python) that define the custom logic for the Respeaker Lite. If changes to core behavior or new C++ functionalities are needed, look here.
- **`readme/`**: Contains various documentation covering extra features:
  - `alarms.md` - Explains the daily alarm feature, requiring correct POSIX timezone setup, and configuring alarm actions (Play sound, Send event, or both).
  - `blueprints.md` - Useful Home Assistant blueprints for managing the satellite (e.g., volume ducking, TTS redirection).
  - `tts_uri.md` - Documents the custom `esphome.tts_uri` event which allows intercepting responses and playing them on other media players.

## Important Features
Some specific capabilities of this implementation to keep in mind:
- Feature parity with Voice PE (excluding volume control).
- 48kHz sample rate output.
- Additional sensors/switches for timers, muting sounds, and turning off button sounds.
- Emits custom events: `esphome.tts_uri` and `esphome.stt_text`.
- Built-in DFU software auto-update (automatically installs XMOS firmware).
