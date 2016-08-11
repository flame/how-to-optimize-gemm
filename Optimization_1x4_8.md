Copy the contents of file [`MMult_1x4_7.c`](../blob/master/src/MMult_1x4_7.c) into a file named [`MMult_1x4_8.c`](../blob/master/src/MMult_1x4_8.c) and change the contents.

Change the first lines in the `makefile` to
```makefile
OLD  := MMult_1x4_7
NEW  := MMult_1x4_8     
```
 * `make run`
```matlab
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like

![](../raw/master/figures/compare_MMult-1x4-7_MMult-1x4-8.png)

We now unrolled the loop by four.  Interestingly enough, this decreases performance slightly.  What this probably means is that by adding the optimization, we confused the compiler, which therefore could not do an optimization that it did before.

