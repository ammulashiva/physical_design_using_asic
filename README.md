# physical_design_using_asic
# steps to install yosys
Yosys
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

![yosys](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/76ecfa86-4e5b-4bba-9c75-d0e98fed2b19)

# Iverilog
# steps to install Iverilog
sudo apt-get install iverilog


