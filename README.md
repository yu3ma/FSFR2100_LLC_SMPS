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
- Minimal input voltage: 295VDC (210VAC)
- Maximal input voltage: 355VDC (250VAC)
- Output voltage 1: +/-28V 3A
- Output voltage 2: +/-18V 1A
- Resonance frequency: 100 kHz 
- Max operating frequency: 250 kHz 
