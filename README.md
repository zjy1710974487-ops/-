EMRI LISA SNR Analysis Pipeline
Figure-Oriented Implementation and Signal Comparison
Overview

This repository implements a numerical pipeline whose primary goal is to generate and compare figures.

The code constructs two signals:

ℎ
𝐵
(
𝑡
)
,
ℎ
𝑇
(
𝑡
)
h
B
	​

(t),h
T
	​

(t)

and focuses on visualizing their difference through multiple plots.

All computations are organized around answering one question:

How does a small modification in the evolution change the observable signal?
How does a small modification in the evolution change the observable signal?
What the Code Actually Computes

The pipeline performs the following steps:

Construct phase evolution 
Φ
(
𝑡
)
Φ(t)
Build waveform
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
Generate two versions:
baseline signal 
ℎ
𝐵
(
𝑡
)
h
B
	​

(t)
modified signal 
ℎ
𝑇
(
𝑡
)
h
T
	​

(t)
Compute residual
ℎ
𝑅
(
𝑡
)
=
ℎ
𝐵
(
𝑡
)
−
ℎ
𝑇
(
𝑡
)
h
R
	​

(t)=h
B
	​

(t)−h
T
	​

(t)
Transform signals to frequency domain
Produce plots comparing all three
Figures and Their Code Logic
1. Time-Domain Waveform Plot

Code operation

Compute 
ℎ
𝐵
(
𝑡
)
h
B
	​

(t) and 
ℎ
𝑇
(
𝑡
)
h
T
	​

(t) from the same amplitude
Only phase evolution differs
Subtract to obtain residual
ℎ
𝑅
(
𝑡
)
=
ℎ
𝐵
(
𝑡
)
−
ℎ
𝑇
(
𝑡
)
h
R
	​

(t)=h
B
	​

(t)−h
T
	​

(t)

What appears in the plot

Two almost overlapping oscillatory curves
A third curve (residual) with growing structure

What this means (from code perspective)

Since amplitude is almost unchanged,
the difference is driven entirely by phase
The longer the evolution,
the larger the misalignment becomes
2. Residual Evolution Plot

Code operation

Directly plots 
ℎ
𝑅
(
𝑡
)
h
R
	​

(t)

What appears

Oscillatory residual
Increasing envelope toward the end

What this means

ℎ
𝑅
(
𝑡
)
≈
2
𝐴
(
𝑡
)
sin
⁡
(
Δ
Φ
2
)
h
R
	​

(t)≈2A(t)sin(
2
ΔΦ
	​

)
Residual grows as phase difference accumulates
Not noise — fully deterministic from code
3. Frequency-Domain Spectrum

Code operation

Apply FFT:

ℎ
(
𝑡
)
→
ℎ
~
(
𝑓
)
h(t)→
h
~
(f)

Then compute magnitude

What appears

Baseline and modified spectra almost overlap
Residual spectrum localized

What this means

Code shows that global frequency content is preserved
Differences are subtle and structured
4. Characteristic Strain Plot

Code operation

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

What appears

Two main curves nearly identical
Residual curve significantly lower

What this means

Modification does not strongly change signal strength
Confirms difference is not amplitude-driven
5. Signal vs Detector Noise

Code operation

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


Plot 
ℎ
𝑐
(
𝑓
)
h
c
	​

(f) together with 
ℎ
𝑛
(
𝑓
)
h
n
	​

(f)

What appears

Signal intersects detector sensitivity band
Both signals detectable

What this means

Code verifies detectability condition
Modification does not push signal below noise
6. Numerical Comparison (No Plot but Derived from Data)

Code computes

Signal-to-noise ratio:

𝜌
=
(
ℎ
∣
ℎ
)
ρ=
(h∣h)
	​


Overlap:

𝑂
=
(
ℎ
1
∣
ℎ
2
)
(
ℎ
1
∣
ℎ
1
)
(
ℎ
2
∣
ℎ
2
)
O=
(h
1
	​

∣h
1
	​

)(h
2
	​

∣h
2
	​

)
	​

(h
1
	​

∣h
2
	​

)
	​


Mismatch:

𝑀
=
1
−
𝑂
M=1−O

Residual norm:

(
ℎ
𝑅
∣
ℎ
𝑅
)
1
/
2
(h
R
	​

∣h
R
	​

)
1/2

What this confirms

Signals are close in inner-product sense
Residual is still measurable
How All Figures Connect

From the code behavior:

Time-domain → shows phase drift
Residual → shows accumulated difference
Frequency-domain → shows small global deviation
Strain plot → shows amplitude similarity
Detector plot → shows detectability

Together they demonstrate:

phase modification
  
⟹
  
visible residual structure
phase modification⟹visible residual structure
Minimal Physical Interpretation (Only What Is Needed)

The only modification introduced in the code affects the phase evolution.

Since phase is integrated over time:

Δ
Φ
(
𝑡
)
=
∫
(
difference in evolution
)
 
𝑑
𝑡
ΔΦ(t)=∫(difference in evolution)dt

even a small local change produces a large global shift.

All figures are direct consequences of this accumulation.

How to Run

Install:

numpy
scipy
matplotlib

Run:

EMRI_LISA_SNR_paper_pipeline.ipynb

Execute cells sequentially.

Output

The code produces:

Time-domain waveform comparison
Residual evolution
Frequency spectra
Characteristic strain plots
Detector comparison plots

All outputs are directly generated from numerical arrays and require no external data.

Summary

This implementation is centered on visual evidence from plots.

The code shows that:

Signals can remain visually similar
Differences accumulate through phase
Residual becomes structured and observable

The conclusion is entirely supported by the figures produced by the pipeline.
