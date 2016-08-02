Copy the contents of file `MMult_1x4_4.c` into a file named `MMult_1x4_5.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_4)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_5)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_1x4_4
NEW  := MMult_1x4_5     
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-4_MMult-1x4-5.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-4_MMult-1x4-5.png,width=40%)]]

Now we start seeing a performance benefit.  The reason is that the four loops have been fused and therefore the four inner products are now being performed simultaneously.    This has the following benefits:
 
 * The index `p` needs only be updated once every eight floating point operations.

 * Element `A( 0, p )` needs only be brought in from memory once instead of four times.  (This only becomes a benefit when the matrices no longer fit in the L2 cache.)