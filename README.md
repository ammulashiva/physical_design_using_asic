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

![Iverilog](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/4106244b-db39-42e5-bc5d-e43dfe40a297)

# gtkwave
# Steps to install gtkwave
sudo apt update
sudo apt install gtkwave

![gtkwave](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/63bef04c-b53d-4175-b326-7212f403652c)

# OpenSTA
https://github.com/The-OpenROAD-Project/OpenSTA

![OpenSTA](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/3ce1cccc-a154-4071-a9c8-682bc4c57fb2)

# ngspice
After downloading the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory, unpack it using:
$ tar -zxvf ngspice-37.tar.gz
$ cd ngspice-37
$ mkdir release
$ cd release
$ ../configure  --with-x --with-readline=yes --disable-debug
$ make
$ sudo make install

![ngspice](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/64efc675-08ed-4c9e-a4da-c6554baac603)

# magic
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

![magic1](https://github.com/ammulashiva/physical_design_using_asic/assets/140998900/2ca1576d-839c-4e49-9574-a5e3e05c6083)





