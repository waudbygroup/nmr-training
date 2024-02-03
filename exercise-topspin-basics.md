---
title: Topspin Basics
layout: default
nav_order: 2
parent: Exercises
---

# Topspin Basics
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

{: .note }
> This is a working draft - do not use!

## Adding Directories to the Data Browser

To add a directory to the Topspin data browser:

1. Press the `ESC` key to open the command line
2. Type `altd` and press `Enter` 
3. Navigate to the directory you want to add and press `Enter`

To sync the newly added directory:

1. Press the `ESC` key to open the command line 
2. Type `altds` and press `Enter`

This will synchronize the directory listing with the files available on disk.

## Internal Command Line

The internal Topspin command line can be accessed by pressing the `ESC` key. This allows you to execute Topspin commands and automate workflows.

Some useful commands:

- `re` - Read experiment
- `altd` - Add directory
- `altds` - Sync directory
- `edp` - Edit processing parameters 
- `eda` - Edit acquisition parameters

## Acquired vs Processed Data 

- **Acquired data** - The direct output of the spectrometer, usually saved as `.fid` or `.ser` files
- **Processed data** - Data that has been Fourier transformed and phased. Saved as `.1r` or `.2rr` files generally.

## Directory Structure

Topspin uses a standardized directory structure:

- **Main folder** - Contains all the experiments, generally named by date 
- **Numbered experiments** - Each experiment folder is numbered (e.g. `2021-08-05-1`, `2021-08-05-2`)
- **Processed data folder (pdata)** - Contains numbered directories with the processed datasets 
- **Acqus files** - Contain the acquisition parameters 
- **fid/ser files** - Raw free induction decay data, before Fourier transform

## Auxiliary Directories 

- pulse programs...

## Setting Preferences 

Preferences like fonts, colors, auxilliary directories etc. can be set using the `setres` command.

## Reading Experiments 

- `re XX` - Open (read) experiment number XX
- `rep XX` - Open (read) processed dataset number XX from the current experiment
- `re XX YY` - Open (read) processed dataset number YY from experiment XX

## Copying Data

- `edc` - Copy an experiment setup (opens a dialog)
- `wrpa XX` - Copy an experiment, including acquired data, to new experiment number `XX`
- `wrp XX` - Write a copy of the current processed dataset to a new processed dataset number `XX`

## Good Practise for Naming Experiments 

- Include your name and the date alongside a brief indication of the sample/measurement in the main folder title, e.g. `chris_fln5_assignment_240130`
- Always use dates in the `YYMMDD` format - this makes it easy to sort by date at a later stage
- Group related samples (e.g. titration measurements) within a directory by separating experiment numbers by tens or hundreds
- Use high numbers like 999 for quick test experiments
- Provide clear sample details in the title file. This should include sample composition, isotopic labelling, solvent, temperature, buffer, and the experiment being acquired. Put a quick summary in the first line and details in subsequent lines.

## Access Processing and Acquisition Parameters

- `edp` - Edit processing parameters
- `eda` - Edit acquisition parameters 
- `ased` - Additional pulse program parameters
