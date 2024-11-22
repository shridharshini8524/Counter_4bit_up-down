# Exp-No:2 - BIT Up-Down Counter - Write Verilog Code and Verify the Functionality using Test-bench ( Using Frontend tool - nclaunch in cadence).

**Aim:** <br>
<br>
&emsp;&emsp;To write a verilog code for 4bit up/down counter and verify the functionality using Test bench.<br>
<br>

**Tools used for ASIC Flow:** <br>
<br>
&emsp;&emsp;nclaunch- Used for Functional Simulation<br>
<br>

**Design Information and Bock Diagram:** <br>
<br>
&emsp;&emsp;An up/down counter is a digital counter which can be set to count either from 0 to MAX_VALUE or MAX_VALUE to 0.<br>

&emsp;&emsp;The direction of the count(mode) is selected using a single bit input. The module has 3 inputs - clk, reset which is active high and a Up Or Down mode input.The output is Counter which is 4 bit in size.<br>

&emsp;&emsp;When Up mode is selected, counter counts from 0 to 15 and then again from 0 to 15.<br>

&emsp;&emsp;When Down mode is selected, counter counts from 15 to 0 and then again from 15 to 0.<br>

&emsp;&emsp;Changing mode doesn't reset the Count value to zero.<br>

&emsp;&emsp;You have to apply high value to reset, to reset the Counter output.<br>
<br>

