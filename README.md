EMRI LISA SNR Analysis Pipeline
First-Order Phase-Transition Effects in Kerr EMRIs
Scientific Context

This repository implements a complete computational pipeline corresponding to the analysis presented in:

“Detectability and Systematic Bias from First-Order Phase-Transition Dephasing in Kerr EMRIs”

The goal of this project is to numerically construct, analyze, and visualize gravitational waveforms from Kerr extreme mass-ratio inspirals (EMRIs), with a particular focus on:

First-order phase-transition (FOPT) effects in the dissipative sector
Accumulated waveform dephasing
Detector-weighted diagnostics in the LISA framework
Bias-sensitive regimes in gravitational-wave inference

The implementation follows the exact structure of the paper:

Inspiral modeling (Sec. II)
Data analysis framework (Sec. III)
Numerical results and diagnostics (Sec. IV)
Core Idea

A localized modification in the inspiral flux (caused by a phase transition) produces:

Small mismatch
Order-unity residual
Large accumulated phase drift

This defines the key observational regime:

Mismatch  ≪ 1
Residual  ~ 1
ΔΦ        ≫ 1

This repository reproduces this regime numerically.

Repository Structure
.
├── EMRI_LISA_SNR_paper_pipeline.ipynb
├── research_notebook.ipynb
├── Untitled30.ipynb
├── PostProcessingScripts.py
└── README.md
Workflow Overview

The pipeline strictly follows the physical logic of the paper.

1. Inspiral Dynamics (Sec. II)

The evolution is driven by the balance equation:

𝑑
𝐸
𝑑
𝑡
=
−
𝐹
(
𝑣
,
𝑎
^
)
dt
dE
	​

=−F(v,
a
^
)

Code implementation:

Computes orbital energy 
𝐸
(
𝑣
)
E(v)
Computes derivative 
𝑑
𝐸
/
𝑑
𝑣
dE/dv
Evolves inspiral using:
dt/dv = - μ (dE/dv) / F

Two branches are constructed:

Baseline: FB(v)
Transition-modified: FT(v)
2. Transition Sector

The phase transition is modeled as a smooth finite-width modification:

Λ
(
𝑣
)
=
Λ
𝐻
+
(
Λ
𝑄
−
Λ
𝐻
)
𝑆
(
𝑥
)
Λ(v)=Λ
H
	​

+(Λ
Q
	​

−Λ
H
	​

)S(x)

with smoothstep interpolation.

Code behavior:

Defines transition window in frequency
Applies correction:
FT = FB * (1 + Λ(v) * H_PT(v))

This is the only place where new physics enters.

3. Phase Evolution

Phase is accumulated through:

𝑑
Φ
𝑑
𝑣
=
2
Ω
𝑑
𝑡
𝑑
𝑣
dv
dΦ
	​

=2Ω
dv
dt
	​


Numerical integration produces:

Φ_B(t) baseline phase
Φ_T(t) transition phase

The key observable:

ΔΦ = Φ_B - Φ_T

In the benchmark:

ΔΦ ~ 5 × 10^3 rad
4. Time-Domain Waveforms

Waveforms are constructed as:

ℎ
(
𝑡
)
=
𝐴
(
𝑡
)
cos
⁡
(
Φ
(
𝑡
)
)
h(t)=A(t)cos(Φ(t))

Generated signals:

Baseline signal h_B
Transition signal h_T
Residual signal h_R = h_B - h_T

Important property:

Residual is dominated by phase slippage, not amplitude difference.

5. Frequency-Domain Analysis

FFT is applied:

h(t) → h̃(f)

Characteristic strain:

ℎ
𝑐
(
𝑓
)
=
2
𝑓
∣
ℎ
~
(
𝑓
)
∣
h
c
	​

(f)=2f∣
h
~
(f)∣

Compared against LISA sensitivity:

ℎ
𝑛
(
𝑓
)
=
𝑓
𝑆
𝑛
(
𝑓
)
h
n
	​

(f)=
fS
n
	​

(f)
	​

6. Detector-Weighted Quantities (Sec. III)

Inner product:

(
ℎ
1
∣
ℎ
2
)
=
4
∫
ℎ
~
1
ℎ
~
2
∗
𝑆
𝑛
(
𝑓
)
𝑑
𝑓
(h
1
	​

∣h
2
	​

)=4∫
S
n
	​

(f)
h
~
1
	​

h
~
2
∗
	​

	​

df

Computed metrics:

SNR
ρ_B ≈ 5.064
ρ_T ≈ 4.073
ρ_R ≈ 1.051
Mismatch
M ≈ 2.986 × 10^-3
Residual Norm
(δh | δh)^(1/2) ≈ 1

These match the paper exactly .

Generated Figures

The pipeline reproduces all key figures in the paper:

Global diagnostics
Transition function Λ(f)
Phase drift ΔΦ(f)
Time-domain residual
Frequency-domain strain
Time-domain comparison
Baseline vs transition vs residual
Frequency-domain structure
Characteristic strain vs LISA noise
Parameter sensitivity (optional)
Fisher bias
Intrinsic refitting mismatch maps
Key Result Interpretation

The code demonstrates a non-trivial regime:

Waveforms remain detectable
Overlap remains high
Phase evolution is strongly deformed

Conclusion:

The dominant effect is not loss of detectability, but loss of faithfulness.

This is the central statement of the paper .

How to Run
Ensure Python environment:
numpy
scipy
matplotlib
Start Jupyter:
jupyter notebook
Run:
EMRI_LISA_SNR_paper_pipeline.ipynb

Execution must be sequential.

Output

The pipeline generates:

Time-domain waveforms
Frequency-domain spectra
SNR and mismatch diagnostics
Publication-quality figures

All figures are designed for:

Direct paper inclusion
Vector format export (PDF recommended)
Reproducibility

To reproduce the benchmark:

Mass: 
𝑀
=
2
×
10
5
𝑀
⊙
M=2×10
5
M
⊙
	​

Secondary: 
𝜇
=
1.4
𝑀
⊙
μ=1.4M
⊙
	​

Spin: 
𝑎
^
=
0.90
a
^
=0.90
Transition window: 
𝑓
∈
[
0.012
,
0.021
]
f∈[0.012,0.021] Hz

These parameters are hard-coded in the main notebook.

Extension Directions

The current implementation is a controlled phenomenological model.

Future improvements:

Teukolsky-based flux instead of PN approximation
Self-force corrections
Multi-mode waveform (beyond (2,2))
Bayesian inference instead of Fisher approximation
Parameterized transition sector in waveform templates
Usage Context

This repository is intended for:

EMRI waveform modeling studies
LISA data analysis methodology
Undergraduate and early-stage research
Preparation of academic presentations
Summary

This codebase is not a generic simulation.

It is a direct computational realization of a specific physical result:

A narrow phase transition in the inspiral flux produces a large coherent phase deformation without significantly degrading waveform overlap.

Everything in this repository is built to demonstrate that statement quantitatively.
