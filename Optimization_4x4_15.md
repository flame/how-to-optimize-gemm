Copy the contents of file `MMult_4x4_14.c` into a file named `MMult_4x4_15.c` and change the contents:

Change the first lines in the `makefile` to
```makefile
OLD  := MMult_4x4_14
NEW  := MMult_4x4_15
```
 * `make run`
```matlab
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like

![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-4x4-14_MMult-4x4-15.png)


And, again, we add some code that makes it so that we avoid repacking the kx4 blocks of B.  Performance is now impressive!
}}}