![image](https://github.com/user-attachments/assets/efe1095e-989e-4005-b53b-e9dc50d4025c)
<br>

**<p align="center">Fig 1: 4 Bit Up/Down Counter** <br>

<br>

**Creating a Work space :** <br>
<br>
&emsp;&emsp;Create a folder in your name (Note: Give folder name without any space) and Create a new sub-Directory name it as Exp2 or counter_design for the Design and open a terminal from the Sub-Directory. <br>
<br>

**Functional Simulation:** <br>
<br>
&emsp;&emsp;Invoke the cadence environment by type the below commands <br>

&emsp;&emsp;tcsh (Invokes C-Shell) <br>

&emsp;&emsp;source /cadence/install/cshrc (mention the path of the tools) <br>

&emsp;&emsp;(The path of cshrc could vary depending on the installation destination)<br>
      
&emsp;&emsp;After this you can see the window like below <br>
<br>
![Picture8](https://github.com/user-attachments/assets/dcc1bb24-5e2d-4f1b-96d0-f410f4f2b0c1)

<br>

**<p align="center">Fig 2: Invoke the Cadence Environment** <br>

<br>

**Creating Source Code:** <br>
<br>
&emsp;&emsp;In the Terminal, type gedit <filename>.v or <filename>.vhdl depending on the HDL Language you are to use (ex: 4b_up_downCount.v).<br>

&emsp;&emsp;A Blank Document opens up into which the following source code can be typed down.<br>

&emsp;&emsp;(Note : File name should be with HDL Extension)<br>
<br>

**Verilog code for 4-Bit Up-Down Counter:**
```

`timescale 1ns / 1 ns
module counter(clk,m,rst,count);
input clk,m,rst;
output reg [3:0] count;
always@(posedge clk or negedge rst) begin
if (!rst)
count=0;
else if(m)
count=count+1;
else
count=count-1;
end
endmodule

```
&emsp;&emsp;Use Save option or Ctrl+S to save the code or click on the save option from the top most right corner and close the text file.<br>
<br>

**Creating Test bench:** <br>
<br>
&emsp;&emsp;Similarly, create your test bench using gedit <filename_tb>.v or <filename_tb>.vhdl to open a new blank document (4bitup_down_count_tb.v).<br>
<br>

**Test-bench code for 4-Bit Up-Down Counter:**
```

`timescale 1ns / 1ns
module counter_test;
reg clk,rst,m;
wire [3:0] count;
initial begin
clk=0;
rst=0;#5;
rst=1; end
initial begin
m=1;
#160 m=0; end
counter counter1 (clk,m,rst, count);
always #5 clk=~clk;
initial begin $monitor("Time=%t rst=%b clk=%b count=%b" , $time,rst,clk,count);
#320 $finish; end
endmodule

```

**To Launch Simulation tool** <br>
<br>
&emsp;&emsp;linux:/> nclaunch -new&            // “-new” option is used for invoking NCVERILOG for the first time for any design<br>

&emsp;&emsp;linux:/> nclaunch&                 // On subsequent calls to NCVERILOG<br>

&emsp;&emsp;It will invoke the nclaunch window for functional simulation we can compile,elaborate and simulate it using Multiple step<br>
<br>

![Picture9](https://github.com/user-attachments/assets/29ee2e8a-792b-4c3f-a1ab-893d4a330563)

<br>

**<p align="center">Fig 3: Setting Multi-step simulation** <br>

<br>
&emsp;&emsp;Select Multiple Step and then select “Create cds.lib File” as shown in below figure<br>

&emsp;&emsp;Click the cds.lib file and save the file by clicking on Save option<br>
<br>

![Screenshot 2024-10-05 093852](https://github.com/user-attachments/assets/91ad3198-0259-4aee-8cad-88454481ac20)

<br>

**<p align="center">Fig 4: cds.lib file Creation** <br>

<br>
&emsp;&emsp;Save cds.lib file and select the correct option for cds.lib file format based on the  HDL Language and Libraries used.<br>

&emsp;&emsp;Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in below figure<br>

&emsp;&emsp;We are simulating verilog design without using any libraries<br>
<br>

![Screenshot 2024-10-05 093943](https://github.com/user-attachments/assets/73f0d852-861a-49b0-9ee9-dcdc79ab8686)

<br>

**<p align="center">Fig 5: Selection of Don’t include any libraries** <br>

<br>
&emsp;&emsp;A Click “OK” in the “nclaunch: Open Design Directory” window<br>

&emsp;&emsp;A ‘NCLaunch window’ appears as shown in figure below<br>

&emsp;&emsp;Left side you can see the HDL files. Right side of the window has worklib and snapshots directories listed.<br>

&emsp;&emsp;Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation<br>
<br>

![Screenshot 2024-10-05 094118](https://github.com/user-attachments/assets/d0abc092-b47c-4f5c-937d-6d4c41e96ee6)

<br>

**<p align="center">Fig 6: Nclaunch Window** <br>

<br>
&emsp;&emsp;To perform the function simulation, the following three steps are involved Compilation, Elaboration and Simulation.<br>
<br>

**Step 1: Compilation:– Process to check the correct Verilog language syntax and usage**  <br>
<br>
&emsp;&emsp;Inputs: Supplied are Verilog design and test bench codes <br>

&emsp;&emsp;Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file <br>
<br> 

**Steps for compilation:** <br>

&emsp;&emsp;1. Create work/library directory (most of the latest simulation tools creates automatically)<br>
  
&emsp;&emsp;2. Map the work to library created (most of the latest simulation tools creates automatically)<br>
  
&emsp;&emsp;3. Run the compile command with compile options<br>

&emsp;&emsp;i.e Cadence IES command for compile: ncverilog +access+rwc -compile fa.v<br>

&emsp;&emsp;Left side select the file and in Tools : launch verilog compiler with current selection will get enable. Click it to compile the code <br>

&emsp;&emsp;Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation <br>
<br>

![Screenshot 2024-10-05 094320](https://github.com/user-attachments/assets/f32e8576-f202-48bf-9ca6-8c90e008bad6)

<br>

**<p align="center">Fig 7: Compiled database in worklib** <br>

<br>
&emsp;&emsp;After compilation it will come under worklib you can see in right side window<br>

&emsp;&emsp;Select the test bench and compile it. It will come under worklib. Under Worklib you can see the module and test-bench. <br>

&emsp;&emsp;The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located.<br>

&emsp;&emsp;It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”<br>
<br>

**Step 2: Elaboration:– To check the port connections in hierarchical design**  <br>
<br>
&emsp;&emsp;Inputs: Top level design / test bench Verilog codes<br>

&emsp;&emsp;Outputs: Elaborate database updated in mapped library if successful, generates report else error reported in log file <br>

&emsp;&emsp;Steps for elaboration – Run the elaboration command with elaborate options <br>

&emsp;&emsp;It builds the module hierarchy<br>
	
&emsp;&emsp;Binds modules to module instances<br>
  
&emsp;&emsp;Computes parameter values<br>
  
&emsp;&emsp;Checks for hierarchical names conflicts<br>
  
&emsp;&emsp;It also establishes net connectivity and prepares all of this for simulation<br>
    
&emsp;&emsp;After elaboration the file will come under snapshot. Select the test bench and simulate it. <br>
<br>
![Screenshot 2024-10-05 094356](https://github.com/user-attachments/assets/e9ccbae6-b490-400a-825c-a6f5f08ed60c)

<br>

**<p align="center">Fig 8: Elaboration Launch Option** <br>

<br>

**Step 3: Simulation: – Simulate with the given test vectors over a period of time to observe the output behaviour.** <br> 
<br>
&emsp;&emsp;Inputs: Compiled and Elaborated top level module name <br>

&emsp;&emsp;Outputs: Simulation log file, waveforms for debugging <br>

&emsp;&emsp;Simulation allow to dump design and test bench signals into a waveform <br>

&emsp;&emsp;Steps for simulation – Run the simulation command with simulator options<br>
<br>

![Picture4](https://github.com/user-attachments/assets/e10f0858-6a89-4652-a2ca-71dd3cf9b395)

<br>

**<p align="center">Fig 9: Design Browser window for simulation** <br>

<br>

![Picture5](https://github.com/user-attachments/assets/7e1b075a-01ce-42c1-9c2d-2635539a9696)

<br>

**<p align="center">Fig 10: Simulation Waveform Window** <br>

<br>

![Picture7](https://github.com/user-attachments/assets/eb068722-97fa-4a8d-9318-e61795c165e2)

<br>

**<p align="center">Fig 11: Simulation Waveform Window** <br>

<br>

**Result:** <br>
<br>
&emsp;&emsp;The functionality of a 4bit_up-down asynchronous reset Counter was successfully verified using a test bench and simulated with the nclaunch tool.
