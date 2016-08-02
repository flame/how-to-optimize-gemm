Copy the contents of file `MMult_4x4_10.c` into a file named `MMult_4x4_11.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_10)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_11)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_4x4_10
NEW  := MMult_4x4_11
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-10_MMult-4x4-11.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-10_MMult-4x4-11.png,width=40%)]]

What we noticed is that for all optimizations so far, performance degraded considerably when the matrices involved were much bigger than could fit in the L2 cache.  In this optimization, we create an extra level of blocking to overcome this.  We now have a main routine that calls what is the `inner kernel` used by the GotoBLAS and BLIS, and then the `AddDot4x4` routine is the micro-kernel used by BLIS.

