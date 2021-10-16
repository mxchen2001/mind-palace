# Matrix Multiplication (WIP)

Maybe one of the most common operation that a computer does as of today is matrix multiplication. The traditional mathematic way a person will multiply a matrix by hand is to compute an element by scanning the rows of the first matrix and the columns of the seconds.

```
+-        -+  +-        -+
| A0 B0 C0 |  | X0 Y0 Z0 |  
| A1 B1 C1 |  | X1 Y1 Z1 |  
| A2 B2 C2 |  | X2 Y2 Z2 |
+-        -+  +-        -+

+-                                 -+
| A0*X0 + B0 * X1 + C0 * X2  ...    |  
| A1*X0 + B1 * X1 + C1 * X2  ...    |  
| A2*X0 + B2 * X1 + C2 * X2  ...    |  
+-                                 -+
```

We can compute the N by N resultant matrix using 3 for loops. The outer loop iterates over N-rows, the middle loop iterates over N-columns, and the inner loop sums N-products to produce the resultant matrix.

```c
for (int i = 0; i < N; i++) {
    for (int j = 0; j < N; j++) {
        for (int k = 0; k < N; k++) {
            C[i][j] += A[i][k] * B[k][j];
        }
    }
}
```

Assuming that every element of the resultant matrix is unique and therefore independently computed, the time complexity of the algorithm is O(N^3).

Lets also assume the matrix is stored contiguously in memory and in row-major order.

```
     +-----+          +-----+     
     | A0  |          | X0  |      
     +-----+          +-----+     
     | B0  |          | Y0  |      
     +-----+          +-----+     
     | C0  |          | Z0  |      
     +-----+          +-----+     
     | A1  |          | X1  |      
     +-----+          +-----+     
     | B1  |          | Y1  |      
     +-----+          +-----+     
     | C1  |          | Z1  |      
     +-----+          +-----+     
     | A2  |          | X2  |      
     +-----+          +-----+     
     | B2  |          | Y2  |      
     +-----+          +-----+     
     | C2  |          | Z2  |      
     +-----+          +-----+     
```

Lets assume that little computer ( ͡° ͜ʖ ͡°) that we are working with has a single level of cache where the cache can only hold 2 cache lines. Lets additionally assume that a cache line for us is 3 words of memory. 

Assuming both matricies start at the beginning of a cache line, we can visualize them in the following way.
```
     +----+----+----+        +----+----+----+
     | A0 | B0 | C0 |        | X0 | Y0 | Z0 |
     +----+----+----+        +----+----+----+  
     
     +----+----+----+        +----+----+----+
     | A1 | B1 | C1 |        | X1 | Y1 | Z1 |
     +----+----+----+        +----+----+----+  

     +----+----+----+        +----+----+----+
     | A2 | B2 | C2 |        | X2 | Y2 | Z2 |
     +----+----+----+        +----+----+----+  
```


Notice that during the execution of the matrix multiplication based on the code aboue, since ABC is being scanned in a row-major order, a single cache line is being used to compute a entries of the resultant matrix. However, at the same time, for every element ABC in the cache line, it must be multiplied with an element from XYZ in 3 different cache lines.

To make it so that the XYZ-matrix is also being scanned without jumps, we can store the matrix in column-major order.

```
     +-----+          +-----+     
     | A0  |          | X0  |      
     +-----+          +-----+     
     | B0  |          | X1  |      
     +-----+          +-----+     
     | C0  |          | X2  |      
     +-----+          +-----+     
     | A1  |          | Y0  |      
     +-----+          +-----+     
     | B1  |          | Y1  |      
     +-----+          +-----+     
     | C1  |          | Y2  |      
     +-----+          +-----+     
     | A2  |          | Z0  |      
     +-----+          +-----+     
     | B2  |          | Z1  |      
     +-----+          +-----+     
     | C2  |          | Z2  |      
     +-----+          +-----+   
```

Now that first matrix is stored in row-major order and the second matrix is stored in column-major order, we can compute 