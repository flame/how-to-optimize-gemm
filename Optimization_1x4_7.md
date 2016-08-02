Copy the contents of file `MMult_1x4_6.c` into a file named `MMult_1x4_7.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_6)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_7)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_1x4_6
NEW  := MMult_1x4_7     
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-6_MMult-1x4-7.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-6_MMult-1x4-7.png,width=40%)]]

We now use four pointers, `bp0_pntr`, `bp1_pntr`, `bp2_pntr`, and `bp3_pntr`, to access the elements `B( p, 0 )`, `B( p, 1 )`, `B( p, 2 )`, `B( p, 3 )`.  This reduces indexing overhead.

