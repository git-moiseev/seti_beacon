# 3. Waveform Design Principles

The previous discussion suggests that the primary objective of waveform design is not to maximize information throughput, but to reduce the uncertainty presented to an uninformed receiver during blind detection.

This objective leads naturally to several design principles.

## 3.1 Continuous Transmission

The transmitter should emit continuously whenever possible.

Continuous transmission allows the receiver to integrate the received signal over an arbitrarily long observation interval, increasing detection sensitivity without requiring knowledge of packet timing.

Burst transmission introduces an additional unknown parameter—the temporal location of the transmission—which increases the search space.

## 3.2 Constant Transmitted Power

The transmitted power should remain constant throughout the observation interval.

Power variations introduce additional temporal structure that the receiver must either estimate or treat as uncertainty during detection.

Constant transmitted power also maximizes the average received energy for a given peak transmitter capability.

## 3.3 Narrow Occupied Bandwidth

The occupied bandwidth should be as small as permitted by the remaining design constraints.

A narrowband signal concentrates transmitted energy into fewer spectral bins, reducing both the frequency search space and the computational cost of spectral analysis.

Bandwidth should not be increased unless doing so simplifies a later stage of the detection process.

## 3.4 Deterministic Signal Structure

The transmitted waveform should avoid unnecessary randomness.

Pseudo-random spreading sequences, frequency hopping, and randomized packet scheduling are effective communication techniques when both transmitter and receiver share prior knowledge.

For blind detection, however, every unknown random component enlarges the hypothesis space.

Whenever possible, deterministic waveform structures should therefore be preferred.

## 3.5 Hierarchical Observability

Not every property of the transmitted waveform needs to be observable during the initial detection stage.

Instead, the waveform should reveal its internal structure progressively.

Each stage of observation should expose only the minimum additional information required for the receiver to proceed to the next stage of processing.

This principle separates the tasks of

- signal discovery,
- parameter estimation,
- synchronization,
- and information recovery,

allowing each stage to operate within a substantially smaller search space than would be required by a monolithic blind detector.

> In conventional communication systems, receiver algorithms are designed to recover a known waveform. In the proposed approach, the waveform itself is designed to simplify the receiver's blind search.

The following sections present a waveform architecture developed according to these principles.
