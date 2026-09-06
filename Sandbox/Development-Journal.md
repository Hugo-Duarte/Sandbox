# Development Journal

## Session 2 — MonoGame Lifecycle and Controlled Defect

## Session 3 — Original Aseprite asset and crisp content pipeline

**Date:** 2026-09-06  
**Time spent:** 90 minutes

- .asesprite source is the editable version of a spripte in Aseprite while the PNG exports the file with the transparency properties that be imported using the MonoGame Content Manager.
- The MGCB allows us to import content to monogame projects and build it via an interface.
- Assets loaded through MonoGame’s Content Manager use their logical content-pipeline name without the source-file extension. MGCB converts the PNG into compiled XNB content, which the game loads as a Texture2D.
- Point smapling draws a texture withou anti aliasing keeping pixel art crisp, interger scaling allows increasing the size of a sprite by one pixel unit.
- The origin of any texture in monogame is set by default at (x = 0, y = 0) by altering the origin we can move this to the center of the sprite as we did in this case.