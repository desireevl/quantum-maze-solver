There are two components to the problem: 
1. Generating the maze
2. Solving the maze

There are also a few potential problems that could be worked on:
- Finding total unique paths (for large mazes this would be more ideal for classical implementations as quantum implementations would be limited by qubits) 
- Finding the shortest path
- Finding a path in the shortest time

I could try implement a classical and quantum solution to compare their speed/accuracy etc. I think there are many opportunities in this and we would need to really define the scope of the problem.
I believe there are two ways to go about the quantum solution: implement a classical solution on a QC or utilise quantum properties. I believe the second option to be more interesting.

1. Generating the maze
Can be done first simply by representing it as a binary maze. The generator needs constraints so that there is at least one possible path. At the end the binary maze can somewhat easily be converted into a nice visualisation. 

There are many kinds of algorithms to generate mazes such as braid (no dead ends) and recursive backtracker (carves the passages instead of inputting the walls). We would need to choose which to used based on what kind of maze we want (probably something standard like dead ends, one exit and one entry etc). 

There is a package called [Daedalus](http://www.astrolog.org/labyrnth/daedalus.htm) which implements every kind of maze algorithm there is which could potentially be used and for reference there is a repo with [python implementations of classical maze algs](https://github.com/mikepound/mazesolving/).

2. Solving the maze
There are many classical algorithms to solve the maze, some very basic and slow as they try all combinations (depth first search) and some with better optimisation (you could also probably multithread). 

Some classical algs:
- Dijkstra's: creates a tree of hte shortest path by first initialising distances then picking the adjacent node with the smallest distance
- A*: similar to above however is better as it uses a function that gives an estimated cost of the total path
- Depth first: sees which direction it can it does. Once it reaches a dead end it will go back and try other possible directions. This technique goes through every path and is slow

For solving the problem quantum-ly I was thinking of using Grover's alg. I'm still not super familiar with Grover's alg and am still reading.
- A thought I had on the bus would be the approach of assigning two qubits to determine direction. When a Hadamard is applied to both you would get four states which could be assigned to the four directions it could try and repeated until the end is found. To determine if the step is valid or not (1 or 0) I was thinking of including it into an ancilla and modifying using some sort of gate. I wouldn't have an idea on how to save the final path at this time however. 
- Some people I chat to suggested a 4D Grover coin method based on quantum walks. 
- There is also a resource below that suggests for a maze with an N path solution, N qubits will be used + log_2(N) qubits which will be for counting. log_2(N) as this will allow enough bits to create every combo (ie N=10, log_2(N) = 4 and 10 in binary is 1010). For only up and down decisions, it would read the counting qubit to determine position and put the qubit into superposition to travel up and down. It would then change the counting qubit to know to move to the next position. The order of the 1's and 0's in the end would tell you the position. My understanding of this is still incomplete as the writeup lacks detail.

There are some papers and blog posts I have found that I am working to read through below

## Relevant Resources
- [Quantum Algorithm to Solve a Maze: Converting the Maze Problem into a Search Problem](https://arxiv.org/pdf/1312.4116.pdf)
- [Quantum Walk with a Four Dimensional Coin](https://arxiv.org/pdf/1103.0126.pdf)
- [Creating Infinite Worlds with Quantum Computing](https://medium.com/qiskit/creating-infinite-worlds-with-quantum-computing-5e998e6d21c2)
- [Experimental Realization of a Delayed-Choice Quantum Walk](https://www.nature.com/articles/ncomms3471.pdf)
- [Solving a Maze with a Quantum Computer](https://arxiv.org/ftp/quant-ph/papers/0304/0304146.pdf)
- [Quantum Algorithm to Solve a Maze: Converting a Maze Problem into Search Problem](https://www.imsc.res.in/~aqis13/extended/posters/Debabrata_Goswami_Easychair_Paper91.pdf)
- [Finding Paths with Quantum Walks or Quantum Walking Through a Maze](https://journals.aps.org/pra/abstract/10.1103/PhysRevA.96.032323)
- [Qiskit Grover Tutorial](https://github.com/Qiskit/qiskit-tutorials-community/blob/2a5559bbd1b98fee7cf316bfd2fa86e427a4ef5d/algorithms/grover_algorithm.ipynb)
- [Jonathan Hui Grover's Alg](https://medium.com/@jonathan_hui/qc-grovers-algorithm-cd81e61cf248)
- [In depth Grover's alg explanation](http://twistedoakstudios.com/blog/Post2644_grovers-quantum-search-algorithm)
