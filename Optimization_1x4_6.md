Copy the contents of file `MMult_1x4_5.c` into a file named `MMult_1x4_6.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_5)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_6)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_1x4_5
NEW  := MMult_1x4_6     
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-5_MMult-1x4-6.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-5_MMult-1x4-6.png,width=40%)]]

Now we start seeing a performance benefit.  We accumulate the updates to the current 1x4 row of C in registers and we place the element A( p, 0 ) in a register, to reduce traffic between cache and registers.
 
