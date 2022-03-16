# Single_Cycle_Arm_Proc
A single cycle ARMv4 processor
Single Cycle ARM verilog and test bench code

--About--

This is a single-cycle Arm V4 processor takes inputs into decoder, decodes the commands and sends it to the datapath. 

  -The architectural state of the machine (excluding memory) is stored in registers: general-purpose registers and Current Program Status Register (CPSR).
  
  -There is a global wire called the “clock (clk)” that is connected to all the registers. The clock synchronizes all events for update
  
  -When a register sees a rising edge on the clock, the register captures the instantaneous “snapshot” of
   the values on its input. From then on, the register holds the captured values and feeds them to its
   output. (i.e., the clock edge basically activates a write).
   
  -The output from the register(s) are fed into a combinational circuit consisting of logic gates (e.g.,
   ADD) to instigate the control. In turn, the output from the logic gates are fed back as input to the
   register(s) that only change on the postive edge of the clock.
 
  -At the next rising edge on the clock, the register again captures the values on its input.
  
  -At each rising edge, the execution of an instruction is initiated. At the next rising edge, the values
   stored in all the registers (i.e., the architectural state) should be updated in such a way that the
   instruction can be considered to have correctly executed.
   
  -The Verilog model given utilizes a Harvard architecture. The code is loaded through the DO
    file at the beginning of simulation. 
  
    
    

      **To run simulation**
      1. Check that arm_single.do has memory file set to ********.dat file
      2. Open modelsim and change source directory
      3. Compile files inside of "Work" folder 
      4. Navigate to tools on tool bar and select tlc, run the .do file 
         --To change waveform values--
           -Change "-hex" to whatever base you want the values in 
     
      ** To create instruction code for simulation **
      1. Create a .x file and a .s file with the same name
      2. Open the .s file inside of Microsoft Visual Studio 
      3. add command code  \Line 1: .text
                           \Line 2: "Code goes here"
                           \line 3: .....
                           \Line 4: ....
                           \Line 5: swi #10
      4. Open inputs folder in powershell and run "python arm3hex "C:/Program Files (x86)/GNU Tools Arm Embedded/9 2019-q4-major/bin/arm-none-eabi-as.exe" (input_File).s (output_file).x"
      5. insert contents from .x file into .dat file
      6. Save and check that .do file is set to correct .dat file


  --Currently working on implementing instructions into the ALU--
  -Had to change ALU control bit size from 2 to 4 to create space for extra commands
  -Changing .do file to memfile2.do for new commands from hex codes compiled using arm3hex
  -Finished Data proccessing commands.

  --Need to do--
  -Ensure Data Processing instructions work with both Immediate and Register formats
  -Memory instructions should work with only offset based addressing
  -Ensure flags work with all commands. 
  -All instructions should support the list of condition codes that have been discussed in class. 
