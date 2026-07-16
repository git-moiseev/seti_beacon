# Blind Detection Complexity as a Communication Resource

### Abstract

Classical communication theory optimizes signal design with respect to bandwidth, transmitted power, noise immunity, and channel capacity. These criteria implicitly assume that the receiver already knows the signaling protocol or can synchronize to it with negligible computational effort. This assumption is inappropriate for beacon transmissions intended for an unknown receiver. In such a scenario, the dominant limitation may not be channel capacity but the computational cost of blind signal detection.

### Blind Detection as a Search Problem

A receiver searching for an unknown transmission must explore a multidimensional hypothesis space. The unknown parameters typically include carrier frequency, bandwidth, Doppler shift, drift rate, symbol duration, modulation type, coding scheme, frame structure, synchronization sequence, repetition period, and numerous implementation-specific details.

The computational cost of detection is therefore proportional to the volume of this search space rather than to the received signal power alone.

From this perspective, the optimal beacon is the one that minimizes the receiver's search space.

### Design Implications

Several design principles follow immediately.

* A fixed carrier is preferable to frequency hopping because it eliminates an entire search dimension.

* A continuously transmitted signal is preferable to burst transmission because it allows arbitrarily long coherent integration without requiring the receiver to search for packet timing.

* A narrowband waveform is preferable to a wideband waveform because it concentrates energy into fewer spectral bins and reduces the computational burden of spectral analysis.

* If the objective is merely to announce the transmitter's existence, an unmodulated carrier is computationally optimal. Every additional layer of modulation, coding, or framing introduces new unknown parameters that must be searched.

* When information transfer is required, the transmitted waveform should reveal its own structure as early as possible through deterministic synchronization sequences or highly regular repetition patterns.

### A Different Optimization Criterion

These conclusions differ fundamentally from those of classical information theory.

Shannon's framework seeks waveforms that maximize reliable information throughput under constraints of bandwidth and signal-to-noise ratio. Blind beacon detection poses a different optimization problem: maximizing the probability that an uninformed receiver discovers the transmission with finite computational resources.

The relevant resource is therefore neither bandwidth nor power alone, but the amount of computation required before meaningful demodulation can even begin.

### Conclusion

For beacon systems intended for unknown observers, computational complexity should be regarded as a fundamental communication resource alongside bandwidth, transmitted power, and observation time.

Under this criterion, the optimal beacon is not necessarily the waveform that maximizes channel capacity. Instead, it is the waveform that minimizes the computational entropy of blind detection, allowing an uninformed receiver to identify its presence using the smallest possible search space.


## A Hierarchical Beacon Waveform

Assume that the receiver knows the nominal transmitter frequency $F_0$, but the actual Doppler shift is unknown. The receiver only knows that the Doppler offset is bounded,

$$
-d \leq \Delta f_D \leq d.
$$

Consequently, the initial detection stage consists of searching for excess signal energy within the frequency interval

$$
F_0-d \leq f \leq F_0+d.
$$

A conventional beacon would transmit a single carrier at $F_0$. While this minimizes the occupied bandwidth, it provides no information about the Doppler shift beyond the location of the detected spectral peak.

Instead, we propose transmitting two fixed frequencies symmetrically located around the nominal carrier,

$$
F_0-e
\qquad\text{and}\qquad
F_0+e,
$$

where

$$
0 < e < d.
$$

The receiver therefore observes

$$
f_- = F_0 + \Delta f_D - e,
$$

and

$$
f_+ = F_0 + \Delta f_D + e.
$$

The center frequency of the pair immediately provides an estimate of the Doppler shift,

$$
\Delta f_D =
\frac{f_-+f_+}{2}-F_0,
$$

while the spacing between the two carriers remains invariant,

$$
f_+ - f_- = 2e.
$$

The separation $2e$ therefore acts as an internal signature of the beacon, independent of Doppler.

### Multi-Stage Signal Discovery

The proposed waveform is intentionally designed to reveal its structure progressively as the receiver increases its computational effort.

