[//]: # (#opencv cuda)
## CUDA Best Practices in OpenCV
1. Types of gpuMat that are efficient for a GPU to compute
- Channels: 1 or 4
- Depths:   char or float, no double
  - For memory efficiency, a 3 channel image is usually spilt up to 3 images and have functions worked on each of them
  - If the operation doesn't consider neighbors, reshape it into single channel image.
2. Never use arithmetic operators in a row
- Memory allocation in GPU is extreamly expensive. Do operations in place if possible.
   - Bad example:
```cpp
b.t1 = 2 * b.mu1_mu2 + C1; //Hidden data transfer happens
```
   - Good example:
```cpp
gpu::multiply(b.mu1_mu2, 2, b.t1); //b.t1 = 2 * b.mu1_mu2 + C1;
gpu::add(b.t1, C1, b.t1);
```

## CUDA Fudametals 
1. [Basic Operations](https://www.youtube.com/watch?v=LjWlZHqUG8A&index=68&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_)
- Map: one to one
- Scatter: one to multiple
- Transpose: one to one, reorder data elements in memory
- Gather: multiple to one
- Stencil: multiple to one and writes every element in the output
- Reduce: all to one
- Sort: all to all
- Scan: all to all, integral image is call *inclusive sum scan*
- Histogram: 
2. [Thread Blocks and SMs](https://www.youtube.com/watch?v=mLOfri_YVvo&index=73&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_)
- A thread block contains many threads
- An SM may run more than one block
- A block can not run on more than one SM
- All the threads in a thread block may cooperate to solve a subproblem
- Different blocks don't attempt to cooperate with each other.
3. [Memory Model](https://www.youtube.com/watch?v=HQejUtJtBlg&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_&index=82)
- All threads in the same block can access the same variable in that block's shared memory
- Threads from different blocks can access the same variable in the global memory
- Threads from the same/different blocks have their own copy/piece of local variables in local memory.
- [Memory access speed](https://www.youtube.com/watch?v=v-gSOY9-RgI&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_&index=92): local > shared >> gloabl >> host
4. Syncronization Model
- [Barrier](https://www.youtube.com/watch?v=6r5FJLqcdqY&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_&index=85  )
5. Global Memory Access
- [coalescence](https://www.youtube.com/watch?v=mLxZyWOI340&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_&index=97): If adjacent threads read or write to very close memory, that's of good coalescence
- NOTE: **Adjacent refers only to x direction**
- Strided, when strides are very big => random access => bad coalescence
6. How to excecute a kernel
```c
kernel<<<BLOCK_DIMS, TREAD_DIMS, SIZE_OF_SHARED_MEM>>>(args...)
// Both BLOCK_DIMS and TREAD_DIMS can be set up to 3 dimensions
// SIZE_OF_SHARED_MEM set how many bytes of shared memory to allocate for each block
```
7. [Choose work efficient or step efficient algorithm](https://www.youtube.com/watch?v=PMeGxYRaJDU&index=148&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_)
- work > processors => go for work efficient one
- work < processors => go for step efficient one
8. Applications of basic operations
- [Compact](https://www.youtube.com/watch?v=GyYfg3ywONQ&index=170&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_): using *scan*
- [Sparse Matrix Multiplications](https://www.youtube.com/watch?v=bOmAllndo-4&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_&index=187): using *scan*
9. Principals of efficient GPU programming
- Decrease time spent on memory operations
- Coalesce global memory access
- Avoid thread divergence
10. Performance Benchmark: [Bandwidth Measurement](https://www.youtube.com/watch?v=mT_WVr8FhT4&index=239&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_)
- 40-60% : Okay
- 60-75% : Good
- \>75   : Excellent
11. [How to raise Bandwidth Rate](https://www.youtube.com/watch?v=FbKWHHIHpWM&index=242&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_)
- Bandwidth rate suffers from ramdom memory accessing

## CUDA Terminologies
1. Thread blocks: software term that define by user
2. SM: Stream Multiprocessors, hardware term
3. [Work Complexity and Step Complexity](https://www.youtube.com/watch?v=V8TTrUdfpIY&list=PLGvfHSgImk4aweyWlhBXNF6XISY3um82_&index=114)