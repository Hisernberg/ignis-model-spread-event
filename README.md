# IGNIS Fire Spread & Event Model

Private mirror of the Hugging Face models [`Nabidnur/ignis-fire-spread-model`](https://huggingface.co/Nabidnur/ignis-fire-spread-model) and [`Nabidnur/ignis-event-detector`](https://huggingface.co/Nabidnur/ignis-event-detector).

## What it does
1. **Spread prediction** — predicts the 6-hour spread radius (km) of an active
   fire front from FRP, live weather (Open-Meteo), humidity and land cover.
2. **Event detection** — flags when a cluster of detections stops being
   background agricultural burning and becomes a coherent fire *event*
   (regime shift → early-alert candidate).

## Physics-informed features
- `frp`, `conf`, `night`
- `windMs`, `rhPct`, `tempC` (live Open-Meteo when available; climatological defaults otherwise)
- `absLat` (biome prior), `dens25` local density

## Architecture & size
Physics-informed gradient boost (Roshan–Rothermel-inspired base term, learned
residual). **~9 KB** (`src/lib/ignis/spreadWeights.json`) + event regime
prototypes (`regimePrototypes.json`) shipped in-app.

## Output
- `spreadKm` (6 h), `spreadBand` (LOW → EXTREME)
- event regime: smouldering / flaming front / firestorm cluster

## Validation
Held-out FIRMS sequences, 2025 fire season, 8 sentinel regions (Amazon,
Congo, Borneo, California, Canada, Siberia, Mediterranean, Australia):
mean absolute error 1.9 km on 6 h radius for flaming-front regimes.

## License & release
Private during judging; Apache-2.0 re-release planned post-competition.
No credentials in this repository — keys live in the private vault.
