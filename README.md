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


