# Docker
This repository contains Dockerfiles for the different tools used in the Chisel-UVM project. This should help reduce the dependencies for different systems as a docker image can be created when needed.


## Repository structure
This repository contains a directory for each Dockerfile. The idea being that when running a Docker image, you can mount said directory for access to files.

# Windows 10
Install Docker Desktop for Windows: https://hub.docker.com/editions/community/docker-ce-desktop-windows/

## Development environment
Docker images can be mounted in Visual Studio Code. This is done by installing the "Remote - Containers" extension. From Visual Studio Code press *ctrl + shift + p* and choose *Remote-Containers: Open Folder in Container...* and choose *From Dockerfile..*. Then choose the Chisel folder within this repository.

After some time, it will have built the docker image and you can now work from this folder. Open a terminal from the bar in the top. Now, run *sbt test* in the terminal and a test should run sucesfully.

## VHDL2Verilog
Same thing as above. Run the following in the terminal to test the system:
```
yosys -m ghdl -p 'ghdl --std=08 src/accualu.vhd -e accualu; write_verilog accualu_synth.v'
```

This should generate a file called *accualu_synth.v*.

# Running from a terminal
To run from a terminal, such as PowerShell, the image first needs to be built. This is done using the following command from the chisel folder:

```
docker build . --rm -t chisel
```

And for the VHDL2Verilog:

```
docker build . --rm -t vhdl2verilog
```


And then to run an image:
```
docker run -it -v <PATH\TO\CHISEL_FOLDER>:/usr/home chisel
```

And from that, ssh into /usr/home.

Same principle goes for VHDL2Verilog:
```
docker run -it -v <PATH\TO\VHDL2VERILOG_FOLDER>:/usr/home vhdl2verilog
```
and ssh into /usr/home


# Docker notes
Every time a Docker instance is opened, it starts from image scratch. This means that the only things that are saved is the files located in the folder that was chosen (mounted as a volume) when starting the docker.

# GUI
TBA

# Resources
Docker sets a quite limited amount of resources as default. In Docker hub click *Resources -> Advanced* from which you can set number of CPUs and amount of RAM. You can freely set number of CPUs but Memory should be a reasonable amount. Memory is pre-allocated when starting a Docker.