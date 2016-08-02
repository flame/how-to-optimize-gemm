Copy the contents of file `MMult_4x4_9.c` into a file named `MMult_4x4_10.c` and change the contents:


Change the first lines in the `makefile` to
```makefile
OLD  := MMult_4x4_9
NEW  := MMult_4x4_10
```
 * `make run`
```matlab
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like


![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-4x4-9_MMult-4x4-10.png)



Finally, we use the vector registers and vector operations.