Copy the contents of file `MMult_4x4_9.c` into a file named `MMult_4x4_10.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_9)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_10)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_4x4_9
NEW  := MMult_4x4_10
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-9_MMult-4x4-10.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-9_MMult-4x4-10.png,width=40%)]]


Finally, we use the vector registers and vector operations.