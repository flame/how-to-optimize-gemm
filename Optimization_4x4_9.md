Copy the contents of file `MMult_4x4_8.c` into a file named `MMult_4x4_9.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_8)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_9)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_4x4_8
NEW  := MMult_4x4_9
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-8_MMult-4x4-9.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-8_MMult-4x4-9.png,width=40%)]]


From 4x4_8 to 4x4_9 is a subtle change: instead of updating the rows of 4x4 block C a row at a time, we compute them two rows at a time.  This sets us up for using vector operations, where we update pairs C( 0,j ) and C( 1,j ) (j =0,...,3) with vector operations.
