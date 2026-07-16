# 1. Introduction

Classical communication theory optimizes transmitted waveforms with respect to bandwidth, transmitted power, spectral efficiency, bit error rate, and channel capacity. These optimization criteria implicitly assume that the receiver possesses sufficient a priori knowledge of the transmitted waveform to perform synchronization and demodulation.

This assumption is not universally valid.

Consider a transmitter intended to be discovered by a receiver that has no prior knowledge of the signaling protocol. The receiver knows only

- the nominal carrier frequency $F_0$, and
- an upper bound on the possible Doppler frequency offset $d$.

All remaining signal parameters are unknown, including modulation, coding, symbol rate, packet structure, synchronization method, and transmission protocol.

Under these conditions, successful communication becomes a two-stage problem.

The receiver must first determine that an artificial transmission is present before attempting synchronization and information recovery. The computational effort required for this blind detection stage may dominate the overall complexity of reception.

Consequently, the waveform should not be optimized solely for communication efficiency after synchronization has been achieved. It should also minimize the computational effort required for its own discovery.

This observation introduces an additional optimization criterion beyond the classical metrics of communication theory: **blind detection cost**.

The objective of this work is therefore not to maximize channel capacity or spectral efficiency, but to investigate waveform design principles that minimize the computational cost of blind detection by an uninformed receiver.

The proposed approach is based on a simple principle:

> A transmitted waveform should reveal its internal structure progressively, exposing only the minimum information required for the receiver to complete each successive stage of detection.

Rather than minimizing the intrinsic complexity of the transmitted signal, the proposed approach minimizes the complexity visible to the receiver during each stage of observation.
