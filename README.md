# Miker's Melee Buff - v1.0.0-test1

**Do not use this mod in public.**
Use only in private sessions with friends who agree to these changes.

| Setting | Original profile | Modified |
|---|---:|---:|
| Standard damage | 75 | 1000 |
| Durable damage | 8 | 800 |
| Demolition | 10 | 50 |
| Stagger | 25 | 50 |
| Push | 30 | 100 |
| Direct penetration | 2 (Light) | 6 (Anti-Tank II) |

The four penetration fields become 6/0/0/0: direct melee penetration increases;
the other three fields retain the supplied default melee profile's zeros.

## Scope and limitations
Targets the supplied mod's scan-identified default Helldiver melee DamageSettings
profile (ID 548). It does not blanket-edit every damage row with similar numbers.
Dedicated melee weapons may use other profiles and are not covered automatically.
Any attack sharing ID 548 inherits these changes. The original package does not
prove that the Helmet Durability Check emote uses this profile.

These are base profile values. Actual damage and reactions still depend on hit
location, target rules, and other game modifiers. Stagger/push numbers do not
promise that every enemy will stagger or move, and demolition 50 does not
promise that every structure can be destroyed by a melee hit.

## Installation
1. Close the game. Disable/remove Helmet Durability Check Demo 20 and any other
   mod that edits the same default-melee profile.
2. Import this ZIP into your mod manager, enable its one option together with
   Bingus Shared Loader v15+ / API 1, then Purge / Deploy.
3. Start the game and test in a private mission.

The original manager GUID and resource path are retained so this replaces the
supplied mod. A profile already changed by the old Demo 20 mod is deliberately
refused; restart with only this version enabled.

## Verification
Look at:
`%LOCALAPPDATA%\CowboyBingus\Helldivers2\MikerMeleeBuff\STATUS.txt`

Success reports damage 1000/800, AP6, demolition/stagger/push 50/50/100.
If it cannot find a matching profile, send STATUS.txt for diagnosis. Do not
change the guard values merely to force a match after a game update.

## Further tuning
`Source/melee_buff.lua` contains the TARGETS table near the top. Edit only the
`target_damage`, `target_durable`, `target_demolition`, `target_stagger`,
`target_push`, and `target_ap` entries for desired values. The other entries
are the original-profile guard. Rebuild the patch after editing source; this
reference source file is not loaded directly by the game.

## Uninstall
Disable/remove the mod, Purge / Deploy, and restart the game. Changes live in
process memory. Disabling a package does not undo an already-running patch
until that game process exits.

## Credits
Based on the supplied Helmet Durability Check - 20 Demolition Force package
and its embedded reference table / memory scanning implementation.
CowboyBingus: Bingus Shared Loader and addon packaging tools.
Miker: requested tuning and edition.
ChatGPT/Codex: implementation and offline validation.

## Validation and build
Offline Lua 5.4 tests passed using synthetic records populated from the supplied
649-row reference: dynamic offset discovery, unique/ambiguous selection,
requested values, idempotence, full-record preservation, partial write and
exception rollback, read-back failure rollback, read-only and changed-profile
refusal. Run `lua Tests/test.lua` from the extracted package directory.
Windows LuaJIT/FFI startup and live game behavior have not been tested here.

Build Source/melee_buff.lua with BingusSharedLoader/scripts/build_addon.py:
resource `mods/codex/helmet_durability_demo20`, GUID
`770fef04-6a51-4514-b807-3294288b4497`. Retain these identities for updates.
