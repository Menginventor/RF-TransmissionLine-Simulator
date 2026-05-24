# RF Line Simulator

A browser-based RF transmission line simulator implemented as a single-page static HTML app.

Live demo: https://menginventor.github.io/RF-Line-Simulator/

## Overview

This project visualizes a lossless 50-ohm transmission line using both analytical and Yee-grid RK4 numerical simulation modes.

Features:
- Analytical phasor solver for forward/reflected waves
- Yee-grid RK4 time-domain simulation with voltage nodes and staggered current edges
- Configurable source frequency, line velocity factor, electrical length, and load impedance
- Predefined load presets: matched, open, short
- Real-time voltage and current waveform rendering
- Readouts for physical length, electrical length, reflection coefficient magnitude, and VSWR

## Usage

1. Open `index.html` in a modern web browser.
2. Adjust the controls in the sidebar:
   - `f0` reference frequency
   - `f` drive frequency
   - velocity factor
   - line length in wavelengths
   - load resistance and reactance
3. Switch between `Analytical` and `Yee Grid RK4` modes.
4. Use `Reset` to restart the numeric simulation and `Pause` to freeze the animation.

## Simulation Modes

### Analytical

- Uses a closed-form phasor solution for lossless wave propagation on a uniform transmission line.
- Calculates forward and reflected voltage/current waves along the line.
- Uses the load impedance and characteristic impedance to compute the complex reflection coefficient.
- Displays instantaneous voltage and current traces from the resulting phasor at the chosen drive frequency.
- Best for understanding steady-state behavior and impedance matching.

### Yee Grid RK4

- Uses a fourth-order Runge-Kutta integrator on a Yee-style spatial grid.
- Stores voltage at nodes `V[k]` and current on staggered edges `I[k+1/2]`, so the numeric line is laid out as `V0 -- I0 -- V1 -- I1 -- V2`.
- Advances edge currents from adjacent node-voltage differences and node voltages from neighboring edge-current differences.
- Supports resistive, inductive, and capacitive load conditions with explicit time-domain dynamics.
- Allows changing the number of Yee cells to trade off between accuracy and performance.
- Best for observing transient wave propagation, reflections, and dynamic behavior.

## Notes

- The simulator assumes a 50-ohm characteristic impedance (`Z0 = 50 ohm`).
- In numerical mode, element count can be changed to improve fidelity.
- The `Open` preset simulates a very large resistance load, while `Short` sets the load to zero impedance.

## License

This repository includes a `LICENSE` file.
