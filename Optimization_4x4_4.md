Copy the contents of file `MMult_4x4_3.c` into a file named `MMult_4x4_4.c` and change the contents:


Change the first lines in the `makefile` to
```makefile
OLD  := MMult_4x4_3
NEW  := MMult_4x4_4
```
 * `make run`
```matlab
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like


![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-4x4-3_MMult-4x4-4.png)
![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-1x4-4_MMult-4x4-4.png)


No performance benefit, yet.
