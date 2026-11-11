# Human character and motion credits

`einstein-human.glb` uses Quaternius's **Universal Base Characters — Standard** male human mesh and **Universal Animation Library — Standard** motion clips. Both source packs declare **CC0 1.0 Universal**. The original license notices are preserved in `QUATERNIUS-BASE-LICENSE.txt` and `QUATERNIUS-ANIMATION-LICENSE.txt`.

## Official sources

- Base character: https://quaternius.itch.io/universal-base-characters
- Base description and license: https://quaternius.com/packs/universalbasecharacters.html
- Animation library: https://quaternius.itch.io/universal-animation-library
- Animation description and license: https://quaternius.com/packs/universalanimationlibrary.html
- CC0 text: https://creativecommons.org/publicdomain/zero/1.0/

Free Standard releases were downloaded directly from the author's itch.io download controls on September 14, 2026. No paid assets are included. Download archive hashes:

- Universal Base Characters[Standard].zip: `fdbf1804c90dfc1ea03e992bff7da2dfd1a79318e13270a660180f9308455f40`
- Universal Animation Library[Standard].zip: `cc73fc4e495b82958207316596317a3f40b9fa38065bde1027937452da537724`

## Processing

The human mesh is `Base Characters/Godot - UE/Superhero_Male_FullBody.gltf`. The motions come from `Unreal-Godot/UAL1_Standard.glb`, the author's version with root motion disabled. The library's jointed mannequin is not included.

Eight clips were sampled at 60 frames per second and retargeted to the human's original skeleton: `Idle_Loop`, `Jog_Fwd_Loop`, `Sprint_Loop`, `Jump_Start`, `Jump_Loop`, `Jump_Land`, `Roll`, and `Death01`. Both source rigs have the same 65 bone names, but different rest poses and bone lengths. Retargeting applies source-to-target world rest orientation corrections, retains target bone translations and scales, and transfers proportional pelvis motion. Original human geometry, skin weights, inverse bind matrices, materials, and textures are preserved. One source image URI ending in `_png.png` was resolved to the corresponding supplied `.png` file.

The result is a self-contained GLB with embedded textures; it does not fetch external resources. Model units, orientation, rest bone positions, world quaternions, clip names, and the generated asset SHA-256 are in `einstein-human.metadata.json`.

## Verification

The generated GLB was loaded in Three.js GLTFLoader and visually inspected in a sprint pose against the original animation. Every clip was sampled at 61 evenly spaced times; all resulting skinned vertex bounds were finite. The target's original limb lengths remain constant. Sprint and jog span ground levels within roughly one centimetre; the in-place jump clips need the game's jump displacement and contact handling. This inspection does not replace an in-game camera and transition review after costume integration.

Author: **Quaternius** — https://quaternius.com

The game's costume styling and Einstein-inspired accessories are separate from the source character.

## Startup packaging

`node scripts/prepare-startup-assets.mjs` removes the body's embedded normal and roughness PNGs, which the game's authored costume already disabled immediately after loading. Metallic factor is zero. Geometry, skin weights, animation clips, other materials and all retained texture bytes are unchanged; no visible detail is reduced. The model is 9,035,092 bytes instead of 16,440,468 bytes. Metadata retains the original source hash and size.

The same script emits `kerr-transfer-half.bin` from the original validated float32 geodesic map. Every half-float value is identical to the previous runtime conversion. Loading the packed map halves its input size and avoids repeating that conversion on the main thread. `build-black-hole.mjs` also emits both representations when regenerating the physics map. The original float32 data remains available for the physics validation suite.
