---
name: Computer Architecture - Hybrid Processors
tools: [Bluespec SystemVerilog, Bash, PyTorch]
image: ../assets/img/projects/nus.jpg
description: Worked on making In-Order Processors as efficient as Out-of-Order ones, while trying to retain an In-Order processor's energy efficiency. This also acted as my Undergraduate Bachelor's Thesis at BITS Pilani.
---

# Computer Architecture: Hybrid Processors

## Debrief
I made progress by synthesizing an In-Order Core from MIT CSAIL's RISCY Out-Of-Order Processor, written in 
Bluespec SystemVerilog and adding essential components to make it an OoO core while checking areas of maximum power 
consumption. 
This method helped in gaining important insights into actual dynamic power consumption by cache, which was 
previously not possible by tools like McPat, and Cacti. 

Mentors: [Prof. Trevor Carlson](https://www.comp.nus.edu.sg/~tcarlson/)

This work acted as my Undergraduate Bachelor's Thesis at BITS Pilani, India.

## Aim

In the research domain, there’s a stark difference which exists between results achieved on architectures modelled and 
simulated on software and architectures modelled on hardware. 
The current methods which exist to find area and power estimations like McPat and Cacti introduce a sizeable overhead, 
which is why my work was to implement ideas which my research team came up with in Bluespec Systemverilog. 

## Progress

Bluespec Systemverilog has inbuilt tools to communicate with Verilator which converts the code written in BSV into 
synthesizable Verilog code. It also uses connects to communicate with benchmarks which are written in C, and the 
processor’s overheads and performance can thus be easily gauged.

I worked on MIT CSAIL’s RISCY OoO processor, along with working and fixing their RISCY InOrder processor, for which 
they had discontinued support. One of the postdocs on my team had designed a processor and submitted it to MICRO. 

While implementing his processor, I found that the algorithm he used for identifying backward dependancy chains was 
hardware heavy, and suggested an easier fix. Each entry of the reOrder buffer had to be checked to find each 
instruction’s destination register, to find if the current instruction had any sources dependant on it. This prompted 
wires from every index which had to be iteratively checked. 

I suggested a Register dependancy table, since the number 
of physical registers were indexed, and the right index could directly be accessed. This is a single example of many 
such improvements I identified and implemented.

I also helped automate the BSV code to be extracted and built on FPGAs on AWS using bash scripting. This required a lot 
of permission modifications since it included s3 buckets, AWS’s elastic file system, and split compilation between C4 
(Compute centric but expensive) and F1 (general but relatively cheaper) instances.
