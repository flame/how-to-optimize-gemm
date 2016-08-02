Copy the contents of file `MMult_4x4_13.c` into a file named `MMult_4x4_14.c` and change the contents:


Change the first lines in the `makefile` to
```makefile
OLD  := MMult_4x4_13
NEW  := MMult_4x4_14
```
 * `make run`
```matlab
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like

![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-4x4-13_MMult-4x4-14.png)


We now pack the kx4 blocks of B.  Notice that in this version, the panels are packed repeatedly, adversely affecting performance.

