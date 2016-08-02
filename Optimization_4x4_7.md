Copy the contents of file `MMult_4x4_6.c` into a file named `MMult_4x4_7.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_6)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_7)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_4x4_6
NEW  := MMult_4x4_7
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-6_MMult-4x4-7.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-6_MMult-4x4-7.png,width=40%)]]
[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-7_MMult-4x4-7.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-7_MMult-4x4-7.png,width=40%)]]

Here We changed to using pointers to track the current 4x1 block of B.
