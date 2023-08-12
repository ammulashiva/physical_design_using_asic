# physical_design_using_asic

[Day 0](#day-0) installation of required softwares

[Day 1](#day-1) getting familiar with yosys, iverilog and gtkwave

[Day 2](#day-2)

[Day 3](#day-3)



## Day 0 

<details>
<summary> Summary </summary>
    I installed the needed tools.
    
</details>

<details>
    <summary>Yosys</summary>
    
I installed yosys using following commands :
```bash

$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys-master 
$ sudo apt install make (If make is not installed please install it) 
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make config-gcc
$ make 
$ sudo make install
```

below is the screenshot showing successful launch: 
![yosys](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/76ecfa86-4e5b-4bba-9c75-d0e98fed2b19)
</details>
<details>
    <summary>Iverilog</summary>

I installed Iverilog using following commands:
```bash
sudo apt-get install iverilog
```
below is the screenshot showing successful launch: 
![Iverilog](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/4106244b-db39-42e5-bc5d-e43dfe40a297)
</details>
<details>
    <summary>gtkwave</summary>

I installed gtkwave using following command:
```bash
sudo apt update
sudo apt install gtkwave
```
below is the screenshot showing successful launch:

![gtkwave](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/63bef04c-b53d-4175-b326-7212f403652c)
</details>

<details>
    <summary>OpenSTA</summary>

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
below is the screenshot showing successful launch: 
![OpenSTA](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/3ce1cccc-a154-4071-a9c8-682bc4c57fb2)
</details>

<details>
    <summary>ngspice</summary>

i downloaded the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory, and unpacked it using following commands:
```bash
$ tar -zxvf ngspice-37.tar.gz
$ cd ngspice-37
$ mkdir release
$ cd release
$ ../configure  --with-x --with-readline=yes --disable-debug
$ make
$ sudo make install
```
Below is the screenshot showing sucessful installation:

![ngspice](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/64efc675-08ed-4c9e-a4da-c6554baac603)
</details>

<details>
    <summary>magic</summary>

I installed magic using the following commands:
```bash
$   sudo apt-get install m4
$   sudo apt-get install tcsh
$   sudo apt-get install csh
$   sudo apt-get install libx11-dev
$   sudo apt-get install tcl-dev tk-dev
$   sudo apt-get install libcairo2-dev
$   sudo apt-get install mesa-common-dev libglu1-mesa-dev
$   sudo apt-get install libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
make install
```
Below is the screenshot showing sucessful installation:

![magic1](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/2ca1576d-839c-4e49-9574-a5e3e05c6083)

Below is the screenshot showing sucessful launch:

![magic2](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/bd855d1b-fce5-467c-8922-1dd30d994c64)
</details>

## Day 1

<details>
<summary>Summary</summary>
    
             This section shows how I downloaded the libraries needed for the synthesys of verilog file and how i simulated and synthesized a 2x1 mux using iverilog and yosys respectively. 

</details>

<details>
    <summary>Downloading Verilog codes and libraries</summary>
    The verilog codes of the 2x1 mux (good_mux.v) and its testbench (tb_good_mux.v) are taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
    and installed using the commands :
    ```bash
    
         # mkdir VLSI
         # cd VLSI
        # git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
    ```
    Below image shows the library path i have downloaded :
  ![download_v_files](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/88f44d88-e652-462e-a656-11cc84c2b9a7)

    
</details>
<details>
    <summary>Simulation: Iverilog and gtkwave</summary>
     I used the following commands to simulate and view the plots of the RTL design:
	    here good_mux.v and tb_good_mux.v are the rtl code and testbench files respectively
	
```bash
   $ iverilog good_mux.v tb_good_mux.v
   $ ./a.out
   $ gtkwave tb_good_mux.vcd
```
 
 Below is the screenshot of the gtkwave plots:
	
  ![mux_gtkwave](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/2ed5db9b-fa75-4815-a94c-6011d9f6a887)
	
</details>
<details>
	<summary>Synthesis: Yosys</summary>
 In the directory of the verilog files, I used the following commands to synthesize and view the synthesized deisgn:
	
 ```bash
# yosys
yosys> read_liberty -lib <path to lib file> //path <..lib/sky130_fd_sc_hd__tt_025c_1v80.lib>
yosys> read_verilog <path to verilog file> //path <good_mux.v>
yosys> synth -top <top_module_name> //good_mux
yosys> abc -liberty <path to lib file> //path <..lib/sky130_fd_sc_hd__tt_025c_1v80.lib>
yosys> show //shows the synthesied design
 ```
 Below is the screenshot of the synthesized design:
	

	
 I used the following commands to generate the netlist:
 ```bash
 yosys> write_verilog <file_name_netlist.v>
 yosys> write_verilog -noattr <file_name_netlist.v>
 ```
 Below is the Screenshot showing the ABC results :
 
![yosys_synthesis](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/d9c25654-95a2-4f49-bff8-899fc9e2681e)
 
 Below is the screenshot of the generated netlist:

 ![circuit_lib](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/85261fcf-58c3-4020-815e-b36f88c88f6d)
 
</details>

 
## Day 2
<details>
	<summary>Summary</summary>

 Timing libs,Hierarchical vs flat synthesis and efficient flop coding styles
 
</details>

<details>
	<summary>intro. to timing libs.</summary>

 To view the contents inside the .lib file type the following command :

 ```bash
    cd VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/
    gvim sky130_fd_sc_hd__tt_025C_1v80.lib
 ```
    ![timing_lib](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/4f542fd2-7f69-4a0b-8a31-e41830a56114)

    One of the fundamental parameters stored within .lib files comprises P.V.T. parameters, where P denotes Process, V denotes Voltage, and T denotes Temperature. The variations in these parameters can cause significant changes in the performance of circuits.

    Process Variation: During the manufacturing process, there may be some deviations in the transistor characteristics, causing non-uniformity across the semiconductor wafer. Critical parameters like oxide thickness, dopant concentration, and transistor dimensions experience alterations.

    Voltage Variation: Voltage regulators might exhibit  variability in their output voltage  over time, inducing fluctuations in current and  impacting the operational speed of the circuits.

    Temperature Variation: The functionality of a semiconductor devices is sensitive to changes in temperature, it effects various parameters that significantly alters the transfer function.
     
    The .lib library is bucket with full of cells as shown below:
    
![different cells](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/238e3699-d6a9-4910-926d-13ef53ef827c)

This file also defines the units for parameters like voltage, power, current, capacitance, and resistance. Within the .lib library, each standard cell consists a set of parameters specific to that cell's features.

Consider the a2111oi gate whose parameters and verilog files is shown below:

![cell_a2111o](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/43f3f2b8-21da-446e-96e4-a7974d869fba)

each cell defines the voltage , temoerature, power leakage , area etc.. in all combinations of inputs for the synthesiser.

</details>

<details>
	<summary>hierarchial vs flat synthesis</summary>

  Consider the verilog file multiple module which is given in the verilog_files directory shown below:

![multiple_modules](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/553a02f3-6dfa-409a-a765-e9c839a98c6a)

In this case the module multiple_modules iinstantiates two sub_modules where the sub_module1 implements the AND gate and sub_module2 implemets the OR gate which are integrated in the multiple_modules. Synthesis the multiple module using the sollowing commands:

```bash

#yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules // synthesis of multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules  //cmd to view the synthesised design in blocks of sub_modules
write_verilog -noattr multiple_modules_hier.v  //creates the netlist in hirearichal modules
!gvim multiple_modules_hier.v  // view the net list

```
Below is the figure showing the schematic of multiple_modules:

![multiple_modules_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/fe6b563b-7680-4e1d-bb9c-250e9a523841)

Below is the netlist generated with sub_modules :

![multiple modules _hier](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/4873c3b5-20bf-4604-a9ef-4f2a9960518c)

  
</details>





