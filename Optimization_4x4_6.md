Copy the contents of file `MMult_4x4_5.c` into a file named `MMult_4x4_6.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_5)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_4x4_6)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_4x4_5
NEW  := MMult_4x4_6
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-5_MMult-4x4-6.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-4x4-5_MMult-4x4-6.png,width=40%)]]
[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-6_MMult-4x4-6.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-6_MMult-4x4-6.png,width=40%)]]

The performance benefits from the fact that we use (regular) registers for the 4x4 block of C and the elements of the current 4x1 column of A.  Notice that we are using more regular registers than there exist, so it is anyone's guess what the compiler does with that.
