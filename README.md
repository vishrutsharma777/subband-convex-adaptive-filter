# Subband Convex Combination of Adaptive Filters for Nonlinear System Identification

Advanced Signal Processing (IIT Gandhinagar), Assignment 4 — 2026.
Authors: **Vishrut Sharma** and **Vikash Kumar Sinha**.

A Simulink model that identifies an unknown nonlinear system by combining a linear and a
nonlinear adaptive filter, with **two-channel subband decomposition** to speed up convergence.

## The unknown system

Defined in a MATLAB Function block (`unknown_system`): a 5-tap FIR filter
w = [0.8, −0.4, 0.2, −0.1, 0.05] followed by a static nonlinearity, plus noise:

    y_lin = wᵀ x(n)
    d(n)  = y_lin + 0.2·sin(π·y_lin) − 0.1·cos(π·y_lin) + 0.0316·v(n),   v ~ N(0, 1)

(noise standard deviation 0.0316, i.e. −30 dB).

## The model

- The input and the desired signal are split into two bands with two-channel analysis subband filters.
- A **linear** adaptive filter (LMS) and a **nonlinear** branch produce `y_linear` and `y_nonlinear`.
- An adaptive mixing parameter **λ** forms the convex combination
  `y_overall = λ·y_linear + (1 − λ)·y_nonlinear`, updated from the overall error.
- The model logs `y_overall`, `λ` and the overall squared error (MSE in dB, smoothed with a moving average).

## Files

| File | What |
| --- | --- |
| `ASPA4.slx` | Simulink model |

## Requirements

MATLAB/Simulink with the DSP System Toolbox (LMS Filter, Two-Channel Analysis Subband Filter,
Lowpass Filter and Moving Average blocks).
