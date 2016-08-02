 * Download attachment:HowToOptimizeGemm.tar.gz  (make sure the file is stored as OptimizeGemm.tar.gz)
 * Uncompress by executing "`gunzip HowToOptimizeGemm.tar.gz`"
 * Expand the tar file by executing "`tar HowToOptimizeGemm.tar`"
 * Change into the directory that is created by executing "`cd HowToOptimizeGemm`"

## Files

In the directory `HowToOptimizeGemm` you will find the following files
that you will use to systematically optimize the matrix-matrix multiplication
operation:

 ||<-2> '''makefile''' ||
 ||<30%>  [:HowToOptimizeGemm/Details/makefile:makefile] ||<65%>  The makefile that describes how to compile, link, and execute the driver/implementations. When you type `make', this file is consulted and commands in it are executed.  Note: there are "tab" characters in the makefile.  These are important...  ||
 ||<-2> '''Test driver'''||
 ||<30%>  [:HowToOptimizeGemm/Details/parameters:parameters.h] ||<65%>  File that holds parameters that control what data is collected ||
 ||<30%>  [:HowToOptimizeGemm/Details/test_MMult.c:test_MMult.c] ||<65%>  driver routine that tests and times the different implementations. This routine executes a reference implementation and the current optimization to be timed.  Parameters for this routine are initialized in `parameters.h`.  In particular, in that file it is indicated how many times to repeat each experiment (problem size) and how each of the three dimensions ([[latex($ m $, $ n $, and $ k $)]] are tied to the problem size being timed. ||
 ||<-2> '''Matrix multiplication implementations''' ||
 ||<30%>  [:HowToOptimizeGemm/Details/REF_MMult.c:REF_MMult.c] ||<65%>  Reference implementation used to check correctness ||
 ||<30%>  [:HowToOptimizeGemm/Details/MMult0:MMult0.c] ||<65%>  Version 0: simplest implementation ||
 ||<30%>  [:HowToOptimizeGemm/Details/MMult1:MMult1.c] ||<65%>  Optimization 1 ||
 ||<-2> '''Utility routines''' ||
 ||<30%> [:HowToOptimizeGemm/Details/compare_matrices:compare_matrices.c] ||<65%> Compares the contents of two matrices and returns the maximum absolute difference ||
 ||<30%>  [:HowToOptimizeGemm/Details/copy_matrix:copy_matrix.c] ||<65%> Copies one matrix to another ||
 ||<30%>  [:HowToOptimizeGemm/Details/dclock:dclock.c] ||<65%> Returns elapsed time in seconds ||
 ||<30%>  [:HowToOptimizeGemm/Details/random_matrix:random_matrix.c] ||<65%> Generates a random matrix ||
 ||<30%>  [:HowToOptimizeGemm/Details/print_matrix:print_matrix.c] ||<65%> Prints the contents of a matrix ||
 ||<-2> '''Plotting the results''' ||
 ||<30%>  [:HowToOptimizeGemm/Details/PlotAll:PlotAll.m] ||<65%> Plots graphs corresponding to the data in files `output_old.m` and `output_new.m`  ||
 ||<30%>  [:HowToOptimizeGemm/Details/proc_parameters:proc_parameters.m] ||<65%> File in which parameters about the architecture are given  ||

These last routines allow one to use octave to plot the performance of two 
different implementations.

## Which Compiler?

In this exercise, we use the gcc (Gnu C) compiler with optimization level -O2.  (See the `makefile`.)  
This is neither the best compiler nor the best optimization level.  The reason is that with this compiler and
level of optimization, we have a certain level of control:

 * Had we used the intel compiler, the "simple loops" in MMult0.c would probably have yielded quite good performance:  This compiler is very good at optimizing a triple loop.  Try it!!!

 * Had we used -O3 (optimization level 3), the gnu compiler would have more aggressively optimized, making the step-by-step optimizations we demonstrate much less predictable.
