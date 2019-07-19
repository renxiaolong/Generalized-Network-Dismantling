# Generalized Network Dismantling

These codes implement the GND and GNDR network dismantling algorithm proposed in 

Xiao-Long Ren, Niels Gleinig, Dirk Helbing, Nino Antulov-Fantulin, 2019. Generalized network dismantling. *Proceedings of the National Academy of Sciences*, Apr 2019, 116 (14) 6554-6559; DOI: [10.1073/pnas.1806108116](https://doi.org/10.1073/pnas.1806108116)
[arXiv:1801.01357](https://arxiv.org/abs/1801.01357). 



    @article{ren_network_2019,
	author = {Ren, Xiao-Long and Gleinig, Niels and Helbing, Dirk and Antulov-Fantulin, Nino},
	title = {Generalized network dismantling},
	volume = {116},
	number = {14},
	pages = {6554--6559},
	year = {2019},
	doi = {10.1073/pnas.1806108116},
	publisher = {National Academy of Sciences},
	abstract = {The proper functioning of many sociotechnical systems depends on their level of connectivity. By removing or deactivating a specific set of nodes, a network structure can be dismantled into isolated subcomponents, thereby disrupting the malfunctioning of a system or containing the spread of misinformation or an epidemic. We propose a generalized network-dismantling framework, which can take realistic removal costs into account such as the node price, the protection level, or removal energy. We discuss applications of cost-efficient dismantling strategies to real-world problems such as containing an epidemic or dismantling criminal or corruption networks.Finding an optimal subset of nodes in a network that is able to efficiently disrupt the functioning of a corrupt or criminal organization or contain an epidemic or the spread of misinformation is a highly relevant problem of network science. In this paper, we address the generalized network-dismantling problem, which aims at finding a set of nodes whose removal from the network results in the fragmentation of the network into subcritical network components at minimal overall cost. Compared with previous formulations, we allow the costs of node removals to take arbitrary nonnegative real values, which may depend on topological properties such as node centrality or on nontopological features such as the price or protection level of a node. Interestingly, we show that nonunit costs imply a significantly different dismantling strategy. To solve this optimization problem, we propose a method which is based on the spectral properties of a node-weighted Laplacian operator and combine it with a fine-tuning mechanism related to the weighted vertex cover problem. The proposed method is applicable to large-scale networks with millions of nodes. It outperforms current state-of-the-art methods and opens more directions for understanding the vulnerability and robustness of complex systems.},
	issn = {0027-8424},
	URL = {https://www.pnas.org/content/116/14/6554},
	eprint = {https://www.pnas.org/content/116/14/6554.full.pdf},
	journal = {Proceedings of the National Academy of Sciences}
    }


Please note that **all the results in the paper were produced with the Visual Studio 2017** (C++ Compiler version: VC++ 2017 version 15.5 v14.12 toolset, C++ standard: C++14/17). Therefore, in order to have reproducible results across different platform, one just needs to specify that "std::default_random_engine" should be "std::mt19937" in line 176 and line 208 of GND.cpp (This has been done in the latest version of our code. So please run the code directly). 

In the meantime we also provide the method that can run in the GNU environment. Please see the details below.


### Compilation

Pre-requirements: GNU C++ compiler, Boost library

Adjust Makefile as needed and type the following command to the terminal:

    make

#### Pre-requirements installation instructions:
Install GNU C++ compiler:
https://gcc.gnu.org/

Install **boost** library:

For *Windows*, see: 
https://www.boost.org/doc/libs/1_62_0/more/getting_started/windows.html

For *Unix/MAC-OS*, see:

https://www.boost.org/doc/libs/1_62_0/more/getting_started/unix-variants.html, 

https://blog.koalatea.io/2018/01/03/getting-started-with-boost-on-mac-osx/

### Running
Before running the program, you need to set the parameters of the input network in 
<code>GND.cpp</code> (line 37-41) and <code>reinsertion.cpp</code> (line 70-74), respectively. 

Here is an example of a criminal network with 754 nodes obtained by the projection of a bipartite network of
persons and crimes. More information about the network is provided here: http://konect.uni-koblenz.de/networks/moreno_crime

To run the GND algorithm, type the following command to terminal: 

    ./GND

The output of the upper program is a list of nodes that should be removed. Based on this result, type the following command to get the list of the removed nodes by GNDR:

    # reintroduce removed nodes as long as the component is of size <= 7
    ./reinsertion -t 7

### Notes on normalization of the dismantling cost

In general case, each node "i" has associated weight "w_i"  and the dismantling cost is always normalized to the maximum possible cost.

Here are a few special cases:
1. If the weight comes from the non-topological source (e.g. in the airport network, fig 5. of the main manuscript), the dismantling cost of removing a set of nodes is just the sum of node weights. 

The normalization is done with the sum of the weights of all the nodes in a network. 

2. In a unit-cost scenario, the normalization is done with the total number of nodes in a network.

3. In a degree-based cost scenario, in the paper, we wrote that the removal cost is proportional to the degree. But one should be careful when the algorithm is recursively applied, the degrees of nodes are changing. 

   Let us explain this on toy example Fig. S2 from [Supplementary Information](https://www.pnas.org/content/116/14/6554) of our paper. 
   
   ![Fig. S2](Datasets_SI/pic/FigS2.png?raw=true "Title")

   The degrees of nodes 81, 82 and 83 are deg(81) = 10, deg(82) = 3 and deg(83) = 3. If we first remove node 83, the associated cost is 3. But, after this step, the degree of node 81 has changed to deg(81)=9.  If in the second step, we remove node 81, the associated cost is 9, which implies that the dismantling cost of removing 83 and 81 is 3+9 = 12. Note, that this is unnormalized cost. 

   We have to normalize it to the maximum possible degree-based cost, which is the total number of links, which is the sum of all degrees divided by 2. 


