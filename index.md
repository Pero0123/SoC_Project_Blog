Welcome to my System on Chip (SoC) Project. My name is Pero Schwitalla. The goal of this project is to create an image using the Artix-7 board and Vivado. In this blog I will explain the project and the process of making it.

## **Project Summary**
### **Tools and Key Terms**
An FPGA can be reprogrammed "in the field", after the chip is manufactured. FPGAs are commonly used high performance computing and for prototyping[1]. They are very versatile compared to application specific integrated circuits(ASICs) which are designed for a specific purpose an cannot be reprogrammed after manufacture[2]. Video Graphics Array(VGA) is a display standart and connector introduced by IBM. It transmits video as analog signals unlike modern standarts like hdmi which transmit data using digital signals. Each colour has its own analog signal, along with sync signals. The original standart supported a resolution of 640 X 480, 4 bit colours and a 60Hz refresh rate with later implementations improving on this. Vivado was used to Design, Synthesis and simulate the project.[3] Vivado was also used to generate a bitstream to upload to the Artix-7 board. The code was written in verilog. Verilog is a hardware description language or HDL[4].

### **Project Set-Up**
<img src="https://raw.githubusercontent.com/melgineer/fpga-vga-verilog/main/docs/assets/images/VGAPrjSum.png">
To set the project up, the Artix-7 board was connected to computer running Vivado using a micro usb cable. The board was also connected to a monitor using the vga interface. I started by creating a new project in Vivado and downloading the template files. I added VGASync.v, VGAColorCycle.v and VGATop.v to the design sources. I also edited the clock to run at 25Mhz using the clock wizard. I added the Basys3_Master.xdc file to the constraints folder.

### **Template Code**
**VGATop.v**
This is the top level file and connects everything together.

**VGASync.v**
This module create sync singals, aswell aswell as the current pixel co-orinates. This allows specifics areas or pixels to be coloured later.
<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/blob/main/docs/assets/images/20241208_232704.jpg" width="320px">

**VGAColorCycle.v** 
This module is the main code for creating an image. It consists of a state machine, each being a specified colour using the red, green and blue registers. Each register is 4 bits to allow 256 levels for each colour. The next state is selected after the timer reaches the COUNT_TO register. This creates a colour cycling effect on the monitor.

The images below show the demo working.


<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241111_160448.jpg" width="320px">
<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241111_160450.jpg" width="320px">
<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241111_160459.jpg" width="320px">

Out of curiosity, I recorded the screen in slow motion to see what is causing the slight flickering. The video shows the new colour begining half way down the screen causing 2 colours being displayed at the same time for a split second. This may be caused by the time delay between states not lining up with the time it takes to display a frame.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241111_160518-ezgif.com-crop.gif" width="320px">

**VGAColor_Stripes.v** 
This module displays coloured vertical stripes. VGASync is used here to define an area for each colour usinng col and row. After I got this running I changed it to diplay vertical stripes. I did this by limiting each colour to a small range of rows instead of columns

The images below show the demo working.


<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241118_162325.jpg" width="320px">
<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241118_163521.jpg" width="320px">


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


