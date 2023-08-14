# IIITB_ASIC
## Day 0 

<details>
 <summary> Summary </summary>

  Installed the needed tools.

</details>	
	
 <details>
 <summary> Yosys </summary>
  
  I installed Yosys using the following commands:

  ```bash  
  git clone https://github.com/YosysHQ/yosys.git
  cd yosys-master 
  sudo apt install make 
  sudo apt-get install build-essential clang bison flex \
      libreadline-dev gawk tcl-dev libffi-dev git \
      graphviz xdot pkg-config python3 libboost-system-dev \
      libboost-python-dev libboost-filesystem-dev zlib1g-dev
  make 
  sudo make install
  ```
Below is the screenshot showing sucessful installation:
![image](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/00d73ed4-2207-4dd9-a57a-eac68fcb04ef)



Below is the screenshot showing sucessful launch:
![image](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/04cc4e16-3179-41b8-a22a-90ff37dcd33a)

</details>
 <details>
 <summary> OpenSTA </summary>
   
I installed and built OpenSTA (including the needed packages) using the following commands:
 ```bash
sudo apt-get install cmake clang gcctcl swig bison flex
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
```
Below is the screenshot showing sucessful installation:
![image](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/a36e4559-abd5-4fba-8f97-2acbcd7f9d92)
Below is the screenshot showing sucessful launch:
![image](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/999fc719-b6f8-4ce7-8028-4f66efe2ecf4)
</details>
 <details>
 <summary> iverilog </summary>
	 
 I installed iverilog using the following command:
  ```bash
sudo apt-get install iverilog
  ```
 Below is the screenshot showing sucessful launch:
 
![image](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/fd1861a0-3995-4f15-b0aa-f58e18e02082)
</details>
 <details>
 <summary> gtkwave </summary>

  I installed gtkwave using the following command:
```bash
sudo apt-get install gtkwave
```

 Below is the screenshot showing sucessful launch:
 ![image](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/21386995-18ef-4c1d-a188-b1d97fab11ce)
![image](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/05fc8a66-be0e-42fc-8189-71243c46cdf7)

</details>
 <details>
 <summary> magic </summary>


I installed magic using the following commands:
  ```bash
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
 ```
 Below is the screenshot showing sucessful launch:
 ![image](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/5e3c330f-8b2d-4f9f-a73c-6e781ca9d3b7)
</details>

## Day 1

<details>
 <summary> Verilog codes </summary>

  Here in this section I used the 2*1 mux which is taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
</details>
<details>
	<summary>Simulation</summary>
	
Below is the screenshot of code of goodmux and its testbench:
![goodmux](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/552e8728-67a3-43a3-bb54-b22fa3ed12b8)
	
Below is the gtkwave plot:
![gtkwave](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/c87070f6-dcc1-46fb-9976-f673ae6033e9)
</details>
<details>
	<summary>Synthesis: Yosys</summary>
	I used following commands to synthesize :
	
	
	yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
	yosys> read_verilog good_mux.v
	yosys> synth -top good_mux
	yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
	yosys> show

   Below is the screenshot of synthesized design:
   
   ![yosys](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/ec14dd89-6aa1-4e07-be66-b71de591e1da)
   
I used the following commands to generate the netlist:
 ```bash
 yosys> write_verilog mymux_netlist.v
 yosys> write_verilog -noattr mymux_netlist.v
 ```
Below is the screenshots for both: 

![netlist](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/2439985b-e072-406d-a89a-ed03de4f9cb6)
![noattr](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/6cd9948e-d76c-4327-bb75-3746fb97267d)

</details>

## Day 2

<details>
 <summary> Overview </summary>

  In this section, I embarked on a comprehensive synthesis process that encompassed various levels of design abstraction. Initially, I tackled the task of synthesizing a multiple module structure, composed of two distinct submodules. This synthesis endeavor took place both at the multiple module level, considering both hierarchical and flattened forms, as well as at the individual submodule level. The latter level of synthesis holds particular significance for two key reasons.
  Here I took the verilog codes from : https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
</details>

