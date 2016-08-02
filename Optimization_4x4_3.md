Copy the contents of file `MMult2.c` into a file named `MMult_4x4_3.c` and change the contents:

Change the first lines in the `makefile` to
```makefile
OLD  := MMult2
NEW  := MMult_4x4_3       # Notice the two underscores!!
```
 * `make run`
```matlab
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like

![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult2_MMult-4x4-3.png)
![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-1x4-3_MMult-4x4-3.png)


No performance benefit, yet.