During the initial search, the receiver employs a relatively coarse spectral resolution in order to minimize computational cost while scanning the entire Doppler uncertainty interval.

If the spectral resolution satisfies

$$
\Delta f_{\mathrm{FFT}} > 2e,
$$

the two carriers cannot be resolved individually. The beacon appears as a single narrowband source with continuous emission.

After detection, the receiver may increase the coherent integration time, improving the spectral resolution according to

$$
\Delta f_{\mathrm{FFT}} \approx \frac{1}{T}.
$$

Once

$$
T > \frac{1}{2e},
$$

the two carriers become distinguishable.

At this stage the receiver can estimate the Doppler shift directly from the midpoint of the frequency pair while simultaneously verifying the expected carrier separation.

Only after these parameters have been determined does the receiver proceed to recover the information encoded in the switching between the two frequencies.

Thus the receiver solves four progressively simpler problems rather than one highly multidimensional optimization problem:

1. Detect excess energy.
2. Resolve a symmetric carrier pair.
3. Estimate the Doppler shift.
4. Decode the transmitted information.

### Computational Implications

The essential feature of this waveform is that additional signal structure is hidden below the resolution of the initial detector.

The first detection stage requires no knowledge of symbol timing, modulation format, packet structure, or coding scheme. The receiver merely searches for a continuous narrowband energy excess.

Additional waveform complexity becomes visible only after the search space has already been dramatically reduced.

The beacon therefore minimizes the computational cost of blind detection while still providing deterministic information that simplifies synchronization and decoding.

Rather than eliminating signal complexity, the proposed design distributes it across successive stages of observation. Each stage exposes only the minimum amount of new information required for the next stage of processing.

This hierarchical disclosure of structure constitutes the central design principle of the proposed beacon architecture.

#### * An optimal beacon should not minimize signal complexity. It should minimize the complexity visible to the receiver at each stage of discovery.

---------------------------------

## Packet Inversion as a Power-Balancing Mechanism

An obvious concern with binary frequency selection is that an arbitrary message may contain unequal numbers of zeros and ones. Consequently, one carrier would accumulate more energy than the other, making the weaker spectral line more difficult to detect. A conventional solution is to employ a DC-balanced line code, ensuring an approximately equal number of zeros and ones over any sufficiently long interval. Such codes, however, introduce additional coding constraints and reduce the effective information rate. A simpler alternative is to exploit the repetitive nature of beacon transmissions.

Let the transmitted packet be

$$
P=(b_1,b_2,\ldots,b_N),
$$


where each bit selects one of the two beacon frequencies. Instead of repeatedly transmitting the identical packet, the transmitter alternates between the original packet and its bitwise complement,

$$
P,;\overline{P},;P,;\overline{P},\ldots
$$

where

$$
\overline{P}=(1-b_1,1-b_2,\ldots,1-b_N).
$$

Over every pair of consecutive transmissions, each information bit is sent exactly once on each carrier. Consequently, the accumulated energy of the two spectral lines is identical, regardless of the packet contents,

$$
E_- = E_+ = \frac{E_{\mathrm{total}}}{2}.
$$

This property is achieved without imposing any restrictions on the transmitted information and without sacrificing coding efficiency.

The packet inversion strategy also creates an additional deterministic feature that can aid synchronization after initial detection. Once the receiver has estimated the packet duration (T_P), the received signal satisfies

$$
x(t+T_P)\approx -x(t),
$$

while after two packet periods,

$$
x(t+2T_P)\approx x(t).
$$

Thus, the transmitted waveform possesses a characteristic two-period symmetry: every second repetition is identical to the first, whereas adjacent repetitions are complementary.

Importantly, this structure is invisible during the initial detection stage. The receiver first detects a continuous narrowband signal, then resolves the symmetric frequency pair, estimates the Doppler shift from the midpoint of the pair, and only afterwards exploits the alternating packet structure for synchronization and data recovery.

This illustrates the central principle of hierarchical beacon design: signal complexity is not eliminated but deliberately postponed. Each additional level of structure becomes observable only after the previous stage has reduced the receiver's uncertainty and computational search space.
