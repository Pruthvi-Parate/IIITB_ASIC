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

[Reference Section]:#
## References
1. https://yosyshq.net/yosys/
2. https://steveicarus.github.io/iverilog/
3. https://gtkwave.sourceforge.net/
4. https://ngspice.sourceforge.io/
5. https://github.com/The-OpenROAD-Project/OpenSTA
6. http://opencircuitdesign.com/magic/
 
