Copy the contents of file `MMult_4x4_7.c` into a file named `MMult_4x4_8.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_7)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_8)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_4x4_7
NEW  := MMult_4x4_8
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-7_MMult-4x4-8.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-7_MMult-4x4-8.png,width=40%)]]


We now use registers to store the elements of the current row of B.  (Notice that we did not do this for the case where we computed C four elements at a time.)  The performance actually drops slightly.  But this step enables further optimizations.
