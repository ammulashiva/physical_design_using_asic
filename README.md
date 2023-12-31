# physical_design_using_asic



## Day 0 - Installation of Required Softwares

<details>
<summary> <strong>Summary</strong> </summary>
    I installed the needed tools.
    
</details>

<details>
    <summary><strong>Yosys</strong></summary>
    
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
    <summary><strong>Iverilog</strong></summary>

I installed Iverilog using following commands:
```bash
sudo apt-get install iverilog
```
below is the screenshot showing successful launch: 
![Iverilog](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/4106244b-db39-42e5-bc5d-e43dfe40a297)
</details>
<details>
    <summary><strong>gtkwave</strong></summary>

I installed gtkwave using following command:
```bash
sudo apt update
sudo apt install gtkwave
```
below is the screenshot showing successful launch:

![gtkwave](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/63bef04c-b53d-4175-b326-7212f403652c)
</details>

<details>
    <summary><strong>OpenSTA</strong></summary>

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
    <summary><strong>ngspice</strong></summary>

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
    <summary><strong>magic</strong></summary>

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

## Day 1 - Getting familiar with Yosys, Iverilog and gtkwave

<details>
<summary><strong>Summary</strong></summary>
    
This section shows how I downloaded the libraries needed for the synthesys of verilog file and how i simulated and synthesized a 2x1 mux using iverilog and yosys respectively. 

</details>

<details>
    <summary><strong>Downloading Verilog codes and libraries</strong></summary>
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
    <summary><strong>Simulation: Iverilog and gtkwave</strong></summary>
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
	<summary><strong>Synthesis: Yosys</strong></summary>
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

 
## Day 2 - Timing libs,Hierarchical vs Flat Synthesis and Efficient Flop Coding Styles
<details>
	<summary><strong>Summary</strong></summary>

 viewed the Timing libs learnt some fundamental parameters in .lib file , done some examples on Hierarchical vs flat synthesis and efficient flop coding styles and learnt some of the basic optimizations . 
 
</details>

<details>
	<summary><strong>Intro. to timing libs.</strong></summary>

 To view the contents inside the .lib file type the following command :

 ```bash
    cd VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/
    gvim sky130_fd_sc_hd__tt_025C_1v80.lib

 ```

![timing_lib](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/4f542fd2-7f69-4a0b-8a31-e41830a56114)

**O**ne of the fundamental parameters stored within .lib files comprises P.V.T. parameters, where P denotes Process, V denotes Voltage, and T denotes Temperature. The variations in these parameters can cause significant changes in the performance of circuits.

**Process Variation:** During the manufacturing process, there may be some deviations in the transistor characteristics, causing non-uniformity across the semiconductor wafer. Critical parameters like oxide thickness, dopant concentration, and transistor dimensions experience alterations.

**Voltage Variation:** Voltage regulators might exhibit  variability in their output voltage  over time, inducing fluctuations in current and  impacting the operational speed of the circuits.

**Temperature Variation:** The functionality of a semiconductor devices is sensitive to changes in temperature, it effects various parameters that significantly alters the transfer function.
     
    The **.lib** library is bucket with full of cells as shown below:
    
![different cells](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/238e3699-d6a9-4910-926d-13ef53ef827c)

This file also defines the units for parameters like voltage, power, current, capacitance, and resistance. Within the .lib library, each standard cell consists a set of parameters specific to that cell's features.

Consider the a2111oi gate whose parameters and verilog files is shown below:

![cell_a2111o](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/43f3f2b8-21da-446e-96e4-a7974d869fba)

each cell defines the voltage , temoerature, power leakage , area etc.. in all combinations of inputs for the synthesiser.

</details>

<details>
	<summary><strong>hierarchial vs flat synthesis</strong></summary>

  Consider the verilog file multiple module which is given in the verilog_files directory shown below:
  
![multiple_modules](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/587aee2f-aa90-4455-b3a5-8480999e1727)

In this case the module multiple_modules iinstantiates two sub_modules where the sub_module1 implements the AND gate and sub_module2 implemets the OR gate which are integrated in the multiple_modules. Synthesise the multiple module using the sollowing commands:

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
Below is the figure showing the **schematic of multiple_modules:**

![multiple_modules_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/fe6b563b-7680-4e1d-bb9c-250e9a523841)

Below is the **netlist** generated with sub_modules :

