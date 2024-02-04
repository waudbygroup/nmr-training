---
title: Spectrometer Fundamentals
layout: default
nav_order: 3
parent: Exercises
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

## Offsets

## Pulses

## Power levels

## Delays

## Shaped pulses

## Gradients

## Scans, dummy scans and receiver gain

## Prosol
