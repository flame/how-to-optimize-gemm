Copy the contents of file `MMult_4x4_13.c` into a file named `MMult_4x4_14.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_13)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_14)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_4x4_13
NEW  := MMult_4x4_14
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-13_MMult-4x4-14.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-13_MMult-4x4-14.png,width=40%)]]


We now pack the kx4 blocks of B.  Notice that in this version, the panels are packed repeatedly, adversely affecting performance.

