---
layout: default
title: Exercises
nav_order: 2
has_children: true
---

# Exercises

Planned outline:
1. Linux tutorial
2. Topspin fundamentals
 * Acquired vs processed data
 * Structure of data directories
 * Auxilliary directories (pulse programs)
 * Copying experiments and data (edc, wrpa, wrp)
 * Good practise for naming experiments
 * Processing and acquisition parameters
3. Spectrometer fundamentals
 * Channels
 * Offsets
 * Pulses
 * Power levels
 * Delays
 * Shaped pulses
 * Gradients
 * Scans, dummy scans and receiver gain
 * Prosol
 * Pulse programs
4. Inserting a sample
 * Temperature control (BCU unit)
 * Injecting and ejecting samples
 * Locking (lock phase, avoiding saturation)
 * Tuning and matching
 * Shimming (tuning transverse shims, shigemi option, autoshim, other options)
5. 1H pulse calibration
 * Using `zg`
  * Setting up the experiment
  * Short pulse
  * Finding the null
 * Finding the offset
  * Exploring calibration with incorrect offset
 * Using `popt`
 * Using `pulsecal`
 * A shortcut - using `zg490`
 * Exploring the effect of shimming
6. 1D 1H experiments
 * Excitation sculpting
  * Phasing
 * Estimating experiment time
 * Presaturation
  * Compare the water suppression, effect on sensitivity of labile protons
 * Exploring number of scans
 * Exploring dummy scans
 * Exploring receiver gain
 * Exploring recycle time (d1, using the spooler)
 * Exploring acquisition time, td and spectrum width
7. 1D processing
 * Explore window functions - compare linewidths of small molecules vs protein
 * Water suppression (processing)
 * Chemical shift referencing
8. Further pulse calibration
 * Calculating soft pulse powers based on a calibrated hard pulse, e.g. for solvent suppression or decoupling pulses (pulse, calcpowlev)
 * Calculating shaped pulse power levels based on calibrated hard pulse, e.g. for solvent suppression or SOFAST experiments (stdisp)
 * Calibrating flip-down and flip-back pulses (zgfd.cw, zgfb.cw)
9. 15N HSQC
 * e.g. hsqcetfpf3gpsi2.cw, fhsqcf3gpph.cw
 * Awareness of power levels and limits for 15N decoupling
 * Optimising spectral width and offset
 * Optimising td, balancing sensitivity, resolution and experiment time
10. 2D processing
 * indirect phase correction (phasing and FCOR)
 * Choosing window functions
 * processing with solvent suppression
 * linear prediction
 * xfb vs xf2
 * processing of first increments
 * extracting slices
 * estimating SNR
11. Comparing 2D 15N experiments
 * Comparison of regular and sensitivity enhanced HSQC
 * Effect of 13C decoupling
 * SOFAST-HMQC
  * Calibration of shaped pulses
 * Exploring effect of d1 on SNR and sensitivity
12. 13C HMQC (hmqcgpphpr.cw)
*	Optimising spectral width and offset
*	Effect of 1JCC scalar couplings
*	Identifying methyls, aliphatics, alpha carbons and aromatics
*	Identify different types of methyls and compare 1JCC coupling in ILV methyls with methionines
13. 13C CT HSQC (hsqcctetgpsp.cw)
*	Appropriate choice of constant time delay, dependence of peak signs on coupling multiplicity
*	Selection of appropriate td
*	Comparison of sensitivity and resolution with 13C HMQC
14. 1H diffusion experiments
*	Understanding the principle of the experiment (Stejskal-Tanner equation)
 * Setting up the experiment (stebpgp1s19.cw)
*	Choice of Δ (d20), δ (2 x p30), understanding gradient power limits
*	Setting up gradient ramp (dosy macro)
*	Processing (xf2)
 * Comparison of different experiments
 * Convection
 * Determination of the diffusion coefficient and hydrodynamic radius (NMRAnalysis.jl)
15.	15N diffusion
 * Setting up the experiment (stebpgp1s19xn.4.cw)
*	Compare solvent suppression and quality of baseline with 1H methods
 * Accuracy for exchangable protons
16.	TRACT
 *	Understanding the principle of the measurement
* Setting up the experiment (tract.cw)
*	Calibrating flip-down and flip-back pulses
*	Setting an appropriate vdlist and running TROSY and anti-TROSY measurements
*	Processing and analysis to determine the effective rotational correlation time (NMRAnalysis.jl)


{: .note }
> This is a note.

{: .important }
> This is important.
 
{: .warning }
> This is a warning.

{: .highlight }
> This is a highlight.

{: .new }
> This is new.
