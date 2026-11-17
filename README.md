# Snowcat

A drivable snowcat for Jibbers (a C# mod for the [Jibbers Mod Loader](https://github.com/jaxoncarelos/JibbersModLoader)).

- **Bring it and drive it:** `B` brings a snowcat in front of you, `F` gets in and out. Drive with `W`/`S`, `A`/`D` and `Space`. It follows the ground and tilts over the slopes, and its tracks run.
- **The blade:**
  - `G` raises and lowers it, smoothly.
  - Hold `Z`/`C` to angle it left or right, and `Q`/`E` to tilt it. `H` straightens it.
  - It pushes the snow it cuts into a ridge ahead and berms off its ends, and the snow follows the blade's angle and tilt.
- **The tiller:** `T` lowers it onto the snow behind to groom the slope.
- **Settings:**
  - raised and lowered heights for the blade and the tiller
  - push and grooming strength
  - how far the blade angles and tilts, and how fast it all raises and lowers
  - the camera distance
  - every key
- **Night:** `L` turns on the headlights.
- **Friends:**
  - Everyone with Snowcat on your server sees each other's snowcats, found through a shared Steam lobby (no party needed). Riders on other servers of the same map are told apart by where their drivers are.
  - Walk up to a friend's snowcat and press `F` to ride along as a passenger.
- **Undo:** `U` takes back your last run of pushing and grooming, for everyone.
- **Admin reset:** `K` opens a password box, and an admin can then reset the slopes for everyone. Only a salted SHA-256 fingerprint of the password is kept, in `JibbersMods\snowcat_admin.txt`. Other players need that file for their game to accept the resets.
- **Controller:** `Y` in/out, `RT`/`LT` gas and reverse, left stick to steer, `B` brake, `X` blade, D-pad down tiller, D-pad left/right to angle, `LB`/`RB` to tilt.

## Source

- `Snowcat/`:
  - `SnowcatMod.cs` is the mod.
  - The pure logic, with no game calls and tested: `Drive` (driving over the ground), `Plow` (blade and tiller), `Parts` (bending the blade and tiller off the one-piece model), `Belt` (the tracks), `Wire` (messages to other players).
  - `Integration/` talks to the game: the snowcat's look, the Steam lobby, the password box.
  - `Shared/` holds code shared with the Chair Lift and Snow Shovel mods: holding a rider in a seat, finding riders, meshes and materials, editing the terrain, and Steam messages.
- `Snowcat/Packed/`: the model and images. The catalog builds mods from code only, so they travel as base64 text. The model is a deflated binary mesh, already turned into Unity's frame, and the images are the original JPEG and PNG files. `PackedAssets.cs` unpacks them.
- `Snowcat.Tests/`: the tests.

The snow is the map's own terrain, reshaped. Each player's game reshapes its own copy as the snowcats work: nothing is sent to the game server, and players without the mod see the slope as it was.

## License

GPL-3.0-only (see `LICENSE`). The snowcat model and textures are by the author and are included under the same license.