<details>
	<summary>Synthesis of Multiple_modules</summary>
	This segment of the study elucidates the synthesis process applied to multiple modules, emphasizing a departure from the single-module approach. The Yosys commands, previously outlined and discussed, form the cornerstone of this synthesis process, adapted and executed to accommodate two distinct design types.Below is 
	the commands for synthesis
	
	yosys> read_liberty -lib <path to lib file>
	yosys> read_verilog <path to verilog file>
	yosys> synth -top <top_module_name>
	yosys> abc -liberty <path to lib file>
	yosys> flatten
	yosys> show
	yosys> write_verilog -noattr <file_name_netlist.v>

  Below is the representation of hierarchy design.
  
  ![mulmod](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/367b38d8-99ff-46f2-8d6e-57f45b299b26)


 Below is the netlist.
 
 ![noattr](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/1f99673d-5d59-4680-973f-12411458e16e)

 And below is the flat code and design.
 
 ![flatcmd](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/329fa960-e360-41bc-810e-3526b92d8426)

![flatcode](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/b2f62f6c-d550-4b9d-8c22-7a05db80124e)


 ![flattenimg](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/8af15e87-9c85-4025-86ac-ba5248173f0f)

</details>
<details>
	<summary>Sub_module1 level
</summary>
Below is the schematic of submodule1.

 ![submodule1](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/61c7bea7-1786-4b36-aa95-7e047f92adf2)

</details>

<details><summary>
	Simulation of dff
</summary>
Below is the representation of dff with async reset.

![asyncReset](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/35102baa-7ca3-4eb4-af0f-895af9a7f355)

Below is the representation of dff with async set.

![asyncSet](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/b0c37d01-647c-47b7-b943-666b52612f20)

Below is the representation of dff with sync reset.

![syncReset](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/a5059c10-54f0-40a3-92c6-6a398322405f)

</details>

<details><summary>
	Synthesis of dff
</summary>
Below is the representation of dff with async reset.

![SasyncReset](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/f19796c8-7ed9-4921-a9f6-233f07f0e436)



Below is the representation of dff with async set.

![SasyncSet](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/aacdea48-5b17-4fad-b908-e61c28cdfb2d)


Below is the representation of dff with sync reset.

![SsyncReset](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/6e0d8c82-09ad-4391-b142-aaa4bf1d55a8)


</details>

<details><summary>
	Synthesis of mult_2.v and mult_8.v
</summary>

Below is the representation of synthesized design of mult2.

![mul2file](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/cca0aef9-f183-449c-a4a8-d99f962558f8)

![mul2](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/cee43580-913f-4dd5-be7f-57a70c1da116)


Below is the representation of synthesized design of mult8.

![mult8file](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/f3aac94f-0eba-4648-b586-d74c989249c9)

![mult8](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/6dd542e3-ed60-442f-9a50-bd557e2d4c52)


</details>

  ## Day 3
<details><summary>
	Overview
</summary> 
Within the expansive realm of ASIC design, the principles of optimization serve as the cornerstone for achieving enhanced performance, efficiency, and functionality. By employing techniques such as Boolean logic optimization, logic synthesis, and technology mapping, we can ensure that the combinational logic in your ASIC design is fine-tuned for optimal speed and efficiency.
</details>
<details> <summary>Combinational logic optimization</summary> 
Combinational optimization stands as a cornerstone in the process of ASIC design, focusing on logic circuits that produce output solely based on their current input values. At this stage, optimization is aimed at refining the logic gates and their interconnections to achieve minimal propagation delays, reduced power consumption, and compact layouts. Below are the commands
	
	yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
	yosys> read_verilog opt_check.v
	yosys> synth -top opt_check
	yosys> opt_clean -purge
	yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
	yosys> show

Below is the representation of the optimized design.

![optcheck](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/ebaf879b-9d1b-41ea-9426-87c5c6c60caf)


Below it the representation to view synthesized design of optimized optcheck_2.v (y=a?1:b)

![optcheck2](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/2065d93b-04bf-423b-b73f-923bbe15eee4)


Below it the representation to view synthesized design of optimized optcheck_3.v (y=a?(c?b:0):0)

![optcheck3](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/70244762-58d2-4a12-9a3f-a627ac457488)


Below it the representation to view synthesized design of optimized optcheck_4.v (y = a?(b?(a & c ):c):(!c))

![optcheck4](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/a7318da5-06db-4160-bc2a-71979991b89c)


Below it the representation to view synthesized design of optimized multiple_module_opt.v 

![multimodopt2](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/ed4ab85e-722f-4799-9007-4553267a4210)


