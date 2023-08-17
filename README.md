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
gtkwave tb_ternary_operator_mux.vcd
```
Below is the obtained simulation which acts as mux

![simtern](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/830066ba-fa93-410c-9fb6-1cffe3ecc9c6)

![synthtern](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/4751c1c3-6de4-49be-a663-d7598179bbf3)


Below is the command and representation to synthesis the design into netlist of mux.

	yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
	yosys> read_verilog ternary_operator_mux.v
	yosys> synth -top ternary_operator_mux
	yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
	yosys> write_verilog -noattr ternary_operator_mux_net.v
	yosys> show

Below is the obtained net file

![ternnetlist](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/bf46f287-2de8-4fe2-b5c7-c0c0cb2d86b8)


Below is the commands GLS of mux

```
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to sky130_fd_sc_hd__tt_025C_1v80.lib: ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib> <name netlist: ternary_operator_mux_net.v> <name testbench: tb_ternary_operator_mux.v>
./a.out
gtkwave tb_ternary_operator_mux.vcd
```

Below is the simulation which matches with pre-synthesis simulation

![postsimtern](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/b49838e9-8c41-4a13-89b0-820dadb78fd3)


</details>

<details><summary> Simulation and synthesis:bad_mux</summary>

 Below are the commands to simulate bad_mux

  In the provided screenshot below of the simulation results, it is apparent that a concerning behavior has been observed. Specifically, the discrepancy arises when the inputs undergo alterations. In this context, it is evident that the variable "y" fails to undergo evaluation. This outcome contradicts the expected behavior and signifies an anomaly in the simulation process. 

![simmux](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/5a4f9f9f-4e4e-495d-a5e7-1785b912d4ab)


Below is the command to synthesize the design into netlist

	yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
	yosys> read_verilog  bad_mux.v
	yosys> synth -top bad_mux
	yosys> abc -liberty sky130_fd_sc_hd__tt_025C_1v80.lib
	yosys> write_verilog -noattr bad_mux_net.v
	yosys> show

Below is the representation of design

![synthmux](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/e773a738-f511-42d4-be5e-b125fd604448)


Below is the netlist

![netlist](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/e75eb526-e682-450f-b0f1-ae7d9cd959fd)


Below is the commands GLS of mux

```
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to sky130_fd_sc_hd__tt_025C_1v80.lib: ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib> <name netlist: bad_mux_net.v> <name testbench: tb_bad_mux.v>
./a.out
gtkwave tb_bad_mux.vdc
```

Below is the representation of obtained simulation and as you can see it's not matching up with the simulation we did before which was pre-synthesis simulation

</details>

<details><summary>
	Simulation and synthesis: blocking_caveat.v
</summary>
	
Below is the commands to simulate blocking_caveat

 ```
iverilog blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```
Displayed below is a visual representation , showcasing the outcome of the simulation we've conducted. Notably, upon careful observation, it becomes evident that the variable "d" is retaining or holding on to its previous values. Strikingly, this behavior is akin to what one might expect from a flip-flop in a circuit, even though the circuit configuration in question does not involve an actual flip-flop component. This incongruence with the intended design and function of the circuit constitutes an incorrect behavior, indicating a deviation from the anticipated simulation results.

![simulationpre](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/f86aeae0-12cb-422d-a78d-d212d1255895)


Below is the synthesis of the design

![synth](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/4747ca8d-4a53-4f3a-aed5-6d9cc5dcc2f2)


Below is the netlist showing

![netlist](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/295d8434-77fb-483b-9f0c-a60fbbd4b768)


Below is the commands GLS of blocking_caveat 

```
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to verilog model: ../mylib/verilog_model/sky130_fd_sc_hd.v> <name netlist: blocking_caveat_net.v> <name testbench: tb_blocking_caveat.v>
./a.out
gtkwave tb_blocking_caveat.vdc
```

Below representation shows an evident dissimilarity arises when comparing this simulation result with the simulation executed prior to the synthesis stage. The primary reason for this disparity can be attributed to the presence of a blocking statement within the design. 



</details>

## Day 5

<details><summary>Overview</summary>
	
In the realm of ASIC VLSI system design, efficient decision-making and control flow mechanisms are paramount to achieving optimal performance and functionality. This is where conditional constructs such as "if" and "case" statements play a pivotal role. These statements serve as powerful tools for directing the behavior of digital circuits, allowing designers to create dynamic responses based on specific conditions or input values. In this context, the intricate interplay between these conditional statements and the underlying hardware architecture forms the cornerstone of crafting sophisticated and responsive ASIC designs.Below shown hardware representation

![WhatsApp Image 2023-08-15 at 2 28 19 PM](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/fce217f0-6689-4b57-bd08-68d28b348078)

![WhatsApp Image 2023-08-15 at 2 28 19 PM (1)](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/7b01a184-a5fc-41e3-a3ef-b5ea0378063e)



</details>

<details><summary>Simulation and synthesis of incomp_if</summary>

Presented below is a representation of simulation and synthesis showcasing the outcome of the simulation process. Upon analysis, it becomes evident that an inferred latch has materialized within the design. This inference is drawn from the observation that the output consistently retains a constant value during instances when the "select" signal fails to achieve a high state.

![sim](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/cc6d44b1-09b7-4580-a6cd-1ad9be1fd976)

![synthif](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/dddffa3c-8df3-40fc-89ec-5de71965cc4f)


</details>

<details><summary>
	Simulation and synthesis of incomp_if2
</summary>
	
Below is shown simulation and synthesized representation of incomp_if2

![sim2](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/e1f4b047-e004-4bb8-9a67-0216f79cc444)

![synth2](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/7365230c-93e3-46d0-ac65-5a33cc0ee0ed)

 
</details>

<details><summary> Simulation and synthesis of incomp_case and comp_case</summary>
In essence, a "case" statement involves evaluating a given expression against a set of predefined conditions, known as case values. Once a match is found between the expression and a case value, the associated block of logic is executed. This allows for the implementation of various pathways based on different input scenarios.

![WhatsApp Image 2023-08-15 at 2 38 38 PM](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/629fbd4f-8d3e-4639-8384-a31e2c2996be)

 
following are the commands

```
iverilog comp_case.v tb_comp_case.v
./a.out
gtkwave tb_comp_case.vcd
```

Below is shown representation of simulation and synthesis. This behavior specifically manifests when the "select" signal is assigned a value of either 2 or 3, with particular emphasis on the condition where the second bit of the "select" signal, denoted as sel[1], asserts a logic level of 1.

![compsim](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/589c1cdd-07a2-416b-842e-c2c7f943a699)

![compsynth](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/1ded7ad9-ab9b-47e4-8522-291142549ee0)

 Below is the representation of incomp_case

![sim](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/1b7f94b4-2ab4-4fc6-8f1d-0753cd2aa156)

![synth](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/8efbce99-bd54-4d68-9cd7-0f033bd41ca0)

 
</details>

<details><summary>Synthesis of partial_case_assign</summary>

Displayed here is a representation of the design achieved, and within it, a clear outcome aligns with our expectations. As anticipated, a single latch materializes, governing the behavior of the x output. Moreover, the boolean expressions we foresaw for both x and y are convincingly deduced by the design itself. This means that the logic we intended for x and y, the way they should operate based on specific conditions, is accurately recognized and implemented by the design.

![partialcase](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/d29999cb-1dc5-4273-b6ec-20072a4f91ea)



</details>

<details><summary>Simulation, synthesis, and GLS of bad_case</summary>

 Below is the representation of bad_case. When the "select" input is set to the binary value "11," a puzzling situation arises within the simulation. In this circumstance, the simulator appears to grapple with determining the appropriate course of action, resulting in the y output steadfastly assuming a constant value of "1."

![sim](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/4a229020-f5eb-49f1-8273-cee1164978d1)

![synth](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/801fba72-cef6-4d7c-9ee3-7fcfabd30d85)


 Below are the commands for GLS
 ```
