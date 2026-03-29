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

   h(t) = A(t) * cos(Φ(t)  

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

## Summary  

The code demonstrates that a small modification in the evolution leads to a growing phase difference.
While this difference is not immediately apparent in the amplitude, it becomes clearly visible through residuals and direct comparisons.