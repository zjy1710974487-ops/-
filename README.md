# EMRI LISA SNR Analysis Pipeline  
Figure-Oriented Implementation and Signal Comparison  

## Overview  
This repository implements a numerical pipeline focused on generating and comparing figures.  

The code constructs two signals:  
h_B(t) and h_T(t)  

and visualizes their difference across multiple plots.  

The goal is to show how a small modification in the evolution affects the observable signal.  

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

5. Transform signals to frequency domain  
6. Generate comparison plots  

---

## Figures and Their Meaning  

### Time-Domain Waveform  

The code computes h_B(t) and h_T(t) using the same amplitude but different phase.  

The plot shows:  
- two overlapping oscillatory signals  
- a residual signal  

Meaning:  
The difference is caused by phase misalignment, not amplitude.  

---

### Residual Plot  

The code directly plots:  

h_R(t) = h_B(t) - h_T(t)  

The plot shows oscillatory structure increasing over time.  

Meaning:  
The difference accumulates due to phase shift.  

---

### Frequency-Domain Spectrum  

The code applies FFT:  

h(t) → h(f)  

The plot shows:  
- similar spectra for both signals  
- localized residual  

Meaning:  
Global frequency content is preserved, differences are subtle.  

---

### Characteristic Strain  

Computed as:  

h_c(f) = 2f * |h(f)|  

The plot shows nearly identical curves.  

Meaning:  
Signal strength remains almost unchanged.  

---

### Detector Comparison  

The code computes detector scale and compares with signal.  

The plot shows both signals above noise level.  

Meaning:  
Both signals are detectable.  

---

### Numerical Comparison  

The code computes:  

SNR  
Overlap  
Mismatch  
Residual norm  

Meaning:  
Signals appear similar but are not identical.  

---

## Key Observation  

All figures consistently show:  

- signals look similar  
- phase difference grows  
- residual is structured  
- signal remains detectable  

---

## Summary  

The code demonstrates that a small change in evolution leads to a growing phase difference.  

This difference is not obvious in amplitude but becomes visible through residuals and comparisons.  
