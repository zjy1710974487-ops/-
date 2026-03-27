EMRI LISA SNR Analysis Pipeline
First-Order Phase-Transition Effects in Kerr EMRIs

Scientific Context

This repository implements a computational pipeline corresponding to the analysis presented in the paper “Detectability and Systematic Bias from First-Order Phase-Transition Dephasing in Kerr EMRIs”. The project focuses on modeling gravitational wave signals from extreme mass-ratio inspirals (EMRIs) and studying the impact of a first-order phase transition in the dissipative flux sector.

Core Physical Idea

A localized modification in the inspiral flux produces a non-trivial observational regime characterized by small mismatch, order-unity residual, and large accumulated phase drift.

M << 1, ρ_R ~ 1, ΔΦ >> 1

The purpose of this repository is to numerically reconstruct and demonstrate this regime.

Repository Structure

The project consists of three main notebooks and supporting scripts.
EMRI_LISA_SNR_paper_pipeline.ipynb contains the full analysis pipeline.
research_notebook.ipynb focuses on exploratory analysis and visualization.
Untitled30.ipynb is used for auxiliary testing.
PostProcessingScripts.py provides reusable functions.

Workflow Overview
Inspiral Dynamics

The inspiral evolution is governed by the energy balance equation:

dE/dt = -F(v, a)

The inspiral clock is computed as:

dt/dv = -μ (dE/dv) / F(v, a)

Two branches are constructed:
Baseline flux F_B(v)
Transition-modified flux F_T(v)

Transition Sector

The phase transition is modeled as a smooth modification:

Λ(v) = Λ_H + (Λ_Q - Λ_H) S(x)

The modified flux is:

F_T(v) = F_B(v) * [1 + Λ(v) H_PT(v)]

Phase Evolution

dΦ/dt = 2Ω(v)

dΦ/dv = 2Ω(v) * dt/dv

ΔΦ = Φ_B - Φ_T

Benchmark result:

ΔΦ ~ 5 × 10^3 rad

Time-Domain Waveform

h(t) = A(t) cos(Φ(t))

Baseline waveform: h_B(t)
Transition waveform: h_T(t)
Residual:

h_R(t) = h_B(t) - h_T(t)

Frequency-Domain Analysis

h̃(f) = ∫ h(t) e^{-2πift} dt

Characteristic strain:

h_c(f) = 2f |h̃(f)|

Noise scale:

h_n(f) = sqrt(f S_n(f))

Detector Inner Product

(h1|h2) = 4 ∫ (h̃1 h̃2*) / S_n(f) df

Key Metrics

Signal-to-noise ratio:

ρ = sqrt((h|h))

Benchmark:

ρ_B ≈ 5.064
ρ_T ≈ 4.073
ρ_R ≈ 1.051

Mismatch:

M = 1 - Match

M ≈ 2.986 × 10^-3

Residual norm:

(δh|δh)^(1/2) ≈ 1

Key Result

The waveform remains detectable and highly overlapping, but accumulates a large phase deviation. The dominant effect is loss of faithfulness rather than loss of detectability.

How to Run

Install numpy, scipy, matplotlib.
Run EMRI_LISA_SNR_paper_pipeline.ipynb in Jupyter Notebook sequentially.

Benchmark Parameters

M = 2 × 10^5 M_sun
μ = 1.4 M_sun
a = 0.90
f ∈ [0.012, 0.021] Hz

Output

The pipeline produces waveform data, spectra, SNR diagnostics, and publication-quality figures suitable for PDF export.

Summary

A narrow phase transition in the inspiral flux produces a large coherent phase deformation while preserving high overlap, defining a bias-sensitive regime in gravitational-wave inference.
