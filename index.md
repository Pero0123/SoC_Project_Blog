---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---

Welcome to my System on Chip (SoC) Project. The goal of this project is to create an image using the Artix-7 board and Vivado. In this blog I will explain the project and the process of making it. [1] An FPGA can be reprogrammed "in the field", after the chip is manufactured. FPGAs are commonly used high performance computing and for prototyping. They are very versatile compared to application specific integrated circuits(ASICs) which are designed for a specific purpose an cannot be reprogrammed after manufacture[2]. Video Graphics Array(VGA) is a display standart and connector introduced by IBM. It transmits video as analog signals unlike modern standarts like hdmi which transmit data using digital signals. Each colour has its own analog signal, along with sync signals. The original standart supported a resolution of 640 X 480, 4 bit colours and a 60Hz refresh rate with later implementations improving on this. Vivado was used to Design, Synthesis and simulate the project.[3] Vivado was also used to generate a bitstream to upload to the Artix-7 board. The code was written in verilog. Verilog is a hardware description language or HDL[4].

## **Project Summary**
The goal of the project was to display an image or pattern on a 640 x 480 vga display. A Field Programmable Gate Array(FPGA) was used to power the project. 
### **Project Set-Up**


<img src="https://raw.githubusercontent.com/melgineer/fpga-vga-verilog/main/docs/assets/images/VGAPrjSum.png">
### **Template Code**
Outline the structure and design of the Verilog code templates you were given. What do they do? Include reference to how a VGA interface works. Guideline: 2/3 short paragraphs, consider including screenshot(s).
### **Simulation**
Explain the simulation process. Reference any important details, include a well-selected screenshot of the simulation. Guideline: 1/2 short paragraphs.
### **Synthesis**
Describe the synthesis and implementation processes. Consider including 1/2 useful screenshot(s). Guideline: 1/2 short paragraphs.
### **Demonstration**
Perhaps add a picture of your demo. Guideline: 1/2 sentences.

## **My VGA Design Edit**
Introduce your own design idea. Consider how complex/achievabble this might be or otherwise. Reference any research you do online (use hyperlinks).
### **Code Adaptation**
Briefly show how you changed the template code to display a different image. Demonstrate your understanding. Guideline: 1-2 short paragraphs.
### **Simulation**
Show how you simulated your own design. Are there any things to note? Demonstrate your understanding. Add a screenshot. Guideline: 1-2 short paragraphs.
### **Synthesis**
Describe the synthesis & implementation outputs for your design, are there any differences to that of the original design? Guideline 1-2 short paragraphs.
### **Demonstration**
If you get your own design working on the Basys3 board, take a picture! Guideline: 1-2 sentences.

## **References**
[1] IBM, “What is an FPGA” [Online] Available: [https://en.wikipedia.org/wiki/Application-specific_integrated_circuit](https://www.ibm.com/think/topics/field-programmable-gate-arrays)
[2]Wikipedia, "What is an ASIC" [Online] Available: https://en.wikipedia.org/wiki/Application-specific_integrated_circuit
[3] AMD, "Vivado Software" [Software] Available : https://www.amd.com/en/products/software/adaptive-socs-and-fpgas/vivado.html#advantages
[4] Doulos, "Vivado Software" [Online] Available : https://www.doulos.com/knowhow/verilog/what-is-verilog/


