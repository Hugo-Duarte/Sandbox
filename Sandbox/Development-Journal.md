# Development Journal

## Session 2 — MonoGame Lifecycle and Controlled Defect

**Date:** 2026-09-05  
**Time spent:** 30 minutes

### Lifecycle observations

The observed execution order was:

1. The `Game1` constructor
2. `Initialize`
3. `LoadContent`
4. `Update`
5. `Draw`

The constructor, `Initialize`, and `LoadContent` executed only once.

`Update` and `Draw` executed repeatedly as part of MonoGame's underlying game loop.

### Game-time observations

`ElapsedGameTime` represents the amount of simulated time associated with the current loop step. It returns to a small frame-sized duration on each iteration rather than accumulating.

`TotalGameTime` represents the accumulated simulated time since the game started and continues increasing during the run.

### Call-stack observations

The Update and Draw call stacks appeared similar. Both methods were invoked through MonoGame's underlying framework loop rather than through separate loops created by the game.

### Controlled-defect investigation

#### Prediction

- **Would compilation succeed?** I predicted that it would not.
- **When would it fail?** I predicted that it would fail during initialisation.
- **What would be unavailable?** I expected graphics drawing to be unavailable.

#### Actual result

Compilation succeeded, but the application failed at runtime during the startup process.

- **Exception type:** `System.InvalidOperationException`
- **Exception message:** `No Graphics Device Service`
- **Relevant framework method:** `Microsoft.Xna.Framework.Game.get_GraphicsDevice()`
- **Visible location:** `Program.cs`, line 2

#### Root cause

The `GraphicsDeviceManager` had deliberately not been created. Therefore, MonoGame did not have a registered graphics-device service when it attempted to access `GraphicsDevice`.

The exception became visible at line 2 of `Program.cs` because it propagated back through the operation that started and ran the game. That line was not the original cause of the invalid state.

This demonstrated that compilation can succeed even when a service required at runtime has not been configured.

### Restoration

The graphics-manager creation was restored. The application was tested again and launched normally with F5.

### Remaining uncertainties

None at present.