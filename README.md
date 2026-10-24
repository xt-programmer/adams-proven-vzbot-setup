# Adam's Proven VZBot setup

This is the Klipper configuration I use on my **VZBot 330 AWD**. It prints great and gives me a comfortable, reliable workhorse setup without pushing the printer to its limits.

I'm sharing it so other VZBot owners have a proven example to look through, compare against, and take ideas from. My focus is consistent print quality and dependable everyday use.

> **Do not copy and paste this configuration onto your printer.** It is tuned for my hardware, wiring, motor directions, currents, heaters, probe geometry, and calibration. Use it as a reference and understand each setting before adapting anything to your own machine.

## My printer

I'm running a VZBot 330 AWD with LDO 2504AC steppers, CNC metal parts, LDO rails, a Goliath hotend, Hextrudort extruder, CPAP cooling, RSCS fans, and a Cartographer probe. It has a full plexiglass enclosure, a PTC chamber heater, and a 240 V AC heated bed, with an Octopus Pro, TMC5160 Pro drivers, and an Orange Pi 5 Pro.

The full parts list is in [printer-hardware.md](printer-hardware.md).

## Files

| File | Contents |
| --- | --- |
| [printer.cfg](config/printer.cfg) | Main printer configuration and saved calibration |
| [cartographer.cfg](config/cartographer.cfg) | Cartographer probe, bed mesh, and resonance testing |
| [macros.cfg](config/macros.cfg) | My print start/end, pause/cancel, and fan-control macros |
| [mainsail.cfg](config/mainsail.cfg) | Mainsail client macros and virtual SD card configuration |
| [moonraker.conf](config/moonraker.conf) | Moonraker server and update-manager configuration |

The saved PID values, bed mesh, Cartographer models, input shaping, and pressure advance belong to my setup. They are included for reference, not as calibration values for another printer. My macros and fan mappings are customized too, so read them together with the main configuration.

Slicer profiles and slicer-related files will be shared separately.

## Redacted details

I've replaced private account paths and my local hostname with the literal marker `**redacted**`. MCU serial paths use `unique_id` placeholders. Those entries need your own values if you adapt the files.

Public upstream links and the original Mainsail attribution are preserved.

## Attribution and licensing

The bundled mainsail.cfg retains its original 2022 Alex Zellner copyright notice and GNU GPLv3 license notice. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for details and the included license text.

I haven't assigned an additional repository-wide license to the other files.
