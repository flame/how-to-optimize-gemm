 * Download attachment:HowToOptimizeGemm.tar.gz  (make sure the file is stored as OptimizeGemm.tar.gz)
 * Uncompress by executing `gunzip HowToOptimizeGemm.tar.gz`
 * Expand the tar file by executing `tar HowToOptimizeGemm.tar`
 * Change into the directory that is created by executing `cd HowToOptimizeGemm`

## Files

In the directory `HowToOptimizeGemm` you will find the following files
that you will use to systematically optimize the matrix-matrix multiplication
operation:

* `makefile`
The makefile that describes how to compile, link, and execute the driver/implementations. When you type `make', this file is consulted and commands in it are executed.  Note: there are "tab" characters in the makefile. These are important...
* `Test driver`
  * `parameters.h`
File that holds parameters that control what data is collected
  * `test_MMult.c` Driver routine that tests and times the different implementations. This routine executes a reference implementation and the current optimization to be timed.  Parameters for this routine are initialized in `parameters.h`.  In particular, in that file it is indicated how many times to repeat each experiment (problem size) and how each of the three dimensions `m`, `n`, and `k` are tied to the problem size being timed.
* `Matrix multiplication implementations`
  * `REF_MMult.c` Reference implementation used to check correctness 
  * `MMult0.c` Version 0: simplest implementation
  * `MMult1.c` Optimization 1

* `Utility routines`

  * `compare_matrices.c` Compares the contents of two matrices and returns the maximum absolute difference

  * `copy_matrix.c` Copies one matrix to another

  * `dclock.c` Returns elapsed time in seconds

  * `random_matrix.c` Generates a random matrix

  * `print_matrix.c` Prints the contents of a matrix

*`Plotting the results`

  * `PlotAll.m` Plots graphs corresponding to the data in files `output_old.m` and `output_new.m`

  * `proc_parameters.m` File in which parameters about the architecture are given









These last routines allow one to use octave to plot the performance of two 
different implementations.

## Which Compiler?

In this exercise, we use the gcc (Gnu C) compiler with optimization level -O2.  (See the `makefile`.)  
This is neither the best compiler nor the best optimization level.  The reason is that with this compiler and
level of optimization, we have a certain level of control:

 * Had we used the intel compiler, the "simple loops" in MMult0.c would probably have yielded quite good performance:  This compiler is very good at optimizing a triple loop.  Try it!!!

 * Had we used -O3 (optimization level 3), the gnu compiler would have more aggressively optimized, making the step-by-step optimizations we demonstrate much less predictable.



