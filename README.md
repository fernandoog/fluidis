# FLUIDIS

Curl-noise feedback fluid for [KodeLife](https://hexler.net/kodelife) — real-time GPU compute shader.

Iridescent dye advected through an incompressible velocity field (curl of FBM), with mouse injection and soft vorticity ribbons.

## Open in KodeLife

1. Install [KodeLife](https://hexler.net/kodelife)
2. **File → Open** → `kodelife/FLUIDIS_COMPUTE.klproj`
3. Select the **FluidCS** compute pass (output is the compute pass)
4. Move the mouse over the preview to stir the fluid

Requires OpenGL 4.5+ (compute shaders + `imageLoad` / `imageStore`).

## Layout

```
fluidis/
├── kodelife/
│   ├── FLUIDIS_COMPUTE.klproj   # open this
│   ├── FLUIDIS_COMPUTE.xml      # uncompressed project
│   └── fluidis_compute.comp
└── src/
    └── fluidis.comp             # same compute source, plain GLSL
```

## How it works

- **Velocity** — analytic curl of multi-octave value noise (divergence-free)
- **Advection** — semi-Lagrangian sample of `prevFrame` along the flow
- **Dye** — mouse injector + orbiting emitters, teal→gold palette
- **Dispatch** — 160×90 groups × 8×8 threads → 1280×720

Uniforms: `time`, `resolution`, `mouse`, `spectrum` (KodeLife built-ins).

## License

MIT
