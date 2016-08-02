Copy the contents of file `MMult_1x4_3.c` into a file named `MMult_1x4_4.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_3)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_4)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_1x4_3
NEW  := MMult_1x4_4     
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-3_MMult-1x4-4.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-3_MMult-1x4-4.png,width=40%)]]

Still, no performance benefit.
