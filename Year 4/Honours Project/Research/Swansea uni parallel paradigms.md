https://sa2c.swansea.ac.uk/introduction-to-mpi/05-parallel-paradigms/index.html
# Parallel Paradigms
Parallel computing is divided into two camps:
- Data Parallel
	- The same operation is performed on many data at the same time
	- Parallelism is achieved by how many data a single operation can act on
- Message Passing (task parallelism)
	- Each CPU runs an independent program
	- Parallelism is achieved by receiving data which it doesn't have, and sending data which it has
## Data Parallel
one standard method for this is called "OpenMP" (Open MultiProcessing). Consider the following:
```C
#pragma omp parallel for
for (i=0; i<N; i++) {
	a[i] = b[i] + c[i]
}
```
Parallelization is achieved by adding the line `#pragma omp parallel for` which is handled by the processor at compile time. The system architecture has a shared memory view of variables and each CPU can access all of the memory addresses. The compiler "calculates" the address offset for each CPU and lets each one compute on a part of the whole data.

## Message Passing
In message passing, each processor runs its own program and works on its own data. To work on the same problem in parallel, they communicate by sending messages to each other. Using the same example:
```C
for (i=0; i<m; i++) {
	a[i] = b[i] + c[i];
}
```
Other than changing the number of loops from `N` to `m`, the code is exactly the same. Here, `m` is the reduced number of loops each CPU needs to do (if there are `N` CPUs, m is 1 (=`N`/`N`)). But the parallelization is not complete yet. In the message passing paradigm, each CPU is independent from the other CPUs. We must make sure that each CPU has correct data to compute and write out the results in the correct order. This part depends on the computer system. Assume the system is a cluster computer. In a cluster computer, sometimes only one CPU has access to the file system. In this case, this particular CPU reads the whole data and sends the correct data to each CPU (including itself). After the computation, each CPU sends the result to that particular CPU. This CPU then writes out the received data in a file in the correct order. if the cluster computer supports a parallel file system, each CPU reads the correct data from one file, computes and writes out the result to one file in correct order.