</details>
<details><summary>
	Sequential logic optimizations
</summary>
Sequential optimization, on the other hand, delves into the complexities introduced by memory elements and feedback loops within a circuit. These components give rise to sequential logic, where the output depends not just on the current inputs but also on the previous states. Achieving optimal performance in sequential logic requires a holistic approach, incorporating factors like clock frequency, setup and hold times, and routing congestion. 

 Below is the command  to simulate the design of dff_const1.v
 
```
iverilog dff_const1.v tb_dff_const1.v
./a.out
gtkwave tb_dff_const1.vdc
 ```
<details><summary>dff_const1</summary>
Below is the representation of the obtained simulation

![wavedff1](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/ac0e1d94-3715-4570-b9f7-695dff470d61)


Below is the representation of syntesized design of optimized dff_const1.v

![Synthdff1](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/543a5741-03e4-48cf-bff1-5abb50d1b960)


</details>

<details><summary>dff_const2</summary>
Below is the representation of the obtained simulation

![wavedff2](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/b481f748-070c-4073-b2ad-155017c65a87)


Below is the representation of syntesized design of optimized dff_const2.v

![synth2](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/a00e4f40-706a-4d4e-8bae-8295b8a98869)


</details>

<details><summary>dff_const3</summary>
Below is the representation of the obtained simulation

![wavedff3](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/d0b8116e-ae01-4165-af26-1674dbbb4759)


Below is the representation of syntesized design of optimized dff_const3.v

![synth3](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/d28c3615-7f9e-4699-a35a-1a7816cc78ec)


</details>

<details><summary>dff_const4</summary>
Below is the representation of the obtained simulation

![wavedff4](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/201203b6-fe4b-43be-85b0-06b792bc6146)


Below is the representation of syntesized design of optimized dff_const4.v

![synth4](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/a0a6032a-f9a6-4751-ba23-b0884f11facb)


</details>

<details><summary>dff_const5</summary>
	
Below is the representation of the obtained simulation

![wavedff5](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/52d88382-92ab-4d49-98be-2184812e82ad)


Below is the representation of syntesized design of optimized dff_const5.v

![synth5](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/3d9e9a9d-b319-4825-8fda-af72474670a2)


</details>

<details><summary>counter_opt</summary>


Below is the representation of optimized design

![synthcounter](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/07e26d54-fd47-455e-ba89-6800bdb4cbab)


</details>

<details><summary>counter_opt2</summary>

Below is the representation of syntesized design

![synthcounter2](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/d7ba7d27-83c6-4d7d-89bf-9dbb908e00bb)


</details>

</details>

## Day 4

<details> <summary>
	Overview
</summary>
Gate-level simulation is a crucial aspect of digital hardware design and verification, especially in fields like VLSI, FPGA, and ASIC design. It involves simulating the behavior of a digital circuit at the gate level, which is the lowest level of abstraction in the design hierarchy. Gate-level simulation helps verify the correctness of a circuit's logic and functionality before fabrication or implementation on hardware.  

Blocking assignments are executed sequentially in the order they appear in the code. When a blocking assignment is encountered, the right-hand side (RHS) expression is evaluated immediately, and the signal on the left-hand side (LHS) is updated with the new value.
Non-blocking assignments, on the other hand, are not executed immediately. Instead, all non-blocking assignments within a procedural block are evaluated simultaneously at the end of the block's execution.

</details>

<details><summary> 
	Simulation and synthesis:ternary_operator_mux
</summary>

Below are the commands

```
iverilog <name verilog: ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vdc
```
Below is the obtained simulation which acts as mux


Below is the command and representation to synthesis the design into netlist of mux.

	yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
	yosys> read_verilog <name of verilog file: ternary_operator_mux.v>
	yosys> synth -top <name: ternary_operator_mux>
	yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
	yosys> write_verilog -noattr <name of netlist: ternary_operator_mux_net.v>
	yosys> show

Below is the obtained net file

</details>

[Reference Section]:#
## References
1. https://yosyshq.net/yosys/
2. https://steveicarus.github.io/iverilog/
3. https://gtkwave.sourceforge.net/
4. https://ngspice.sourceforge.io/
5. https://github.com/The-OpenROAD-Project/OpenSTA
6. http://opencircuitdesign.com/magic/
7. https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
 