```bash

module multiple_modules(a, b, c, y);
  input a;
  wire a;
  input b;
  wire b;
  input c;
  wire c;
  wire net1;
  output y;
  wire y;
  sub_module1 u1 (
    .a(a),
    .b(b),
    .y(net1)
  );
  sub_module2 u2 (
    .a(net1),
    .b(c),
    .y(y)
  );
endmodule

module sub_module1(a, b, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  wire a;
  input b;
  wire b;
  output y;
  wire y;
  sky130_fd_sc_hd__and2_0 _3_ (
    .A(_1_),
    .B(_0_),
    .X(_2_)
  );
  assign _1_ = b;
  assign _0_ = a;
  assign y = _2_;
endmodule

module sub_module3(a, b, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  wire a;
  input b;
  wire b;
  output y;
  wire y;
  sky130_fd_sc_hd__or2_0 _3_ (
    .A(_1_),
    .B(_0_),
    .X(_2_)
  );
  assign _1_ = b;
  assign _0_ = a;
  assign y = _2_;
endmodule
```

## Flat Synthesis
   Flattening the hierarchy means simplifying the hierarchical structure of a design by collapsing or merging lower-level modules or blocks into a single, unified representation. In yosys the flattening can be done with flat command. Yosys illustration of flattening the hiererchy.
   ```bash

root@ammula-shiva-kumar-HP-Laptop-15-da1xxx:/home/ammula-shiva-kumar/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files# yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
flatten
write_verilog -noattr multiple_modules_flat.v
!gvim multiple_modules_flat.v

```
  Below is the figure showing the netlist of the multiple_modules after flattening :

  ![multiple_modules_flat](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/09e70b0f-0a26-44bf-8055-94f9369de3c0)

  Below figure shows the schematic ofmultiple modules after flattening :
  
![multiple_modules_flat_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/5e29ab99-df3e-4e6a-a47c-73bfc87a78c1)

### Steps to synthesise sub module

Suppose a multiplier design needs to be used in numerous instances. Rather than undergoing synthesis six times independently, the preferred approach is to synthesize it once and then duplicate it within the primary module. Using module-level synthesis becomes advantageous when dealing with multiple occurrences of identical modules. Another reason for synthesizing submodule is to follow the principle of divide and conque for extensive designs that may not be optimized effectively, synthesizing the design module by module ensures that each module is effectively optimized.
    
    The commands used in Yosys to Synthesise submodule are:

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top sub_module1
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
Below figure shows the Schematic of submodule :

![multiple_modules_submodule1](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/e1f77a95-7512-45fd-b782-09966a06b0b2)

</details>

<details>
	<summary><strong>Various Flop coding styles and optimizations </strong></summary>

 ### Flops and flop Coding Styles
 
**A** flop is a Storage element which can store the data Synchronously or asynchronously, it has a input clock and a set and a reset ,the set and reset can be synchronous or asynchronus . for example if there is a large combinational circuit between two registers then it may lead to setup violation so in order to solve the problem we need to use a flop in between the combinational circuit so that the delay gets divided and setup violation doesnt happen.
     below are the various flops with different configurations:
     
     **Code** for asynchronous set d flop :
     
```bash
     module dff_async_set ( input clk ,  input async_set , input d , output reg q );
     always @ (posedge clk , posedge async_set)
begin
	if(async_set)
		q <= 1'b1;
	else	
		q <= d;
end
endmodule

```
Code for **synchronous reset d flipflop** :

```bash

module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk )
begin
	if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule

```

Code for **asynchronous and synchronous reset d flop** :

```bash

  module dff_asyncres_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
  always @ (posedge clk , posedge async_reset)
  begin
	if(async_reset)
		q <= 1'b0;
	else if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
  end
 endmodule

```
Code for **asynchronous reset d flop** :

```bash

module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
	if(async_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule

```
## Simulation of above flops

The synthesis and simulation of verilog files can be done by usind the following commands:

```bash

$iverilog <Filename.v>
$./a.out
$gtkwave <dumpfile_name.vcd>

```
Below figure shows the simulation of **asynchronous set d flop** :

![async_set_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/13a6f7b6-b059-4e12-a94d-0653722c2c86)

Below figure shows the simulation of  **synchronous reset d flipflop**:

![sync_res_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/063079d3-852b-44cd-b958-cc388e9d63dd)

Below figure shows the simulation of **asynchronous and synchronous reset d flop** :

