# Orbit propagator

An interactive 3D orbit propagator and mission-analysis tool for Earth satellites. It runs entirely in the browser from a single HTML file, with no install and no dependencies.

**[Open the live demo](https://hanaan64.github.io/orbit-propagator/)**

## What it does

- Propagates any Keplerian orbit with two-body gravity, J2 oblateness and atmospheric drag (exponential atmosphere, co-rotating with Earth), using a fourth-order Runge–Kutta integrator
- Uses a real epoch: Earth's orientation from sidereal time, and the Sun's position from almanac formulas
- Predicts eclipses with a cylindrical shadow model, giving the shadow fraction per orbit, the longest eclipse and the beta angle
- Predicts ground station passes (rise time, duration and peak elevation) above an elevation mask, for Goonhilly, Harwell, Kiruna, Svalbard or any custom location
- Estimates orbital lifetime under drag
- Plans Hohmann transfers with a combined plane change, including propellant mass from the rocket equation
- Shows live osculating elements, ground track, altitude and energy-error plots, and exports the ephemeris to CSV
- Includes presets for the ISS, a sun-synchronous orbit, a Molniya orbit and GEO

## Validation

The physics was checked against analytical results. Two of these checks run live in the tool: the energy-error readout, and the J2 node drift (theory vs simulated) in the left panel.

| Check | Simulated | Expected |
|---|---|---|
| Energy drift, ISS orbit with J2, 2 days | 5 × 10⁻⁹ | 0 (conserved) |
| ISS nodal precession (J2) | −4.97 °/day | −4.96 °/day (secular theory) |
| Sun-synchronous orbit, 700 km, 98.2° | +0.989 °/day | +0.984 °/day (secular theory) |
| Drag decay, 415 km, 100 kg / 1 m², 30 days | 8.47 km | 8.55 km (analytic ȧ = −ρB√(μa)) |
| ISS eclipse at beta ≈ 2° | 38.8 %, 36 min | ≈ 36 min (typical low-beta ISS eclipse) |
| LEO 300 km (28.5°) to GEO | 4.256 km/s | ≈ 4.25 km/s (textbook) |

## Run it

Open `index.html` in any modern browser, or use the live demo link above.

**Controls:** drag to rotate, scroll or pinch to zoom, Space to pause, R to restart.

## Limitations

- Earth orientation uses Greenwich mean sidereal time only (no precession, nutation or polar motion)
- The atmosphere is a fixed exponential model with no solar-cycle variation, so lifetimes are order-of-magnitude estimates
- J2 is the only gravity harmonic; there are no third-body (Sun/Moon) or solar radiation pressure perturbations
- The Earth's shadow is cylindrical (no penumbra)

## About

Built by Hanaan Khan
