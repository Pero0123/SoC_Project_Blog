Welcome to my System on Chip (SoC) Project. My name is Pero Schwitalla. The goal of this project is to create an image using the Artix-7 board and Vivado. In this blog I will explain the project and the process of making it.

## **Project Summary**
### **Tools and Key Terms**
An FPGA can be reprogrammed "in the field", after the chip is manufactured. FPGAs are commonly used high performance computing and for prototyping[1]. They are very versatile compared to application specific integrated circuits(ASICs) which are designed for a specific purpose an cannot be reprogrammed after manufacture[2]. Video Graphics Array(VGA) is a display standart and connector introduced by IBM. It transmits video as analog signals unlike modern standarts like hdmi which transmit data using digital signals. Each colour has its own analog signal, along with sync signals. The original standart supported a resolution of 640 X 480, 4 bit colours and a 60Hz refresh rate with later implementations improving on this. Vivado was used to Design, Synthesis and simulate the project.[3] Vivado was also used to generate a bitstream to upload to the Artix-7 board. The code was written in verilog. Verilog is a hardware description language or HDL[4].

### **Project Set-Up**
<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/image.png" width="680px">
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
Vivado also supports simulating designs in software. This is usefull to test a design befoe generating the bitstream and uploading to the hardware as this can be a very slow process. To save time, a scaled down version of the project is simulated. the rows only go from 0 to 5 instead of 0 to 479.
<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot 2024-12-09 111541.png" width="320px">
### **Synthesis**
The next step is to run the Synthesis and Implementation. Synthesis converts the code to a netlist and Implementation uses the netlist as the input and does the routing[5]. After this step a bitstream can be generated. The bistream is a binary file used to configure the FPGA[6].






## **My VGA Design Edit**
Introduce your own design idea. Consider how complex/achievabble this might be or otherwise. Reference any research you do online (use hyperlinks).
### **Code Adaptation**
Briefly show how you changed the template code to display a different image. Demonstrate your understanding. Guideline: 1-2 short paragraphs.
### **Simulation**
Show how you simulated your own design. Are there any things to note? Demonstrate your understanding. Add a screenshot. Guideline: 1-2 short paragraphs.
### **Synthesis**
Describe the synthesis & implementation outputs for your design, are there any differences to that of the original design? Guideline 1-2 short paragraphs.

## **References**
[1] IBM, “What is an FPGA” [Online] Available: [https://en.wikipedia.org/wiki/Application-specific_integrated_circuit](https://www.ibm.com/think/topics/field-programmable-gate-arrays)
[2]Wikipedia, "What is an ASIC" [Online] Available: https://en.wikipedia.org/wiki/Application-specific_integrated_circuit
[3] AMD, "Vivado Software" [Software] Available : https://www.amd.com/en/products/software/adaptive-socs-and-fpgas/vivado.html#advantages
[4] Doulos, "Vivado Software" [Online] Available : https://www.doulos.com/knowhow/verilog/what-is-verilog/
[5] AMD, "Synthesis and Implementation" [Online] Available : https://www.doulos.com/knowhow/verilog/what-is-verilog/](https://adaptivesupport.amd.com/s/question/0D52E00006hpkc2SAA/the-difference-between-implementation-and-synthesize?language=en_US
[6] vhdlwhiz, "Bitstream" [Online] Available : https://vhdlwhiz.com/terminology/bitstream/#:~:text=A%20bitstream%20is%20a%20file,a%20human%2Dreadable%20hex%20file.