![asyncres_syncres_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/07dcb88c-c515-471b-93f2-b13ef1fe28c9)

Below figure shows the simulation of **asynchronous reset d flop** :

![async_res_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/ec714932-6a80-4943-bcfc-3d43cd13404a)

## Some optimizations

Consider the module **mul2.v** shown below:

```bash

module mul2 (input [2:0] a, output [3:0] y);
	assign y = a * 2;
endmodule

```
Here 'a' is 3 bit and 'y' is 4 bits wide . when a is multiplied by 2 'a' gets shifted to left by 1 bit so the output should be just 'a' is connected to y[2:0] and y[3] connected ground
now let us see how the optimizations will be done 
 here in the below figure we see that theoutput is as i have described:

 ![mult_2_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/c31b7665-a331-430c-bf49-b3ce7f7caf0f)


 Now consider the module **mult_8.v** shown below:

```bash

module mult8 (input [2:0] a , output [5:0] y);
	assign y = a * 9;
endmodule

```
Here 'a' is 3 bit and 'y' is 6 bits wide . when a is multiplied by 9 'a' , here y can be written as 

  y = a * (8+1) ;
  
  y = a * 8 + a ;
  
  therefore here 'y'gets shifted to left by 3 bits and a'a' is added, so the output should be just '{a, a}' Here 'a' is stacked 2 times to get 'y'. now let us see how the optimizations will be done 
 here in the below figure we see that theoutput is as i have described:

 ![mult8_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/bce8a772-05c0-4de7-9517-d0625f7f33b0)
 
 
</details>

## Day 3 - Combinational and Sequential Optimizations
 <details>
	 <summary><strong>Summary</strong></summary>
	 
**Here** combinational and sequential logics have been introduced and some examples were done on sequential and combinational optimisations.
       
 </details>

<details>
	<summary><strong>Intro.to Optimizations</strong></summary>

### Combinational logic OPtimizations

#### squesing the logic to get the most optimised design
   - Area and power savings
#### Constant Propagation
 - Direct optimisation
#### Boolian logic Optimisations
 - K-Map
 - Quine-Mckluskey

      Here let us consider an example of **constant propagation** as shown in the below figure :

![constant_propagation_ex](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/8b784e64-1eb8-4255-a3ba-01de4fada482)

here **Y= ((AB)+C)'**

If **A = 0** ;then
       
**Y = C'**

**In** this example A is constant so the logic got opthe boolian equation is optimisedimised so the number of transisters and area got reduced.

Now consider another example in **boolian logic optimization** :

**A?(B?C:(C?A:0)):(!C)**

