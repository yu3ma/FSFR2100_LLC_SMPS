# FSFR2100_LLC_SMPS
LLC resonant half-bridge isolated 200W Switched Mode Power Supply based on Fairchild's (now On Semiconductors) FSFR2100XS power controller.

This repository include design files, shematic and single-layer PCB films for DIY high power high quality resonant AC/DC converter.

Forum discussion: http://forum.yu3ma.net/showthread.php?tid=10

##Introduction

The popularity of the LLC resonant converter in its half-bridge implementation is due to its high-efficiency, low level of EMI emissions and its ability to achieve high power density. These features fit the demands of many modern applications. LLC resonant half bridge converters are widely used in consumer electronics, like powering the display panel of LCD TV. 

##FHA circuit model 

The FHA (First Harmonic Approximation) approach is based on the assumption that the power transfer from the source to the load through the resonant tank is almost completely associated to the fundamental harmonic of the Fourier expansion of the currents and voltages involved. This is consistent with the selective nature of resonant tank circuits. 
The harmonics of the switching frequency are then neglected and the tank waveforms are assumed to be purely sinusoidal at the fundamental frequency: This approach gives quite accurate results for operating points at and above the resonance frequency of the resonant tank (in the continuous conduction mode), while it is less accurate, but still valid, at frequencies below the resonance (in the discontinuous conduction mode). 
Good and properly constructed LLC works with basic harmonic of about 100KHz, has a very low content of other harmonics, sinusoidal current fed your transformer and output diode, has drastically lower dU and dI / dT of comparable hard switching topologies, minimal "ringing ", ie. generally speaking very "clean" waveform that is easy to filter.

##Operation under overload and short-circuit condition 

An important aspect to analyze is the converter's behavior during output overload and/or short-circuit. 

Unlike the hard switching there is immunity to impact loads being uninterruptedly repeated.
This in turn means that the required rated output of LLC = amplifier power / efficiency amplifiers + 20% obtained.
LLC converters can easily within a half-wave, for example - the bass tone on the amplifier, take load that is 50% higher than the declared and without any damage during the entire  life cycle of the device. 

Also, LLC of 180W has the same potential as the hard switching of 250W for use in an amplifier, and this is because of its principle of operation which allowed current limit that can be longer in time.
Limiting the minimum operating frequency is effective in preventing capacitive mode operation only if the minimum (normalized) frequency value is greater than 1. This suggests that, in response to an overload/short-circuit condition at the output, the converter operating frequency must be pushed above the resonance frequency (it is better if well above it) in order to decrease power throughput. 
It is worth noticing that, if the converter is specified to deliver a peak output power (where output voltage regulation is to be maintained) greater than the maximum continuous output power for a limited time, the resonant tank must be designed for peak output power to make sure that it will not run in capacitive mode. Of course, its thermal design will consider only the maximum continuous power. 
In any case, whatever the converter specified, short-circuit conditions or, in general, overload conditions exceeding the maximum specified for the tank circuit, need to be handled with additional means, such as a current limitation circuit. 

##Technical Specifications

The converter specification data are the following: 

- Nominal input voltage: 325VDC (230VAC)
- Maximal input voltage: 355VDC (250VAC)
- Minimal input voltage: 295VDC (210VAC)
- Brown-out: 260VDC (184VAC)
- Output voltage 1: +/-28V 3A
- Output voltage 2: +/-14V 1A
- Resonance frequency: 85 kHz 
- Max operating frequency: 250 kHz 

##Operation and Design

LLC converter belongs to the SRC (serial resonant converter) series, where the resonant network is established with two inductors and a capacity on the primary side of the converter (hence LLC). 

This can be accomplished with a simple SMPS (Switched Mode Power Supply) transformer station with external inductance as  Ls (where this is much easier to be done on the secondary side of the transformer), but integrated structure has some noticeable advantages regarding external inductance  in terms of depending on the energy that is recirculated vs supply voltage.  At this point we need to  understand that the LLC with integrated structure is more flexible to change of the supply voltage than the SRC with external coil. 

Basically, in  terms of consumer, LLC is closer to the current than to voltage source supply (which applies to all SRCs),  resulting therefore in exceptional immunity to overload and short-circuit.  Also, all SRCs are dependent on relatively narrow span of voltage supply. 

Unlike the SRC, there are PRC (parallel resonant converters), which can work within a much wider range of supply voltage (completely feasible with all the control circuits for SRC / LLC), but have some other drawbacks (again huge topic). For now, let us just say that they are more expensive and complex to carry out and that they can't perform with light-load and no-load.

LLC also can't work no-load, but it can work with very light loads (usually some parasitic load   is sufficient for self-supply and possibly some light bleeder). Unfortunately, with light loads <1/3 to 1/5 (depending on model), LLC loses its great ZVS feature and efficiency abruptly falls at low loads.

However, this is not a significant drawback as it  means that  with low power, total energy  is    smaller, therefore  the heat that is lost  in general remains low and within acceptable limits.
Therefore do not be surprised that the LLC is heated most with relatively small loads - this is normal. 

As the load grows, its temperature decreases (we are here considering the primary side) to about 80% of power when a typical well-constructed LLC is coldest (except the output diode), then again his temperature rises towards 100% of load, when it  reaches a similar value as with maybe 30%.

The hottest component under high loads on each LLC is the primary side of the transformer and it is quite normal. It is normal that the primary coil reaches about 60-80ºC, as well sa the core.

Otherwise, a ferrite core for SMPS  has minimum losses within the temperature range of 60-120 ºC typically. Lowest peak  is at about 80ºC in the majority and  manufacturers use this feature. If you make a SMPS and the transformer is cold you should know that you have a smaller efficiency than feasible.

Our sample (as well as the most modern ones) was performed with so-called "Integrated magnetics" structure, where the first two L components are made on the same core as: 

- Ls (or Lr, serial leakage inductance) that is not coupled with the consumer, ie. the one that the primary chopper "see" as the sum of all the inductance of the magnetic structure, which are not coupled with the consumer. It basically almost does not change with the change of   consumer resistance (it is changing the minimum size in practice, due to the characteristics of the ferrite, but  it is not  of a significant importance). 

- Lp (or Lm) parallel inductance, or inductance of the parallel connection of the primary magnetization inductance, ideal transformer and mapped Rac (of the consumer) to the  primary of the transformer. This inductance is variable, ie. depends on the mapped consumer resistance and its value can range from Lp (magnetization inductance of the transformer when mapped consumer resistance is infinite, ie. when the inverter has no-load), all the way to short-circuited where Lp is equal to zero. This inductance is the aspect of the chopper (rectangular signal generator) connected in series with Ls and resonant capacitor Cr.

Both of these inductances in series with Cr comprise serial oscillatory circuit that has several interesting characteristics :
