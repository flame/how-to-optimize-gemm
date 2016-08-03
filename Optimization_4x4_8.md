Copy the contents of file [`MMult_4x4_7.c`](https://github.com/SudoNohup/HowToOptimizeGemm/blob/master/src/MMult_4x4_7.c) into a file named [`MMult_4x4_8.c`](https://github.com/SudoNohup/HowToOptimizeGemm/blob/master/src/MMult_4x4_8.c) and change the contents:


Change the first lines in the `makefile` to
```makefile
OLD  := MMult_4x4_7
NEW  := MMult_4x4_8
```
 * `make run`
```matlab 
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like

![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-4x4-7_MMult-4x4-8.png)


We now use registers to store the elements of the current row of B.  (Notice that we did not do this for the case where we computed C four elements at a time.)  The performance actually drops slightly.  But this step enables further optimizations.
