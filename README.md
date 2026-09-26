# Orbit propagator

A numerical orbit propagator for Earth satellites, with an interactive 3D mission-analysis tool and a validated Python model.

**[Open the interactive version](https://claude.ai/artifact/SHksJrAqBrMAPhZBra9mQg)**

![Interactive orbit propagator showing a Molniya orbit](images/web.png)

## What it does

- Propagates any Keplerian orbit with two-body gravity, J2 oblateness and atmospheric drag (exponential atmosphere, co-rotating)
- Real epoch: Earth rotation from sidereal time, Sun position from almanac formulas
- Eclipse prediction (cylindrical shadow), shadow fraction per orbit and beta angle
- Ground station pass prediction (rise time, duration, peak elevation) with an elevation mask
- Orbital lifetime estimate under drag
- Hohmann transfer and combined plane change planner, with propellant mass from the rocket equation
- Live osculating elements, ground track, altitude and energy-error plots; ephemeris export to CSV

## Validation

Every result below is produced by the notebook, checked against an analytical answer.

| Check | Simulated | Expected |
|---|---|---|
| Energy drift, ISS orbit with J2, 1 day | 1.8 × 10⁻¹¹ | 0 (conserved) |
| ISS nodal precession (J2) | −4.98 °/day | −4.96 °/day (secular theory) |
| Sun-synchronous orbit, 700 km, 98.2° | +0.988 °/day | +0.984 °/day (secular theory) |
| Drag decay, 415 km, 100 kg / 1 m², 30 days | 8.47 km | 8.55 km (analytic ȧ = −ρB√(μa)) |
| LEO 300 km (28.5°) to GEO | 4.256 km/s | ≈ 4.25 km/s (textbook) |

![Python dashboard](images/dashboard.png)

## Files

- `orbit_propagator.ipynb`: physics, validation and analysis in Python (NumPy, SciPy DOP853 integrator, Matplotlib). Opens in Colab or VS Code.
- `orbit_propagator.py`: the same notebook as a plain script with `# %%` cells.
- `orbit_propagator.html`: the interactive version, a single self-contained file. Open it in any browser.

## Run it

```bash
pip install numpy scipy matplotlib ipywidgets
jupyter notebook orbit_propagator.ipynb
```

Or upload the notebook to Google Colab (File → Upload notebook).

## Limitations

This is a quick-look analysis tool, not operations-grade software.

- Earth orientation uses Greenwich mean sidereal time only (no precession, nutation or polar motion)
- Fixed exponential atmosphere, so no solar-cycle or space-weather variation; lifetimes are order-of-magnitude
- Only the J2 zonal harmonic; no third-body (Sun/Moon) or solar radiation pressure perturbations
- Cylindrical Earth shadow (no penumbra)

## Next steps

- Higher-order gravity (J3, J4) and Sun/Moon third-body perturbations
- TLE import with SGP4 for comparison against real satellites
- NRLMSISE-00 atmosphere with solar flux input

## About

Built by Hanaan Khan, MSc Space Science and Engineering (Space Technology), UCL. Developed with AI assistance; the physics was validated against analytical results as shown above.
