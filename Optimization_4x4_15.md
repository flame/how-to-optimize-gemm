Copy the contents of file `MMult_4x4_14.c` into a file named `MMult_4x4_15.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_14)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_15)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_4x4_14
NEW  := MMult_4x4_15
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-14_MMult-4x4-15.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-14_MMult-4x4-15.png,width=40%)]]


And, again, we add some code that makes it so that we avoid repacking the kx4 blocks of B.  Performance is now impressive!
}}}
