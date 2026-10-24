# Adam's Proven VZBot setup

**A proven VZBot 330 Klipper configuration, shared as a real-world reference.**

This repository contains the printer configuration and supporting files from Adam's VZBot setup. It is an example of how one machine is configured: useful for comparing settings, understanding the configuration structure, and taking ideas for your own VZBot 330.

> **Do not copy and paste this configuration onto your printer.** These files describe one particular machine, including its wiring, motor directions, currents, motion limits, heaters, probe geometry, macros, and saved calibration data. Proven on this setup does not mean correct for another VZBot. Redacted values and existing device-ID placeholders also make this a reference snapshot, not a ready-to-run configuration.

There is no installation or getting-started guide here. Slicer profiles and slicer-related files are outside this repository and will be shared separately.

## What's included

| File | Purpose |
| --- | --- |
| [printer.cfg](config/printer.cfg) | Main Klipper configuration: motion, motors and drivers, extruder, heaters, fans, input shaping, and saved calibration |
| [cartographer.cfg](config/cartographer.cfg) | Cartographer MCU and probe, bed mesh geometry, ADXL345, and resonance testing |
| [macros.cfg](config/macros.cfg) | Print start/end, pause/cancel, and fan-control macros |
| [mainsail.cfg](config/mainsail.cfg) | Bundled Mainsail client macros and virtual SD card configuration |
| [moonraker.conf](config/moonraker.conf) | Moonraker server, authorization settings, and update-manager configuration |

The main configuration includes mainsail.cfg, macros.cfg, and cartographer.cfg. Moonraker has its own configuration file.

## Configuration at a glance

The following describes the contents of this snapshot; it is not a recommended hardware list or a set of target values.

| Area | What the files describe |
| --- | --- |
| Printer | VZBot 330, CoreXY, with additional X1 and Y1 steppers |
| Controller | Controller labelled Octopus; main MCU path identifies STM32H723 |
| Host | Host temperature sensor labelled OrangePi |
| Drivers | TMC5160 for X, X1, Y, Y1, Z, and extruder |
| Configured travel | X: 330 mm; Y: 300 mm; Z: 400 mm |
| Extruder | 0.4 mm nozzle, 1.75 mm filament, 60:10 gear ratio, PT1000 sensor |
| Probe | Cartographer; saved model metadata identifies V4 hardware |
| Cooling | Part cooling, hotend fan, two RSCS fans, and exhaust fan |
| Chamber | Temperature sensor and a separate multi-pin chamber output |

The file set does not establish every board revision, motor model, hotend model, or firmware version. Those details should not be inferred from the printer name alone.

## Machine-specific details worth noticing

- **Motion values are aggressive.** The snapshot sets max_velocity to 1250 mm/s and max_accel to 60000 mm/s². These are configured limits, not evidence that every print runs at those values, and not suggested starting points.
- **Travel is configuration-specific.** Despite the 330 model name, the configured Y maximum is 300 mm. Homing locations, probe offsets, mesh boundaries, and park positions belong to this machine.
- **Saved calibration is retained as reference.** The SAVE_CONFIG block contains heater PID values, a saved bed mesh, probe information, and Cartographer scan/touch models. Input shaping and pressure advance are also machine/material-dependent examples.
- **Saved and active mesh settings differ.** The saved mesh is 6 × 6, while the active Cartographer mesh configuration requests 25 × 25 points. The saved profile is historical data, not a description of every new mesh.
- **Macros depend on the full configuration.** PRINT_START heats the bed, holds the hotend at 130 °C, homes, invokes CARTOGRAPHER_TOUCH_HOME, creates a bed mesh, and then reaches the requested hotend temperature. Its defaults are BED=80 and HOTEND=250. OLD_PRINT_START is retained as an older alternative, not the main print-start routine.
- **Pause/cancel definitions overlap.** Both mainsail.cfg and macros.cfg define PAUSE and CANCEL_PRINT with rename_existing. Review the included macro definitions together rather than transplanting individual blocks without their context.
- **Parking and Z moves assume this machine.** PRINT_END and PAUSE contain fixed park positions and relative Z lifts; CANCEL_PRINT contains a fixed Z move. Their suitability depends on position, homing state, coordinate mode, and available travel.
- **Fan commands are customized.** M106 P0 controls the normal part fan, P2 controls both RSCS fans, and other P values control the exhaust. The supplied M107 behavior is not a symmetric mapping for all of those paths.
- **The chamber output is not a temperature-controlled chamber heater section.** It is configured as an output_pin using two pins, with a separate chamber temperature sensor.
- **Moonraker settings reflect one installation.** The broad trusted-client ranges, CORS entries, paths, and update channels are reference values, not a general network configuration recommendation.

## Redactions and privacy

Private host-account paths and the machine's explicit local hostname are represented by the literal text **redacted**, enclosed in two asterisks on each side. Existing single-asterisk redaction markers have been normalized to that same marker. Any occurrence of the private host username in the supplied files is removed from this published copy.

The two MCU serial paths already contained unique_id placeholders in the supplied snapshot. They remain placeholders. No actual unique MCU identifiers were present in those fields.

Generic network settings such as 0.0.0.0 and private-network CIDR ranges are retained because they describe server binding and authorization policy rather than identify an individual device. Public upstream project links and the third-party Mainsail copyright notice are also retained.

Redacted paths and hostnames are intentionally incomplete. They are not valid replacements for your own installation details. The original local source files were not changed during publication.

## About this snapshot

This is an owner-proven configuration shared for reference. Publication involved reviewing the supplied text files, checking their include relationships, and sanitizing private host details. It did not involve running the configuration on a printer or independently verifying motion, thermal behavior, or print results.

## Attribution and licensing

The bundled mainsail.cfg carries its original 2022 Alex Zellner copyright notice and states that it may be distributed under GNU GPLv3. That notice is preserved. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

No additional repository-wide license is assigned to the other files in this snapshot.
