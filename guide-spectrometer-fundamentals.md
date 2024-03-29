---
title: Spectrometer Fundamentals
layout: default
nav_order: 3
parent: Guides
---

# Spectrometer Fundamentals
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Introduction

Adapted from the [EMBO Practical course on structure determination by NMR](https://users.cs.duke.edu/~brd/Teaching/Bio/asmb/Papers/NMR/Introduction-reviews/Blackledge/sprangers_practical.pdf).

## Pulse programs

An important skill is to be able to examine and understand pulse programs. This does not necessarily mean to understand the complete details of the sequence design, but a knowledgeable user should be able to examine a pulse program to determine parameters that may be required for its setup.

Bruker pulse programs are plain text files, and have a simple basic syntax. The pulse program is executed line by line, and when a line is finished the program continues on the next line. When two commands are written on one line they start both at the beginning. The line lasts as long as the longest command on that line.

Lines beginning with a semicolon `;` are comments - they are ignored by the spectrometer, but can provide useful information about parameters, and note on how the sequence operates.

Pulse programs use a rather concise syntax to express pulses, power levels, delays and so forth. It's important to be able to recognise what these symbols mean, and the physical units that they are expressed in. A brief guide to the most important of these is provided in the rest of this document.

## Channels

NMR spectrometers are capable of pulsing on or acquiring signals from a variety of different nuclei. Each nucleus used in an experiment must be associated with a channel -- a path from the signal generator and transmitter through an amplifier to the coil, and from the coil through a pre-amplifier and amplifier to the receiver.

Channels are labelled `f1`, `f2` and so on. There are typically four channels on spectrometers used for biomolecular NMR (`f1`, `f2`, `f3` and `f4`):

| channel | nucleus |
|:--------|:--------|
| f1      | proton (1H) |
| f2      | carbon (13C) |
| f3      | nitrogen (15N) |
| f4      | deuterium (2H) |

However, this may not always be the case, for example, f1 may also be used for fluorine (19F) on some spectrometers.

The amplifier setup and arrangement of channels can be checked using the `edasp` command in Topspin.

{: .note }
> It's good practise to check the amplifier setup before tuning and matching, because these are the channels that will be available. Only make changes if you know what you're doing though! 

## Offsets

Each channel on the spectrometer has an associated frequency. For example, on a 600 MHz spectrometer, the proton channel would have a frequency of about 600 MHz, the carbon-13 channel a frequency around 150 MHz, and nitrogen-15 channel a frequency around 60 MHz. These are often referred to as **base frequencies** and are denoted `bf1`, `bf2` etc. for channels f1, f2, etc. They are not configurable by the user, but correspond to an chemical shift of **zero ppm** (based on referencing to the solvent, not to internal standards like DSS or TMS).

{: .note }
> When you lock onto a solvent, the spectrometer automatically adjusts the B0 field strength (LOCK FIELD) so that the solvent appears at the expected chemical shift (e.g. 4.7 ppm for H2O/D2O or D2O) relative to the base frequency.

When setting up an experiment, one usually wants to set the centre of the spectrum -- the transmitter frequency -- to a chemical shift other than zero ppm (i.e. different to the base frequency). There are three reasons for this:

1. (For the 1H channel only) Placing the solvent signal in the center of the spectrum (i.e. so it is on-resonance with the transmitter frequency) is usually required for solvent suppression experiments
2. By placing the center of the spectrum in the middle of the signals being observed, you can reduce the spectrum width that has to be acquired. This can speed up recording times for 2D experiments and increase sensitivity
3. Placing the transmitter near the center of signals being observed reduces *off-resonance effects* -- imperfections that result when signals are a large distance from the transmitter frequency

We can define the center of the spectrum by an **offset** relative to the base frequency. These are referred to as `o1`, `o2`, `o3` etc. and are specified in Hz. Equivalently, you can define them as chemical shifts (ppm) through the parameters `o1p`, `o2p`, `o3p` etc.

The combination of offset and base frequency defines the actual spectrometer frequencies generated by the transmitter for each nucleus. These are denoted by `sfo1`, `sfo2`, `sfo3` etc.

To summarise:

| Term | Description | Units |
|:---|:---|:---|
| bf1, bf2, bf3 | Base frequencies (0 ppm) | MHz |
| o1, o2, o3 | Offsets  | Hz |
| o1p, o2p, o3p | Offsets  | ppm |
| sfo1, sfo2, sfo3 | Actual transmitter frequencies (BF + offset) | MHz |


## Pulses

Pulses (specifically, pulse lengths) are represented by the parameters `p0` to `p31`. They are stored in units of **microseconds (us)**, but you can input values in ms or s by following numbers with 'm' or 's'. Be careful if doing this though, because long pulses can only be safely applied at low power levels.

By convention, some parameters are commonly used for different types of pulses on different nuclei:

| Symbol | Description |
|:---|:---|
|`p1` | 1H 90 degree hard pulse |
|`p2` | 1H 180 degree hard pulse |
|`p3` | 13C 90 degree hard pulse |
|`p4` | 13C 180 degree hard pulse |
|`p21` | 15N 90 degree hard pulse |
|`p22` | 15N 180 degree hard pulse |
|`p16` and `p19` | Gradient pulses |

You can check and edit pulse lengths in the `ased` acquisition parameter editor, or by typing their symbol directly from the command line.

{: .warning }
> There are no safety checks on pulse lengths! It is possible to cause serious damage to the probe by using a pulse that's too long for the given power level.
> Always double check you haven't made a typo when you enter a new pulse length, and be aware of units. If in doubt, check with an experienced user.

## Power levels

The effect of a pulse on spins depends on the duration of the pulse, and the power level at which it is applied. Power levels can be a confusing subject because there are several ways to describe them, both in practise and when discussed in the literature.

There are two ways to specify power levels within Topspin:

* Watts (W) -- this is a direct measure of the power going into the probe from the amplifier
* Attenuation in decibels (dB) -- this measures the *reduction* in power, relative to the amplifier's maximum. Decibels are a logarithmic unit, and so this is often a more useful way to handle power levels that can vary over orders of magnitude.

Power levels in Watts are stored in the parameters `plW0-63` and attenuations in the parameters `pldB0-63`. Changing the value in one unit will update the other parameter automatically. The relation is:

$$dB = -10 \log_10 P_1 / P_\mathrm{ref}$$

where $$P_\mathrm{ref}$$ is the reference power level.

{: .warning }
> High powers (in W) correspond to small, often negative, attenuations when measured in dB. Likewise, large attenuations (in dB) correspond to small power levels (in W). Take care you don't get confused by this -- there are no safety checks and it's possible to cause serious damage to the probe.

The amplifier for each channel has a maximum power level. Short pulses applied at maximum power are referred to as *hard pulses*, and these are the most common pulses that need to be calibrated (discussed elsewhere). By convention, some parameters are commonly used to specify the maximum power level for different channels:

| Symbol | Description |
|:---|:---|
|`plW1` or `pldB1` | 1H maximum power |
|`plW2` or `pldB2` | 13C maximum power |
|`plW21` or `pldB21` | 15N maximum power |

{: .warning }
> The maximum power level is checked before a pulse sequence is run. However, the *average* power deposition throughout the sequence is not. You can still damage the probe by applying high power levels for long periods of time!

### Power levels: Theory

Away from the spectrometer, for example when reporting a pulse sequence in a paper, or when analysing a sequence theoretically, power levels are normally specified as a *frequency* $$\nu_1$$, in Hz or kHz. This is the frequency that spins will rotate about the applied field (on-resonance) when the pulse is applied.

For example, if a 20 kHz pulse is applied, spins will rotate about the applied field 20,000 times per second. It would therefore take 1/20000 = 0.00005 s = 50 μs to make a complete 360 degree rotation, corresponding to a 90 degree pulse length of 12.5 μs.

More generally, the flip (rotation) angle $$\beta$$ depends on the pulse strength $$\nu_1$$ and pulse length $$\tau_p$$:

$$\beta = \nu_1 \tau_p$$

Within the probe, the pulse strength $$\nu_1$$ is proportional to the voltage $$V$$ in the coil. However, the *power* in the probe (set by `plW1` etc.) depends on the square of the voltage, according to Ohm's law:

$$P = V^2 / R$$

The resistance $$R$$ is usually 50 Ω. This means that to double the pulse strength, one must *quadruple* the rf  power. High power levels can reach the limit of the amplifier, but can also cause *sample heating* -- sometimes up to several degrees!

Putting all this together, the pulse attenuation (in dB) changes with voltage (i.e. pulse strength) as:

$$dB = -20 \log_10 V_1 / V_2$$

Thus, a increase of 20 dB in attenuation corresponds to a ten-fold reduction of the pulse strength (and a hundred-fold reduction in rf power and sample heating). Similarly, halving the pulse power corresponds to an increase of 6 dB in attenuation (and a four-fold reduction in rf power and sample heating).


## Delays

Delays are represented by the parameters `d0` to `d31`. They are stored as **seconds (s)**.

By convention, some parameters are commonly used for different types of delay:

| Symbol | Description |
|:---|:---|
|`d1` | Recycle delay = time between scans. Typically 1-2 seconds, shorter for SOFAST/BEST experiments |


You can check and edit delays in the `ased` acquisition parameter editor, or by typing their symbol directly from the command line.

{: .important }
> Delays are specified in seconds, while pulses are specified in microseconds -- take care that this doesn't cause confusion or mistakes.


## Shaped pulses

## Gradients

## Scans, dummy scans and receiver gain

## Prosol
