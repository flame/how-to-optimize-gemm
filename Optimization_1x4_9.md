Copy the contents of file `MMult_1x4_8.c` into a file named `MMult_1x4_9.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_8)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult_1x4_9)]]-~ ||

Change the first lines in the `makefile` to
    {{{
OLD  := MMult_1x4_8
NEW  := MMult_1x4_9     
}}}
 * `make run`
  {{{ 
octave:3> PlotAll        % this will create the plot
}}}

This time the performance graph will look something like

[[ImageLink(http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-8_MMult-1x4-9.png,http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult-1x4-8_MMult-1x4-9.png,width=40%)]]

We now use something called 'indirect addressing'.   Notice, for example, the line 
{{{
    c_00_reg += a_0p_reg * *(bp0_pntr+1);
}}}
Here 

 *`a0p_reg` holds the element `A( 0, p+1 )`  (yes, this is a bit confusing.  A better name for the variable would be good...)

 * We want to `bp0_pntr' points to element `B( p, 0 )`.  Hence `bp0_pntr+1' addresses the element `B( p+1, 0 )`.  There is a special machine instruction to then access the element at `bp0_pntr+1' that does not require the pointer to be updated.

 * As a result, the pointers that address the elements in the columns of B only need to be updated once every fourth iteration of the loop.

Interestingly, it appears that the compiler did this optimization automatically, and hence we see no performance improvement...
