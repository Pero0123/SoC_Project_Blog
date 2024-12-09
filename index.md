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

This module create sync singals, aswell aswell as the current pixel co-orinates. This allows specifics areas or pixels to be coloured later. Each pixel has a co-ordinate as shown in the diagram below. The top left is (0,0) and the bottom right is (479,639). This makes it possible to check when a particular pixel is reached and write a specified colour to it.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot%202024-12-09%20125639.png" width="420px">

**VGAColorCycle.v** 

This module is the main code for creating an image. It consists of a state machine, each being a specified colour using the red, green and blue registers. Each register is 4 bits to allow 256 levels for each colour. The next state is selected after the timer reaches the COUNT_TO register. This creates a colour cycling effect on the monitor.

The images below show the demo working.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241111_160448.jpg" width="420px"> 

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241111_160450.jpg" width="420px">

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241111_160459.jpg" width="420px">

Out of curiosity, I recorded the screen in slow motion to see what is causing the slight flickering. The video shows the new colour begining half way down the screen causing 2 colours being displayed at the same time for a split second. This may be caused by the time delay between states not lining up with the time it takes to display a frame.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241111_160518-ezgif.com-crop.gif" width="420px">

**VGAColor_Stripes.v** 

This module displays coloured vertical stripes. VGASync is used here to define an area for each colour usinng col and row. After I got this running I changed it to diplay vertical stripes. I did this by limiting each colour to a small range of rows instead of columns

The images below show the demo working.


<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241118_162325.jpg" width="420px">

Below is a snippet of the original code. There is an if statement which sets the colour for each 80px column

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot 2024-12-09 124531.png" width="420px">

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241118_163521.jpg" width="420px">

Below is the modified code. Each 60px row is set to a different colour.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot 2024-12-09 124627.png" width="420px">


### **Simulation**

Vivado also supports simulating designs in software. This is usefull to test a design befoe generating the bitstream and uploading to the hardware as this can be a very slow process. To save time, a scaled down version of the project is simulated. the rows only go from 0 to 5 instead of 0 to 479.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot 2024-12-09 111541.png" width="420px">

### **Synthesis**

The next step is to run the Synthesis and Implementation. Synthesis converts the code to a netlist and Implementation uses the netlist as the input and does the routing[5]. After this step a bitstream can be generated. The bistream is a binary file used to configure the FPGA[6].






## **My VGA Design Edit**

First I made small edits to the code to the colour stripes file figure out exactly how it works and make sure I understand it. I changed the code to draw only blocks of each colour in the top row. Next I modified the code to display a diagonal line. This was by changing the range for rows and columns for each colour in the if statements.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241118_174046.jpg" width="420px">

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241118_172408.jpg" width="420px">

Once I felt that I understood the code well, I started to work on my own design. The plan was to create a version of tic tax toe, using colours instead of Xs and Os. I was planning on assigning one switch for every grid position. The first step is to create the grid. I calculated the offset I needed from each side of the screen to center a box. I also divided up this box into a 3x3 grid. The image below is of the rough sketches and calculations used during the design process. Once I had the all the values calculated I started coding each section.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot 2024-12-09 132059.png" width="420px">

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot 2024-12-09 132044.png" width="420px">

Next I added the grid inside the box and then added if statements which colour in the squares. I choose random colours for these to differentiate them.


<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241202_161930.jpg" width="420px">

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241202_174351.jpg" width="420px">

At some point I accidental changed the last if statement which cause the image to change to the one below. I corrected the incorrect row value and changed the colour back to white.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241202_175025.jpg" width="420px">



<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241202_175407.jpg" width="420px">

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/20241202_175418.jpg" width="420px">

This is a snippet of the code for the grid.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot 2024-12-09 142214.png" width="420px">

This is the code to allow the colour to be changed using one of the switches on the board. I had to add the switch to the constraints file and name it.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot 2024-12-09 142236.png" width="420px">

### **Synthesis**

Below are screenshots of the Schematic of my design and the netlist. Each logical block is one of the source files such as the clock, vga sync and colour cycle. The registers the end are colours which will be written. There are 3 inputs on the left which represent the clock, reset and the input switch a. The input clock is 50Mhz, which is divided to 25Mhz by the first logic block. This signal is used by the vga sync block. the col and row registers from vga sync are connected to the colour cycle block. This allows code which writes to specific. The Schematic and netlist are almost identical to the colourstripes ones because they are based on the same desing and function in a similar way. The only difference is the input switch a.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/SchematicEdited.png" width="600px">

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Netlist.png" width="400px">


Below are screenshots of the Schematic and netlist for the colour cycle design. It is similar to my own design with the biggest difference being that there are no row and col signals. This is because colour cycle doesn't use these as the same colour is written to every pixel.

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot 2024-12-09 150752.png" width="400px">

<img src="https://raw.githubusercontent.com/Pero0123/SoC_Project_Blog/main/docs/assets/images/Screenshot 2024-12-09 150831.png" width="600px">


## **References**

[1] IBM, “What is an FPGA” [Online] Available: [https://en.wikipedia.org/wiki/Application-specific_integrated_circuit](https://www.ibm.com/think/topics/field-programmable-gate-arrays)

[2]Wikipedia, "What is an ASIC" [Online] Available: [https://en.wikipedia.org/wiki/Application-specific_integrated_circuit)

[3] AMD, "Vivado Software" [Software] Available : [https://www.amd.com/en/products/software/adaptive-socs-and-fpgas/vivado.html#advantages)

[4] Doulos, "Vivado Software" [Online] Available : [https://www.doulos.com/knowhow/verilog/what-is-verilog)

[5] AMD, "Synthesis and Implementation" [Online] Available : [https://adaptivesupport.amd.com/s/question/0D52E00006hpkc2SAA/the-difference-between-implementation-and-synthesize?language=en_US)

[6] vhdlwhiz, "Bitstream" [Online] Available : https://vhdlwhiz.com/terminology/bitstream/#:~:text=A%20bitstream%20is%20a%20file,a%20human%2Dreadable%20hex%20file.)



