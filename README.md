# Generalized Network Dismantling

These codes implement the GND and GNDR network dismantling algorithm proposed in 

Xiao-Long Ren, Niels Gleinig, Dirk Helbing, Nino Antulov-Fantulin, 2019. Generalized network dismantling. [arXiv:1801.01357](https://arxiv.org/abs/1801.01357). 



## Compilation

Pre-requirements: GNU C++ compiler, Boost library

Adjust Makefile as needed and type the following command to the terminal:

    make

### Pre-requirements installation instructions:
Install GNU C++ compiler:
https://gcc.gnu.org/

Install **boost** library:

For *Windows*, see: 
https://www.boost.org/doc/libs/1_62_0/more/getting_started/windows.html

For *Unix/MAC-OS*, see:

https://www.boost.org/doc/libs/1_62_0/more/getting_started/unix-variants.html, 

https://blog.koalatea.io/2018/01/03/getting-started-with-boost-on-mac-osx/

## Running
Before running the program, you need to set the parameters of the input network in 
<code>GND.cpp</code> (line 37-41) and <code>reinsertion.cpp</code> (line 70-74), respectively. 

Here is an example of a criminal network with 754 nodes obtained by the projection of a bipartite network of
persons and crimes. More information about the network is provided here: http://konect.uni-koblenz.de/networks/moreno_crime

To run the GND algorithm, type the following command to terminal: 

    ./GND

The output of the upper program is a list of nodes that should be removed. Based on this result, type the following command to get the list of the removed nodes by GNDR:

    # reintroduce removed nodes as long as the component is of size <= 7
    ./reinsertion -t 7