iverilog  ../mylib/verilog_model/primitives.v ../mylib/verilog_model/sky130_fd_sc_hd.v bad_case_net.v tb_bad_case.v
./a.out
gtkwave tb_bad_case.vcd
```

Below is the simulation in which we can see the mismatch

![Gls-sim](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/e6059b11-1a61-4173-82c3-45f810dc8cdf)


</details>

<details><summary>Simulation, synthesis, and GLS of  mux_generate</summary>

Below is the representation simulation of mux_generate which is 4*1 mux

![sim](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/3f2d744d-bc84-4420-98ef-b0abff8315e4)

![synth](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/7bc6d12b-4617-48e4-929a-a01034ccced0)


To obtain GLS below are the commands 

```
iverilog  ../mylib/verilog_model/primitives.v ../mylib/verilog_model/sky130_fd_sc_hd.v mux_generate_net.v tb_mux_generate.v
./a.out
gtkwave tb_mux_generate.vcd
```

Below is the resulted simulation which completely matches with previous one

![glssim](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/f7e39bd0-ba8b-4f2e-b8b5-46618b5af8ff)


</details>

<details><summary>demux_case</summary>

Below is the representation of demux_case and by observing it is 1*8 demux

![sim](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/0d40008b-caae-4805-8be1-9a4df7d3476e)


</details>

<details><summary>demux_generate</summary>

Below is the representation of demux_generate and by observing it is 1*8 demux

![sim](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/96172813-2099-4a3e-99e4-84803e637bd2)


Below is the synthesized design representation

![genrateSynth](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/3d501c44-5b7a-484a-8870-a29321d75bff)


For GLS below are the commands

```
iverilog  ../mylib/verilog_model/primitives.v ../mylib/verilog_model/sky130_fd_sc_hd.v demux_generate_net.v tb_demux_generate.v
./a.out
gtkwave tb_demux_generate.vcd
```

Below is shown the simulation which is perfectly matches with the previous one

![Gls](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/dcba932f-419f-49eb-85f5-d352332ac316)



</details>

<details><summary>RCA</summary>
	
Below is the representation of rca and by observing it is 8bit rca

![sim](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/518c7364-880c-4bc2-9491-058af91e0d6b)


Below is the synthesized version of 8bit rca

![synth](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/ce31432d-60be-4d51-89e4-0cfa83f8c2dd)


To obtain GLS below are the commands

```
iverilog  ../mylib/verilog_model/primitives.v ../mylib/verilog_model/sky130_fd_sc_hd.v rca_net.v tb_rca.v
./a.out
gtkwave tb_rca.vcd
```

Below is the simulation which perfectly matches with the previous one

![gls](https://github.com/Pruthvi-Parate/IIITB_ASIC/assets/72121158/70a76c8d-f8b5-4813-9197-90129fa5fb48)


## Day 6

<details>
<summary>
</summary>
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
 