In the end, both data parallel and message passing logically achieve the following:
![[Pasted image 20261027100721.png]]
Each rank operates on its own set of data. In some cases, one has to combine the data parallel and message passing methods. For example, there are problems larger than one GPU can handle. Then, data parallelism is used for the portion of the problem contained within one GPU, and the message passing is used to employ several GPUs unless special hardware/software supports multiple GPU usage.
# Algorithm Design
Designing a parallel algorithm that determines which of the two paradigms above one should follow rests on the actual understanding of how the problem can be solved in parallel. This requires some thought and practice. 
To get used to thinking in parallel, we discuss "Embarrassingly Parallel" (EP) problems first and then we consider problems which are not EP.
## Embarrassingly Parallel Problems
Problems which can be parallelized most easily are EP problems, which occur in many Monte Carlo simulation problems, and in many big database search problems. In Monte Carlo simulations, random initial conditions are used in order to sample a real situation. So, a random number is given and the computation follows using this random number. Depending on the random number, some computation may finish quicker and some computation may take longer to finish. And we need to sample a lot (like a billion) to get a rough picture of the real situation. The problem becomes running the same code with a different random number over and over again. In big database searches, one needs to dig through all the data to find wanted data. There may be just one or many data which fit the search criterion. Sometimes, we don't need all the data which satisfies the condition. Sometimes, we do need all of them. To speed up the search, the big database is divided into smaller databases, and each smaller databases are searched independently by many workers.
### Queue Method
Each worker will get tasks from a predefined queue (a random number in a Monte Carlo problem, or smaller databases in a big database search problem). The tasks can be very different and take different amounts of time, but when a worker has completed its tasks, it will pick the next one from the queue. In an MPI code, the queue approach requires the ranks to communicate what they are doing to all the other ranks, resulting in some communication overhead (but negligible compared to overall task time).
### Manager / Worker Method
The manager / worker approach is a more flexible version of the queue method. We hire a manager to distribute tasks to the workers. The manager can run some complicated logic to decide which tasks to give to a worker. The manager can also perform any serial parts of the program like generating random numbers or dividing up the big database. The manager can become one of the workers after finishing managerial work.
In an MPI implementation, the main function will usually contain an `if` statement that determines whether the rank is the manager or a worker. The manager can execute a completely different code from the workers, or the manager can execute the same partial code as the workers once the managerial part of the code is done. It depends on whether the managerial load takes a lot of time to finish or not. Idling is a waste in parallel computing!
Because every worker rank needs to communicate with the manager, the bandwidth of the manager rank can become a bottleneck if administrative work needs a lot of information. This can happen if the manager needs to send smaller databases (divided from one big database) to the worker ranks. This is a waste of resources and is not a suitable solution from an EP problem. Instead, it's better to have a parallel file system so that each worker rank can access the necessary part of the big database independently.
## General Parallel problems (Non-EP Problems)
As we discussed, not all parts of a serial code can be parallelized. So, one needs to identify which part of a serial code is parallelizable. In science and technology, many numerical computations can be defined on a regular structured data (e.g. partial differential equations in a 3D space using a finite difference method). In this case, one needs to consider how to decompose the domain so that many CPUs can work in parallel.
### Domain Decomposition
When the data is structured in a regular way, such as when simulating atoms in a crystal, it makes sense to divide the space into domains. Each rank will handle the simulation within its own domain.
Many algorithms involve multiplying very large matrices. These include finite element methods for computational field theories as well as training and applying neural networks. The most common parallel algorithm for matrix multiplication divides the input matrices into smaller submatrices. If there are four ranks, the matrix is divided into four submatrices.
If the number of ranks is higher, each rank needs data from one row and one column to complete its operation.
### Load Balancing
Even if the data is structured in a regular way and the domain is decomposed such that each CPU can take charge of roughly equal amounts of the sub-domain, the amount of work is different in that domain since more complicated chemistry/physics is happening in that domain. Balancing this type of loads is a difficult problem and requires a careful thought before designing a parallel algorithm.
# Communication Patterns
In MPI parallelization, several communication patterns occur.
## Gather / Scatter
In gather type communication, all ranks send a piece of information to one rank. Gathers are typically used when printing out information or writing to disk. For example, each could  send the result of a measurement to rank 0 and rank 0 could print all of them. This is necessary if only one rank has access to the screen. It also ensures that the information is printed in order. 
Similarly, in a scatter communication, one rank sends a piece of data to all the other ranks. Scatters are useful for communicating parameters to all the ranks doing the computation. The parameter could be read from disk but it could also be produced by a previous computation.
Gather and scatter operations require more communication as the number of ranks increases. The amount of messages sent usually increases logarithmically with the number of ranks. They have efficient implementations in the MPI libraries. 
## Halo Exchange
A common feature of a domain decomposition algorithm is that communications are limited to a small number of other ranks that work on a domain a sort distance away. For example, in a simulation of atomic crystals, updating a single atom usually requires information from a couple of its nearest neighbours.
In such a case each rank only needs a thin slice of data from its neighbouring rank and send the same slice from its own data to the neighbour. The data received from neighbours forms a "halo" around the ranks own data.
## Reduction
![[Pasted image 20261027104817.png]]
A reduction is an operation that reduces a large amount of data, a vector or a matrix, to a single number. The sum example above is a reduction. Since data is needed from all ranks, this tends to be a time consuming operation, similar to a gather operation. Usually each rank first performs the reduction locally, arriving at a single number. They then perform the steps of collecting data from some of the ranks and performing the reduction on that data, until all the data has been collected. The most efficient implementation depends on several technical features of the system. Fortunately many common reductions are implemented in the MPI library and are often optimised for a specific system.
## All-to-All
In other cases, some information needs to be send from every rank to every other rank in the system. This is the most problematic scenario; the large amount of communication required reduces the potential gain from designing a parallel algorithm. Nevertheless the performance gain may be worth the effort if it is necessary to solve the problem quickly.
