Copy the contents of file `MMult_4x4_11.c` into a file named `MMult_4x4_12.c` and change the contents:

Change the first lines in the `makefile` to
```makefile
OLD  := MMult_4x4_11
NEW  := MMult_4x4_12
```
 * `make run`
```matlab
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like

![](https://github.com/SudoNohup/HowToOptimizeGemm/raw/master/figures/compare_MMult-4x4-11_MMult-4x4-12.png)


We now pack to 4xk block of A before calling `AddDot4x4`.  We see a performance drop.  If one examines the inner kernel
```c
void InnerKernel( int m, int n, int k, double *a, int lda, 
                                       double *b, int ldb,
                                       double *c, int ldc )
{
  int i, j;
  double 
    packedA[ m * k ];

  for ( j=0; j<n; j+=4 ){        /* Loop over the columns of C, unrolled by 4 */
    for ( i=0; i<m; i+=4 ){        /* Loop over the rows of C */
      /* Update C( i,j ), C( i,j+1 ), C( i,j+2 ), and C( i,j+3 ) in
	 one routine (four inner products) */
      PackMatrixA( k, &A( i, 0 ), lda, &packedA[ i*k ] );
      AddDot4x4( k, &packedA[ i*k ], 4, &B( 0,j ), ldb, &C( i,j ), ldc );
    }
  }
}
```

one notices that each 4xk block of A is packed repeatedly, once for every time the outer loop is executed.

