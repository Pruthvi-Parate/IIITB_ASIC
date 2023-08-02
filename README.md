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

[Reference Section]:#
## References
1. https://yosyshq.net/yosys/
2. https://steveicarus.github.io/iverilog/
3. https://gtkwave.sourceforge.net/
4. https://ngspice.sourceforge.io/
5. https://github.com/The-OpenROAD-Project/OpenSTA
6. http://opencircuitdesign.com/magic/
 
