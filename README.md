# How To Optimize Gemm wiki pages
https://github.com/flame/how-to-optimize-gemm/wiki

Copyright by Prof. Robert van de Geijn (rvdg@cs.utexas.edu).

Adapted to Github Markdown Wiki by Jianyu Huang (jianyu@cs.utexas.edu).

# Table of contents

  * [The GotoBLAS/BLIS Approach to Optimizing Matrix-Matrix Multiplication - Step-by-Step](../../wiki#the-gotoblasblis-approach-to-optimizing-matrix-matrix-multiplication---step-by-step)
  * [NOTICE ON ACADEMIC HONESTY](../../wiki#notice-on-academic-honesty)
  * [References](../../wiki#references)
  * [Set Up](../../wiki#set-up)
  * [Step-by-step optimizations](../../wiki#step-by-step-optimizations)
  * [Computing four elements of C at a time](../../wiki#computing-four-elements-of-c-at-a-time)
    * [Hiding computation in a subroutine](../../wiki#hiding-computation-in-a-subroutine)
    * [Computing four elements at a time](../../wiki#computing-four-elements-at-a-time)
    * [Further optimizing](../../wiki#further-optimizing)
  * [Computing a 4 x 4 block of C at a time](../../wiki#computing-a-4-x-4-block-of-c-at-a-time)
    * [Repeating the same optimizations](../../wiki#repeating-the-same-optimizations)
    * [Further optimizing](../../wiki#further-optimizing-1)
    * [Blocking to maintain performance](../../wiki#blocking-to-maintain-performance)
    * [Packing into contiguous memory](../../wiki#packing-into-contiguous-memory)
  * [Acknowledgement](../../wiki#acknowledgement)

# Related Links
* [BLISlab: A Sandbox for Optimizing GEMM] (https://github.com/flame/blislab)
* [GEMM: From Pure C to SSE Optimized Micro Kernels] (http://apfel.mathematik.uni-ulm.de/~lehn/sghpc/gemm/)

# Acknowledgement
This material was partially sponsored by grants from the National Science Foundation (Awards ACI-1148125/1340293).

_Any opinions, findings and conclusions or recommendations expressed in this material are those of the author(s) and do not necessarily reflect the views of the National Science Foundation (NSF)._
