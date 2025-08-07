# ADS-EDA-DESIGN-Workflow

# ADS-Based MMIC LNA Design Flow

This repository captures **my personal, hands-on experience** for designing two RF blocks:
a (MMIC) low-noise ampfier (LNA) 
a Low-Pass Filter (LPF) in Keysight ADS. 

All steps and insights come directly from my own experience exploring ADS’s simulation, optimization, and yield-analysis features.

## Table of Contents

1. [Overview](#overview)  
2. [Prerequisites](#prerequisites)  
3. [Design Steps](#design-steps)  
   1. [Define Specifications](#define-specifications)  
   2. [Choose Amplifier Topology](#choose-amplifier-topology)  
   3. [Initial Simulation & Nominal Results](#initial-simulation--nominal-results)  
   4. [Sensitivity Analysis](#sensitivity-analysis)  
   5. [Optimization](#optimization)  
   6. [Yield Simulation & DOE Analysis](#yield-simulation--doe-analysis)  
   7. [Topology Redesign](#topology-redesign)  
   8. [Final Yield Optimization](#final-yield-optimization)  
4. [Key Takeaways](#key-takeaways)  
5. [References & Further Reading](#references--further-reading)  

---

## Overview

During my time working with Keysight ADS, I developed and refined this step-by-step MMIC LNA design flow. Every tip, diagram, and script in this repo is derived from my own trials—setting up simulations, diagnosing sensitivity, and pushing yield well above 80%. I’ve replaced branded slides with original sketches and distilled ADS features into clear, reusable guidelines.

---

## Prerequisites

- Keysight ADS (version X.X or later) installed  
- A compatible device model library for your MMIC process  
- Basic understanding of S-parameters, noise figure, and yield concepts  

---

## Design Steps

### 1. Define Specifications

From my first ADS run, I learned the importance of documenting clear goals. I kept mine in `specs.txt`:

- **Noise Figure (NF)** ≤ 2.0 dB  
- **Small-signal Gain (|S₂₁|)** ≥ 14.8 dB  
- **Output Reflection (|S₂₂|)** ≤ –15 dB  

### 2. Choose Amplifier Topology

Based on initial trials, I settled on a three-stage matching network:

1. Input match (source conjugation)  
2. Interstage network (gain flatness)  
3. Output match (load conjugation)  

### 3. Initial Simulation & Nominal Results

My first sweep over 7–9 GHz exposed unexpected bumps in NF. I exported CSV results from ADS and plotted them to compare iterations.

### 4. Sensitivity Analysis

ADS’s sensitivity tool quickly showed me which component values—often coupling capacitors and stub lengths—dominated performance. I focused on the top five for deeper tuning.

### 5. Optimization

- **Stage-by-stage noise-figure optimization** taught me to tune in isolation.  
- **Full-chain multi-objective optimization** then balanced NF, gain, and match in one pass.

### 6. Yield Simulation & DOE Analysis

My initial Monte Carlo runs returned only ~45 % yield. A DOE pin-pointed the output match network as the bottleneck.

### 7. Topology Redesign

Armed with DOE insights, I redesigned the output matching stub and interstage coupling. This was a big turning point in my personal workflow.

### 8. Final Yield Optimization

After re-tuning, my Monte Carlo results rose to over 80 %—a milestone that confirmed the value of an iterative, data-driven approach.


## Key Takeaways

- **Hands-on iteration:** My workflow evolved through trial, error, and DOE insights.  
- **Personal scripts & sketches:** I version-controlled every data export and block diagram I drew.  
- **Data-driven redesign:** Let yield and sensitivity results guide topology changes, not guesswork.
- **Possible AI Applications for choosing topologies**
