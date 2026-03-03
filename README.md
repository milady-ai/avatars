# milady-ai/avatars

VRM avatars, backgrounds, previews, and animations for [milady-ai/milady](https://github.com/milady-ai/milady).

## Structure

```
vrms/
  milady-{1..24}.vrm          # Community avatars
  milady-official-{1..8}.vrm  # Official milady avatars
  shaw.vrm                    # Named avatar (Shaw)
  shaw.jpg                    # Shaw thumbnail (legacy)
  imported-avatars.json        # Manifest: index → filename, preview, label
  previews/                    # Thumbnail images for avatar selection UI
    milady-{1..24}.png
    milady-official-{1..8}.png
    shaw.jpg
  backgrounds/                 # Companion view background images
    milady-{1..24}.png
    milady-official-{1..8}.png
    shaw.png

animations/
  idle.glb                     # Default idle animation
  Idle.fbx                     # Idle (FBX format)
  BreathingIdle.fbx            # Breathing idle animation
  Standing Greeting.fbx        # Greeting animation
  emotes/                      # In-app emote animations (GLB)
    chopping.glb, crawling.glb, crying.glb, dance-breaking.glb,
    dance-happy.glb, dance-hiphop.glb, dance-popping.glb, death.glb,
    fall.glb, firing-gun.glb, fishing.glb, flip.glb, float.glb,
    hook-punch.glb, idle.glb, jump.glb, kiss.glb, looking-around.glb,
    punching.glb, range.glb, rude-gesture.glb, run.glb, sorrow.glb,
    spell-cast.glb, squat.glb, sword_swing.glb, talk.glb, walk.glb,
    waving-both-hands.glb
  mixamo/                      # Mixamo expression animations (FBX)
    Acknowledging.fbx, Agreeing.fbx, Angry.fbx, Bashful.fbx, ...
    (37 files total)
```

## Avatar Indexing

The app resolves avatars by numeric index (see `AppContext.tsx`):

| Index | File Pattern | Count |
|-------|-------------|-------|
| 1–24 | `milady-{N}.vrm` | 24 community avatars |
| 25–32 | `milady-official-{N-24}.vrm` | 8 official avatars |
| 33 | `shaw.vrm` | Named avatar |
| 0 | Custom upload | User-uploaded VRM via `/api/avatar/vrm` |

Each avatar has a corresponding **preview** (thumbnail for UI) and **background** (companion view backdrop) image at the same relative path under `vrms/previews/` and `vrms/backgrounds/`.

## Usage in milady app

Files from this repo are placed in `apps/app/public/` with the same directory structure:

```
apps/app/public/
  vrms/          ← vrms/ from this repo
  animations/    ← animations/ from this repo
```

The `imported-avatars.json` manifest maps each avatar index to its filename, preview image, and display label.

## Adding a New Avatar

1. Add the `.vrm` file to `vrms/` (e.g., `milady-25.vrm`)
2. Add a preview thumbnail to `vrms/previews/` (e.g., `milady-25.png`)
3. Add a background image to `vrms/backgrounds/` (e.g., `milady-25.png`)
4. Update `imported-avatars.json` with the new entry
5. Update `BASE_VRM_COUNT` in `apps/app/src/AppContext.tsx` in the main repo
