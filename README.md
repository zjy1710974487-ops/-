# EMRI LISA SNR Analysis Pipeline  
Figure-Oriented Implementation and Signal Comparison  

## Overview  

This repository provides a numerical pipeline designed for figure generation and comparison.

The code constructs two signals,
h_B(t) and h_T(t),
and visualizes their differences through a series of plots.

The aim is to illustrate how a minor modification in the evolution impacts the observable signal.

---

## What the Code Does  

The pipeline performs the following steps:  

1. Compute phase evolution Φ(t)  
2. Construct waveform:  

   h(t) = A(t) * cos(Φ(t))  

3. Generate two signals:  

   baseline signal h_B(t)  
   modified signal h_T(t)  

4. Compute residual:  

   h_R(t) = h_B(t) - h_T(t)  

5. Transform all signals to the frequency domain. 
6. Generate comparison plots  

---

## Figures and Their Meaning  

### Time-Domain Waveform  

TThe code constructs h_B(t) and h_T(t) using the same amplitude but different phase evolution.

The plot displays:
two overlapping oscillatory signals
a residual signal

Interpretation:
The difference arises from phase misalignment, not amplitude variation.



---

### Residual Plot  

The code directly plots the residual:

h_R(t) = h_B(t) – h_T(t)
The resulting trace shows an oscillatory structure whose amplitude grows over time.

Interpretation:
The difference accumulates as the phase shift between the two signals increases with time.


---

### Frequency-Domain Spectrum  

The code applies a fast Fourier transform (FFT):

h(t) → h(f)

The resulting plot reveals:

- similar spectra for the two signals

- a residual that is localized in frequency

Interpretation:
The global frequency content remains largely unchanged, and the differences between the signals are subtle and confined to specific frequency bands.



---

### Characteristic Strain  

The characteristic strain is computed as:

h_c(f) = 2f · |h(f)|

The resulting plot shows nearly identical curves for the two signals.

Interpretation:
The overall signal strength remains almost unchanged.
---

### Detector Comparison  

The code computes detector scale and compares with signal.  

The plot shows both signals above noise level.  

Interpretation:  
Both signals are detectable.  

---

### Numerical Comparison  

The code computes the following metrics:

Signal-to-noise ratio (SNR)
Overlap
Mismatch
Residual norm

Interpretation:
While the signals appear similar, the quantitative measures confirm that they are not identical.



---

## Key Observation  

Across all figures, the results consistently show:

The two signals appear broadly similar.
The phase difference between them grows over time.
The residual exhibits a clear, structured form.
The signal remains detectable throughout.

---

## Code-to-Figure Implementation

The following sections explain how the code generates each figure and how the numerical steps correspond to the plots.

## Signal Construction

The code defines an amplitude $A(t)$ and computes two phase functions:
Φ_B(t) (baseline) and Φ_T(t) (modified).

The signals are constructed as:
h_B(t) = A(t)cos(Φ_B(t))

h_T(t) = A(t)cos(Φ_T(t))

Since both signals share the same amplitude, any difference comes from the phase.

## Time-Domain Plot

The code plots h_B(t) and h_T(t) on the same time grid.
It also computes the residual:

h_R(t) = h_B(t) - h_T(t)

All three curves are displayed together.

## Residual Plot

The residual h_R(t) is plotted separately.
Its structure reflects the accumulated phase difference over time.

## Frequency-Domain Spectrum

The code applies a Fast Fourier Transform:

h(f) = FFT[h(t)]

It then computes |h(f)| and plots the spectra of h_B, h_T, and h_R.

## Characteristic Strain

The characteristic strain is computed as:

h_c(f) = 2f |h(f)|

This is plotted for both signals.

## Detector Comparison

The detector noise curve is added as a function of frequency.
The code overlays the signal curves and the noise curve for comparison.

## Numerical Metrics

The code computes:

1. Signal-to-noise ratio (SNR)
2. Overlap
3. Mismatch
4. Residual norm

These are calculated using the waveform data.

## Implementation Summary

All figures are generated from:
1. Time array t
2. Phase functions Φ_B(t) and Φ_T(t)
3. Signals h_B(t) and h_T(t)

All plots are transformations of these quantities. The differences seen in the figures come directly from the phase modification.

## Summary  

The code demonstrates that a small modification in the evolution leads to a growing phase difference.
While this difference is not immediately apparent in the amplitude, it becomes clearly visible through residuals and direct comparisons.