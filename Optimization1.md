Copy the contents of file `MMult0.c` into a file named `MMult1.c` and change the contents:

 || from || to ||
 ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult0)]]-~ ||<^> ~-[[Include(HowToOptimizeGemm/Details/MMult1)]]-~ ||

Change the first lines in the `makefile` to
```makefile
OLD  := MMult0
NEW  := MMult1
```

 * `make run`
```matlab
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like

![](http://www.cs.utexas.edu/users/rvdg/HowToOptimizeGemm/Graphs/compare_MMult0_MMult1.png)

We see no performance benefit.  What we are doing is slowly changing the code into one where there will be a performance benefit.
