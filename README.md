# VehicleShootingAnywhere

A companion to Hunterz' **Vehicle Shooting** for DayZ: passengers can shoot from any seat of any
vehicle, DayZ Expansion helicopters included, with any firearm. Vehicle Shooting on its own only
allows pistols, and only in vehicles that use the vanilla seat animations.

It's a small script override: nothing of Vehicle Shooting is repacked.

## In game

- Any passenger seat (not the driver's) of any vehicle: cars, trucks, boats and the Expansion
  helicopters.
- Any firearm, not only pistols and revolvers.

## Requirements

- [Vehicle Shooting](https://steamcommunity.com/workshop/filedetails/?id=3436144357) (Hunterz & Dave)
- [Survivor Animations](https://steamcommunity.com/workshop/filedetails/?id=2918418331)
  (TheDaveCZE & Hunterz), which Vehicle Shooting needs

Server and client. Load it **after** Vehicle Shooting.

## For server owners

1. Put the mod in the server folder as `@VehicleShootingAnywhere`.
2. Add it to `-mod=` after Vehicle Shooting: `-mod=...;@SurvivorAnimations;@VehicleShooting;@VehicleShootingAnywhere`
3. Copy `@VehicleShootingAnywhere/keys/tarbaby.bikey` into the server's `keys/`.

Nothing to configure.

## How it works

`VehicleShootingAnywhere/Scripts/4_World/VehicleShootingAnywhere.c` overrides two of Vehicle
Shooting's checks on `PlayerBase`:

- `CanStartVehicleShooting`: any `CarScript` (Expansion's helicopters and boats are cars too),
  any seat but the driver's.
- `IsVehicleShootingWeapon`: any `Weapon_Base`.

## Layout

| Path | What |
|---|---|
| `VehicleShootingAnywhere/` | The mod (PBO prefix `VehicleShootingAnywhere`): config, script, Workshop description and preview |
| `CHANGELOG.md` | One entry per release; the entry is also the Workshop change note |

## Building and releasing

The mod is packed and signed (key `tarbaby`) by the DayZMissions tooling;
`DayZMissions/mods/VehicleShootingAnywhere` is a symlink to `VehicleShootingAnywhere/` here.

1. Add the version's entry to `CHANGELOG.md`, commit, tag and push:

   ```sh
   git tag -a v1.0.2 -m "VehicleShootingAnywhere 1.0.2"
   git push origin main v1.0.2
   ```

2. From DayZMissions, upload it yourself (SteamCMD asks for the password and a Steam Guard
   code; it knocks the desktop Steam client offline, so don't publish while playing):

   ```sh
   tools/workshop_publish.sh VehicleShootingAnywhere <steam login>
   ```

   The version comes from the tag, and that version's `CHANGELOG.md` entry becomes the change note.
   `VehicleShootingAnywhere/workshop.id` (the Workshop item id) is local only and git-ignored.

## Credits

Hunterz and Dave for Vehicle Shooting, which does all the real work; TheDaveCZE for Survivor
Animations; Helicopter Shooting Red Falcon for showing the same trick for RedFalcon helis.
