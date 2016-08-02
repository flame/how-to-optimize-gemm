Copy the contents of file `MMult2.c` into a file named `MMult_1x4_3.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult2)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_3)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult2
NEW  := MMult_1x4_3       # Notice the two underscores!!
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult2_MMult-1x4-3.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult2_MMult-1x4-3.png,width=40%)]]

Still, no performance benefit.
