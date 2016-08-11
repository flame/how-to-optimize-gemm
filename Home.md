From http://wiki.cs.utexas.edu/rvdg/HowToOptimizeGemm

Copyright by Prof. Robert van de Geijn (rvdg@cs.utexas.edu).

Adapted to Github Markdown Wiki by Jianyu Huang (jianyu@cs.utexas.edu).

# The GotoBLAS/BLIS Approach to Optimizing Matrix-Matrix Multiplication - Step-by-Step

This page leads one, step by step, through the optimization of 
matrix-matrix multiplication.  For now, it is assumed that the 
reader has a Linux account on an Intel processor based computer.  We will use
the gcc compiler as part of the exercise.

Please send comments to rvdg@cs.utexas.edu.

# NOTICE ON ACADEMIC HONESTY

If you use these materials for a class project, you MUST disclose where you found this information.  You will risk being accused of academic dishonesty otherwise...

# References

This work is based on two publications.  You will want to read these when you are done with this exercise.  If you use information on this page in other research, please reference these papers.

 * Anatomy of high-performance matrix multiplication.
   Kazushige Goto, Robert A. van de Geijn.
   ACM Transactions on Mathematical Software (TOMS), 2008.

     (Available without charge at the following site: http://www.cs.utexas.edu/users/flame/FLAMEPublications.html)

 * BLIS: A Framework for Rapidly Instantiating BLAS Functionality.
   Field G. Van Zee, Robert A. van de Geijn.
   ACM Transactions on Mathematical Software (TOMS), 2015.

     (Available without charge at the following site: http://www.cs.utexas.edu/users/flame/FLAMEPublications.html)

For more advanced exercises with recent architectures (Intel Sandy/Ivy Bridges, Haswell, etc.), you may want to try BLISlab.

 * BLISlab: A Sandbox for Optimizing GEMM

     (Available at: https://github.com/flame/blislab)
   

# Set Up

This wiki page assumes that you have access to an Intel-based processor, the gnu-cc compiler, and [octave](https://www.gnu.org/software/octave/) (an Open Source version of MATLAB that is part of a typical Linux or Unix install).

To be able to follow along with the below examples, you will want to download some routines, as described on the 
[Set Up](./SetUp)
page.

Make sure that the [`makefile`](../blob/master/src/HowToOptimizeGemm/makefile) starts with the following lines:
```makefile
OLD  := MMult0
NEW  := MMult0
```
This indicates that the performance of
the version of matrix-matrix multiplication in 
[`MMult0.c`](../blob/master/src/HowToOptimizeGemm/MMult0.c) is measured (by virtue of the statement `OLD  :=0`).  

Next, to make sure that when plotting the graphs are properly scaled, 
set certain parameters in the file [`proc_parameters.m`](../blob/master/src/HowToOptimizeGemm/proc_parameters.m).  See the 
comments in that file.  (Setting these parameters will ensure
that when plotting the y-axis ranges from 0 to the peak performance
of the architecture.)

Picking the right clock speed is a bit tricky, given that modern architectures have something called 'turbo boost' which changes the clock speed.  For example, the Intel i5 core in my laptop has a clock speed of 1.7 GHz, but a turbo boost rate of 2.6 GHz.  I chose to indicate in [`proc_parameters.m`](../blob/master/src/HowToOptimizeGemm/proc_parameters.m) that the processor has a clock speed of 2.6 GHz, since otherwise some of the results would show that the implementation attains greater than the peak speed of the processor...

Execute
 * `make run`
 This will compile, link, and execute the test driver, linking to the implementation in [`MMult0.c`](../blob/master/src/HowToOptimizeGemm/MMult0.c).  The performance data is saved in file `output0.m`.
 * `more output0.m`
 This will display the contents of the output file [`output_MMult0.m`](../blob/master/src/HowToOptimizeGemm/output_MMult0.m).  It should look something like
```matlab
version = 'MMult0';
MY_MMult = [
40 1.163636e+00 0.000000e+00 
80 8.827586e-01 0.000000e+00 
120 1.289071e+00 0.000000e+00 
160 1.200469e+00 0.000000e+00 
200 1.195100e+00 0.000000e+00 
240 1.211038e+00 0.000000e+00 
 [ lines deleted ]
720 2.096185e-01 0.000000e+00 
760 2.116985e-01 0.000000e+00 
800 2.115609e-01 0.000000e+00 
];
```
 The first column equals the problem size.  The second column the performance (in Gflops) when a matrix-matrix multiply with the indicated problem size `m=n=k` is executed.  The last column reports the maximum absolute difference encountered between the implementation in [`REF_MMult.c`](../blob/master/src/HowToOptimizeGemm/REF_MMult.c) and [`MMult0.c`](../blob/master/src/HowToOptimizeGemm/MMult0.c).  It should be close to 0.00000e+00 although as different optimizations are added the difference may not be perfectly zero.
 * `octave`
 This will start up octave.  Then, in octave, 
```matlab
octave:1> PlotAll        % this will create the plot
```
 I usually start up a separate xterm session, in which I keep octave running, so that every time I want to make a new graph, I can just execute 'PlotAll' in that session.

The performance graph (on my 1.7GHz Intel Core i5 MacBook Air) looks something like

![](../raw/master/figures/compare_MMult0_vs_MMult0.png) 

Notice that the two curves are right on top of each other because data for the same implementation are being compared.  From the fact that the top of the graph represents peak performance, it is obvious that this simple implementation achieves only a fraction of the ideal performance.

A question, of course is, is this the best we can do?  We are going to walk through a sequence of optimizations, culminating in performance marked by "NEW" in the following graph:

![](../raw/master/figures/compare_MMult0_MMult-4x4-15.png) 

# Step-by-step optimizations

We will now lead the visitor through a series of optimizations.  In some cases, a new implementation (optimization) merely is a small step in the right direction.  We change the code a little at a time in order to be able to make sure it remains correct.

# Computing four elements of C at a time
 
## Hiding computation in a subroutine

 * We first rewrite the basic implementation to hide the inner loop in a subroutine, `AddDot`:

 * [Optimization 1](./Optimization1)

 * [Optimization 2](./Optimization2)

This does not yield better performance:

![](../raw/master/figures/compare_MMult0_MMult2.png) 

It does set us up for the next step.

## Computing four elements at a time

 * We compute C four elements at a time in a subroutine, `AddDot1x4`, which performs four inner products at a time:

 * [Optimization (1x4) 3](./Optimization_1x4_3)

 * Now we inline the four separate inner products and fuse the loops into one, thereby computing the four inner products simultaneously in one loop:

 * [Optimization (1x4) 4](./Optimization_1x4_4)

 * [Optimization (1x4) 5](./Optimization_1x4_5)

At this point, we are starting to see some performance improvements:

![](../raw/master/figures/compare_MMult0_MMult-1x4-5.png) 

## Further optimizing

 * We accumulate the elements of C in registers and use a register for elements of A

 * [Optimization (1x4) 6](./Optimization_1x4_6)

 * We use pointers to address elements in B

 * [Optimization (1x4) 7](./Optimization_1x4_7)

 * We unroll the loop by four  (a relatively arbitrary choice of unrolling factor)

 * [Optimization (1x4) 8](./Optimization_1x4_8)

 * We use indirect addressing to reduce the number of times the pointers need to be updated

 * [Optimization (1x4) 9](./Optimization_1x4_9)

There is considerable improvement for problem sizes that fit (at least partially) in the L2 cache.  Still, there is a lot of room for improvement.

![](../raw/master/figures/compare_MMult0_MMult-1x4-9.png) 

# Computing a 4 x 4 block of C at a time

We now compute a 4 x 4 block of C at a time in order to use vector instructions and vector registers effectively.  The idea is as follows:  There are special instructions as part of the SSE3 instruction set that allow one to perform two 'multiply accumulate' operations (two multiplies and two adds) per clock cycle for a total of four floating point operations per clock cycle.  To use these, one has to place data in 'vector registers'.  There are sixteen of these, each of which can hold two double precision numbers.  So, we can keep 32 double precision numbers in registers.  We will use sixteen of these to hold elements of C, a 4 x 4 block.

## Repeating the same optimizations

 * We compute C four elements at a time in a subroutine, `AddDot4x4`, which performs sixteen inner products at a time:

 * [Optimization (4x4) 3](./Optimization_4x4_3)

 * Now we inline the sixteen separate inner products and fuse the loops into one, thereby computing the sixteen inner products simultaneously in one loop:

 * [Optimization (4x4) 4](./Optimization_4x4_4)

 * [Optimization (4x4) 5](./Optimization_4x4_5)

At this point, we are again starting to see some performance improvements:

![](../raw/master/figures/compare_MMult0_MMult-4x4-5.png) 
![](../raw/master/figures/compare_MMult-1x4-5_MMult-4x4-5.png) 

 * We accumulate the elements of C in registers and use a register for elements of A

 * [Optimization (4x4) 6](./Optimization_4x4_6)

 * We use pointers to address elements in B

 * [Optimization (4x4) 7](./Optimization_4x4_7)

## Further optimizing

We now start optimizing differently as we did for the 1x4 case.

 * We store a row of k x 4 matrix B in registers

  * [Optimization (4x4) 8](./Optimization_4x4_8)

   Notice that we now use MANY more regular registers than physically available... 

 * We rearrange the computation so that two rows of 4x4 block of C are computed at a time.

  * * [Optimization (4x4) 9](./Optimization_4x4_9)

 * We use vector registers and vector operations.

  * [Optimization (4x4) 10](./Optimization_4x4_10)

We notice a considerable performance boost:

![](../raw/master/figures/compare_MMult0_MMult-4x4-10.png) 
![](../raw/master/figures/compare_MMult-1x4-9_MMult-4x4-10.png) 

Still, there is a lot of room for improvement.

## Blocking to maintain performance

 * In order to maintain the performance attained for smaller problem sizes, we block matrix C (and A and B correspondingly):

  * [Optimization (4x4) 11](./Optimization_4x4_11)

Now, performance is maintained:

![](../raw/master/figures/compare_MMult0_MMult-4x4-11.png) 
![](../raw/master/figures/compare_MMult-4x4-10_MMult-4x4-11.png) 

## Packing into contiguous memory

 * First, we pack the block of A so that we march through it contiguously.

  * [Optimization (4x4) 12](./Optimization_4x4_12)

  * [Optimization (4x4) 13](./Optimization_4x4_13)
  
    This yields a surprisingly large performance boost: 

![](../raw/master/figures/compare_MMult0_MMult-4x4-13.png) 
![](../raw/master/figures/compare_MMult-4x4-11_MMult-4x4-13.png)

 * Finally, we pack the block of B so that we march through it contiguously.

  * [Optimization (4x4) 14](./Optimization_4x4_14)

  * [Optimization (4x4) 15](./Optimization_4x4_15)
  
We now attain 90% of the turbo boost peak of the processor!
 
![](../raw/master/figures/compare_MMult0_MMult-4x4-15.png) 
![](../raw/master/figures/compare_MMult-4x4-13_MMult-4x4-15.png)

