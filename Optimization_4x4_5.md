Copy the contents of file [`MMult_4x4_4.c`](https://github.com/SudoNohup/HowToOptimizeGemm/blob/master/src/MMult_4x4_4.c) into a file named [`MMult_4x4_5.c`](https://github.com/SudoNohup/HowToOptimizeGemm/blob/master/src/MMult_4x4_5.c) and change the contents:


 * Change the first lines in the `makefile` to
```makefile
OLD  := MMult_4x4_4
NEW  := MMult_4x4_5
```
 * `make run`
```matlab 
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like


![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-4x4-4_MMult-4x4-5.png)
![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-1x4-5_MMult-4x4-5.png)

Now we see a performance benefit, when the matrices becomes large, since the data is reused more after being brought into the registers.  On the left is the comparison of `4x4_4` and `4x4_5`.  On the right the comparison of `1x4_5` (computing four elements of C at a time) and `4x4_5` (computing sixteen elements of C at a time).
