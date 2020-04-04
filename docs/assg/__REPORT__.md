---
title: 
author:
partner:
date:
---
## (5 pts)
Summarize the main differences between DRAM and SRAM memories.

## (5 pts)
Draw a circuit of transistors showing the internal structure for all the storage cells for a 4x2 DRAM (four words, two bits each), clearly labelling all internal components and connections.

## (5 pts)
Summarize the main differences between EPROM and EEPROM memories.

## (5 pts)
Use an HLSM to capture the design of a system that can save data samples and then play them back. The system has an 8-bit input D where data appears. A single-bit input S changing from 0 to 1 requests that the current value on D (i.e., a sample) be saved in a nonvolatile memory. Sample requests will not arrive faster than once per 10 clock cycles. Up to 10,000 samples can be saved, after which sampling requests are ignored. A single-bit input P changing from 0 to 1 causes all recorded samples to be played back—i.e., to be written to an output Q one sample at a time in the order they were saved at a rate of one sample per clock cycle. A single-bit input R resets the system, clearing all recorded samples. During playback, any sample or reset request is ignored. At other times, reset has priority over a sample request. Choose an appropriate size and type of memory, and declare and use that memory in your HLSM.

## (5 pts)
 For an 8-word queue, show the queue’s internal state and provide the value of popped data for the following sequences of pushes and pops: (1) push A, B, C, D, E, (2) pop, (3) pop, (4) push U, V, W, X, Y, (5) pop, (6) push Z, (7) pop, (8) pop, (9) pop.

## (5 pts)
A system S counts people that enter a store, incrementing the count value when a single-bit input P changes from 1 to 0. The value is reset when R is 1. The value is output on a 16-bit output C, which connects to a display. Furthermore, the system has a lighting system to indicate the approximate count value to the store manager, turning on a red LED (LR=1) for 0 to 99, else a blue LED (LB=1) for 100 to 199, else a green LED (LG=1) for 200 and above. Draw a block diagram of the system and its peripheral components, using two processors for the system S. Show the HLSM for each processor.

## (5 pts)
 Compose a 4x16 decoder with enable from 2x4 decoders with enable.