=>** A'C' +A[BC+B'AC}**

=>** A'C' + ABC + AB'C**

=> **A'C' + AC[B+B']**

=> **A'C' + AC **

In this example the boolian equation is **optimised**. 

### Sequential Logic Optimisations

#### Basic
 - Sequential constant Propagation
#### Advanced [not covered as a part ]
 - State Optimization
 - Retiming
 - sequential logic cloning

Consider an example in sequential logic as shown in the below figure:

![sequential_ex](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/bf639199-3060-44f4-bb22-58f19f6757e3)

here as D is grounded 'Q' is always '0' So

**Y = (A.0 )'**

=>** y = 1** (Optimised)

</details>

<details>
	<summary><strong>Combinational LOgic Optimisations</strong></summary>

 Consider an example shown below

 ```bash

 module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule

```
Here **y = a'.0 + a.b**

 => **y = a.b **

 the commands used in yosys are :

 
```bash

#yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check.v
synth -top opt_check // synthesis of multiple_modules
opt_clean -purge  // cleans all the unused cells
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show

```
 
 synthesised the code using yosys and the schematic is shown below :

![opt_check_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/a7842ea5-88a4-461d-9092-38ef95854817)


**Example 2** :

```bash

 module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule

```
here 

**Y = a'b +a**

=>** Y = a + b** ;

the synthesised schematic is shown below :

![opt_check2_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/92cd7042-95ef-4579-8429-fdee7f58ca1b)


 **Example 3** :

```bash

module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule

```
here 

**Y = a'0 + a[a'.0 +ab]**

=>** 0+ abc**

=> **Y = a.b.c **;

the synthesised schematic is shown below :

![opt_check3_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/fcfe7f28-e7f4-4823-afef-5b47fd761452)

</details>


<details>
	<summary><strong>Sequential LOgic Optimisations</strong></summary>

 Consider an example **1** of **sequential circuit** :

 ```bash
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end

endmodule

```
here use the command dfflibmab -liberty ../lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib to include the dff libs
the synthesied schematic is shown below :

![dff_const1](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/368b1b7d-9376-4e7c-b3c1-f5a0ad4fc972)

**Example 2**:

```bash
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end

endmodule

```
here use the command dfflibmab -liberty ../lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib to include the dff libs
the synthesied schematic is shown below :


![dff_const2](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/85b07b6f-447e-4ec1-8c6c-69247ac0333b)

**Example 3**:

```bash
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule

```

here in the above example the outputQ depends on the previous input of the input Q1 so both flops should be present so cannot be optimised further
as shown in the below figure :

![dff_const3_diagram](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/6764fc12-28b6-441e-b12e-b6b86c0e127b)


**Here** use the command dfflibmab -liberty ../lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib to include the dff libs
the synthesied schematic is shown below :

![dff_const3](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/b79d7ad5-9714-4009-b04f-e8ca80ea29a8)



</details>


<details>
	<summary><strong>sequential optimisations for unused outputs</strong></summary>

     consider an example shown below :

```bash

module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end
 
endmodule

```

**Here** the bits count[1:2] are unused onlythe bit cunt[0] is used so other redundancy bits are removed in the synthesis 
the synthesised schematic is shown below :

![counter_opt_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/3c988a17-2728-4083-b5f6-f759d595efd8)

      
</details>

## Day 4 -  GLS, Blocking vs non Blocking and Synthesis - Simulation mismatch
<details>
	<summary><strong>GLS, Blocking vs non blocking and Synthesis -simulation mismatch</strong></summary>

 ## GLS Concepts And Flow Using Verilog

  **GLS**- Gate level Synthesis 

Here gate level netlist is taken and the testbench for it and the Gte level verilog models are given to the iverilog to generate a value change dump format which is then given to the gtkwave to view the output .

Below figure shows the process :

![GLS](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/7adfa7ce-5dff-4d4e-bab1-4781d0ee9895)

There is a need to check the netlist after the synthesis because there can be a mismatch. 

# Reasons to Synthesis And Simulation Mismatch :
 - Missing Sensitivity List
 - Blocking VS Non Bolcking List
 - Non standard Verilog Coding

 Consider an example for missing sensitivity list :

 ```bash

module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (sel)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule

```
**I**n the above code when 'sel changes the always block is evaluated and the 'y' values get updated. But for a mux 'y' gets updated when ever the value of 'i0' or 'i1' changes with respect to the 'sel' value so the simulatior shows the wrong value/output . so in order to correct that that we need to replace the always block sensitivity list with '*' . as shown below :

 ```bash

module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule

```

### Blocking And Non Blocking Statements in Verilog :


#### Inside Always Block
 - if we use operator '=' then
 - executes the ststments in the order it is written
 - so the first statment is evaluated before the second statment

#### Inside Always Block
 - if we use operator '<=' then
 - executes all the RHS when always block is entered and assigns to LHS .
 - Parallel Evaluation .
      
</details>

<details>
	<Summary><strong>Labs On GLS and Synthesis Simulation Mismatch </strong></Summary>

Condider an example shown below:
```bash

module ternary_operator_mux (input i0 , input i1 , input sel , output y);
	assign y = sel?i1:i0;
endmodule

```

First create the **netlist** using the below commands in yosys :

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog ternary_operator_mux.v
synth -top ternary_operator_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog ternary_operator_mux_net.v
exit

```
**Next** use the iverilog with the files netlist, test bench primitives and skylab.v in mylib folder using the following commands given below :

```bash

iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
  ./a.out
  gtkwave tb_ternary_operator_mux.vcd

```
the **results** of the gtk wave are shown below :

![terenary_op_mux_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/ff66bdfd-605d-4729-9c75-e339cbbf58fb)

 Let us Consider an another example where the Synthesis and simulation mismatch happens :

```bash

module bad_mux (input i0 , input i1 , input sel , output reg y);
always @ (sel)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule

```
the simulation output for the above example is given by :

![bad_mux_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/a1378187-3cfd-4639-81b1-cced9a65b859)

the simulation of the above example after synthesis and net list generation :

![bad_mux_net](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/1fd9f0e6-f57b-43f3-86c0-d186e31bc394)


Under this, we see a clear mismatch between the simulation and synthesis designs. The RTL file and netlist files aren't the same logic implemention. This happened due to the sensitivity listing under the RTL file.


 
</details>

<details>
	
<summary><strong>Lab on Synthesis Simulation mismatch and B)locking Statments </strong></summary>

Consider an **example**

```bash
module blocking_caveat (input a , input b , input  c, output reg d); 
reg x;
always @ (*)
begin
	d = x & c;
	x = a | b;
end
endmodule

```
The **RTL simulation** of the above code is given beloow :

![blocking_caveat_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/c694887a-b710-435d-bff7-6b56c1ff5886)

The **Synthesised schematic** is shown below :

![blocking_caveat_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/9ec26e10-6153-4ea4-a5a0-577050127ad9)

The Simulation of the **generated netlist** is shown below :

![blocking caveat_net](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/eb49979f-1722-4ab0-ab18-75ede7c174e4)

 Here in the above simulations we can clearly see that booth simulations are different . in this case we can use the un Blocking statments to write the code and get our expected results.
 
</details>

## Day 5 - if,case,for loop and for Generate

<details>

<summary><strong>If and Case Constructs</strong></summary>

### If Statment

**Description** 

The if statement controls conditional execution of other sequential statements. It contains at least one Boolean condition (specified after the if keyword). The remaining conditions are specified with the elsif clause. The else clause is treated as elsif true then. Conditions are evaluated one by one until any of them turns to be true or there are no more conditions to be checked for. When a condition is true then the sequence of statements specified after the then clause is executed. If no condition is met then the control is passed to the next statement after the if statement. 

**Syntax** for If Statment :

 ```bash

if(<condition_1>) begin
  ...
end
else if(<condition>) begin
  ...
end 
else if(<condition>) begin
  ...
end
else begin
  ...
end


Syntax: if and else condition
if(<condition>) begin
  ...
end
else begin
  ...
end

```

    It can be said that, when the condition 1 is valid, statement 1 is of the highest priority, and the rest of the condtions aren't checked for.
    Similarly, we check for which condtion falls true. In case none do, the else block statements takes highest priority.
    The if-else statements can be designed using muxs as shown in the below figure

![if_with _mux](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/8273c5cf-31df-4a6f-928d-fb4bfb54741d)

### Cautions while using if-else

 - In case we miss the else block, it can cause an inferred latch.
 - It is a latch that wasn't intended in the design.
 - the formation of a latch with mux is shown below 

![Pasted image](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/ea2c65ae-fee2-4e21-a45e-208528245fcc)

### Case 

**Description**

The case statement starts with a case keyword followed by the case expression (in parenthesis) and case items or default statement. It ends with the endcasekeyword. The default statement is optional and should be used only once. A case item contains a list of one or more case item expressions, separated by comma, and the case item statement. The case item expression and the case item statement should be separated by a colon.

During the evaluation of the case statement, all case item expressions are evaluated and compared in the order in which they are given. If the first case item expression matches the case expression, then the statement which is associated with that expression is executed and the execution of the case statement is terminated. If comparison fails, then the next case item expression is evaluated and compared with the case expression. If all comparisons fail and the default section is given, then its statements are executed. Otherwise none of the case items will be executed.

Both case expression and case item expressions should have the same bit length. None of the expressions are required to be a constant expression. 

Syntax for the Case Statment is given Below :

```bash

case (expression)

  expression : statement ;

  expression : statement ;

default : statement ;

endcase

```
### Cautions while using case

 - In case we miss the default block, it can cause an inferred latch.
 - Always complete all the expressions of the case.
 - dont write two expressions which simultaneously takes same values while executing case statment


</details>


<details>

<summary><strong>Hands on "Incomplete if case"</strong></summary>

Consider an **Example_1**

```bash

module incomp_if (input i0 , input i1 , input i2 , output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
end
endmodule

```
In the above example according to the logic the output should stay or latched when **I0** is **1'b0** let us see the simulation of the RTL code :

![incomp_if_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/376f69ad-424a-4e8f-93da-88706889a5aa)

The **Schematic** after synthesis is shown below :

![incomp_if_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/378883c8-54fa-4310-8adb-93d822ef03f9)


**Example_2**

```bash

module incomp_if2 (input i0 , input i1 , input i2 , input i3, output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
	else if (i2)
		y <= i3;

end
endmodule

```
In the above example according to the logic the output should stay or latched when **I2** is **1'b0** let us see the simulation of the RTL code :

![incomp_if2_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/15235dc9-7ab1-44aa-9769-322d2b48ad6b)

here when the **I2** is **0** a latch is inferred to fix the output at that level let us see the **Schematic** after the synthesis is done is shown below :

![incomp_if2_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/50dcb5a3-dd3a-49a3-92de-2dd76c160ec7)

</details>
 
<details>
	
<summary><strong>Hands on "overlapping case"</strong></summary>

consider an **Example_1** shown below

```bash

module comp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
		default : y = i2;
	endcase
end
endmodule

```

The RTL Simulation generated is :

![comp_case_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/883a4bd4-2323-4d9e-8198-0070a3c47d5f)

The Synthesised Design is :

![comp_case_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/cd969db6-555e-4916-abbb-ec6c615de7cd)

**Example_2** :

```bash

module bad_case (input i1 , input i1, input i2, input i3 , input [1:0] sel, output reg y);
always @(*)
begin
	case(sel)
		2'b00: y = i0;
		2'b01: y = i1;
		2'b10: y = i2;
		2'b1?: y = i3;
		//2'b11: y = i3;
	endcase
end

endmodule

```

The RTL Simulation generated is :

![bad_case_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/e64b7c5b-9f37-438e-9e61-65231c1d2172)-4aed-4640-8e04-66cee0a243f9)

The Synthesised Design is :

![bad_case_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/4cb7ff2b-74fd-4145-bbdd-6ba044d6fd65)

**Example_3** :

```bash

module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel, output reg y , output reg x);
always @ (*)
begin
	case(sel)
		2'b00 : begin
			y = i0;
			x = i2;
			end
		2'b01 : y = i1;
		default : begin
		           x = i1;
			   y = i2;
			  end
	endcase
end
endmodule

```

The Synthesised Design is :

![partial_case_assign_sche](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/635174b9-5876-41d2-86a0-894001defa30)

**Example_4** :

```bash

module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
	endcase
end
endmodule

```

The RTL Simulation generated is :

![incomp_case_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/033fb3b2-5190-4818-bf7e-4de3bc6cb91b)

The Synthesised Design is :

![incomp_case_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/3b530bba-cd05-48db-8790-e6d1a9d985d1)

</details>

<details>

<summary><strong>For loop and For generate</strong></summary>

 There are two methods of looping in verilog :

- for loop
- generate followed by for loop

**For loop**

The for loop iterates till the mentioned condition is satisfied. The execution of for loop depends on :

**Initialization:**  An initial value of the variable is set. It is executed only once.

**Condition:** A condition or expression is evaluated. If it is evaluated to be the true body of for loop (statements inside begin and end) are executed else, the loop terminates.

**Update:** After execution of for loop body, the variable value is updated

**Example**

```bash

input reg [31:0] inp;
integer i;
always @(*)
begin
  for (i=0;i<32;i=i+1)
  begin
    if(i == sel)
      y = inp[i];
  end
end 
```

- Under this example we take a 32 bit input, and we loop in and take the output for y bit wise using for loop. 

  
**Generate for loop**
The generate statement in Verilog is a very useful construct that generates synthesizable code during elaboration time dynamically. The simulator provides an elaborated code of the ‘generate’ block. It provides the below facilities:

- To generate multiple module instances or code repetition.
- Conditionally instantiate a block of code based on the Verilog parameter, however, the parameter is not permitted in the generate statement.
- It basically provides control on variables, functions, tasks, and instantiation declarations. A generate block has been written within generate and endgenerate keywords.

```bash

genvar i;
generate
  for(i=0;i<3;i=i+1)
    begin
      and u1 (.a(a[i]) , .b(b[i]) , .y(y[i]));
    end
endgenerate

```

- In this example, we instantiate *and* gate u1 3 times using generate for loop.

</details>

<details>

<summary><strong>Hands on "for loop" & "for generate"</strong></summary>

Under this section, we go through some implementations, simulation and synthesis for a better understanding.

**Example_1 - MUX**

- In this, we implement a mux using for loop.Advantage of this method over if-case method is that we don't have to write multiple lines. For a 64 input mux, using if-case we need over 64 lines of code, whereas the same can be done under 5-6 lines using for loop.

-  RTL code for mux_generate.v

```bash

module mux_generate (input i0 , input i1, input i2 , input i3 , input [1:0] sel  , output reg y);
wire [3:0] i_int;
assign i_int = {i3,i2,i1,i0};
integer k;
always @ (*)
begin
for(k = 0; k < 4; k=k+1) begin
	if(k == sel)
		y = i_int[k];
end
end
endmodule
```

- Running RTL simulaltion using iverilog and gtkwave.

![mux_generate_rtl_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/0bf15451-560b-42f6-b1d9-aae97e8d44e2)

- Running synthesis using yosys.

![mux_generate_schematic](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/c551b629-8e5d-456a-b7bb-024d80b055ab)

- Running GLS using iverilog and gtkwave and the netlist attained in syhthesis. 

![mux_generate_net_simu](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/b92ff793-943e-4aec-a531-0c950a7aa34e)

- It is observed that both the RTL simulation and GLS have same output waveform. Thus we have the correct design.


**Lab 2 - DEMUX**
- Under this, we follow up with the implementation of demux
- RTL code for demux_generate.v

```bash
module demux_generate (output o0 , output o1, output o2 , output o3, output o4, output o5, output o6 , output o7 , input [2:0] sel  , input i);
reg [7:0]y_int;
assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
integer k;
always @ (*)
begin
y_int = 8'b0;
for(k = 0; k < 8; k++) begin
	if(k == sel)
		y_int[k] = i;
end
end
endmodule


```

- Running RTL simulation using iverilog and GTKwave.

![Screenshot from 2023-08-16 12-19-03](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/34d9d370-cc01-4d5d-a8cf-90558d66d5eb)
  
- Running synthesis using yosys.

![Screenshot from 2023-08-16 12-21-23](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/f0292279-54fd-440f-afb8-81ecd9517cdf)

- Running GLS using iverilog and GTKwave with the netlist file generated during synthesis.

![Screenshot from 2023-08-16 12-23-57](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/9114c776-7097-415c-89af-15e3512f0ee3)

- We see that both the waveforms for GLS and RTL simulation are the same. Thus we have the correct logic implementataion for demux. 

**Lab 3 - Ripple Carry Adder**

- Under this, we look into implementation of an 8 bit ripple carry adder.
- In this we need 8 single bit adders, that is instantiate single bit full adder 8 times. We implement *generate for* for making this into a simple and shorter code.

- RTL file for rca.v
```bash
module rca (input [7:0] num1 , input [7:0] num2 , output [8:0] sum);
wire [7:0] int_sum;
wire [7:0]int_co;

genvar i;
generate
	for (i = 1 ; i < 8; i=i+1) begin
		fa u_fa_1 (.a(num1[i]),.b(num2[i]),.c(int_co[i-1]),.co(int_co[i]),.sum(int_sum[i]));
	end

endgenerate
fa u_fa_0 (.a(num1[0]),.b(num2[0]),.c(1'b0),.co(int_co[0]),.sum(int_sum[0]));


assign sum[7:0] = int_sum;
assign sum[8] = int_co[7];
endmodule

```  

- Running RTL simulation using iverilog and gtkwave.

![Screenshot from 2023-08-16 12-31-55](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/a79e6e6e-8dda-4791-ad1c-f2f508413c13)

- Running synthesis using yosys and generating the hardware and writing netlist file.

![Screenshot from 2023-08-16 12-34-51](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/e211ab8c-8490-4869-b985-0d342d6628d7)

- Running GLS using iverilog and gtkwave with the netlist file.

![Screenshot from 2023-08-16 12-37-15](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/35041a9d-9ec3-4984-8de0-2adb37ce958d)

- We see the same simulation and GLS waveform, thus the ripple carry adder logic is correct and has been correctly synthesizer. The advantage of using generate for is that we have to instantiate once and the code multiple copies, ie multiple instances as defined.

</details>





# References

1. https://github.com/YosysHQ/yosys
2. https://github.com/steveicarus/iverilog
3. https://github.com/gtkwave/gtkwave
4. https://github.com/The-OpenROAD-Project/OpenSTA
5. https://github.com/ngspice/ngspice
6. https://github.com/RTimothyEdwards/magic
7. https://github.com/The-OpenROAD-Project/OpenLane
8. https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop
9. https://miro.com/
