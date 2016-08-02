Copy the contents of file `MMult_4x4_6.c` into a file named `MMult_4x4_7.c` and change the contents:

Change the first lines in the `makefile` to
```makefile
OLD  := MMult_4x4_6
NEW  := MMult_4x4_7
```
 * `make run`
```matlab
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like

![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-4x4-6_MMult-4x4-7.png)
![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-1x4-7_MMult-4x4-7.png)


Here We changed to using pointers to track the current 4x1 block of B.
