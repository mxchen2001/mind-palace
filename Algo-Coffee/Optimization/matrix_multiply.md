# Matrix Multiplication

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
            M[i][j] += A[i][k] * B[k][j];
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

Lets assume that little computer ( ͡° ͜ʖ ͡°) that we are working with has a single level of cache where the cache can only hold 3 cache lines. Lets additionally assume that a cache line for us is 3 words of memory. 

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

We will represent the resultant matrix in a similar manner
```

               +-----+-----+-----+
               | M00 | M01 | M02 |
               +-----+-----+-----+ 

               +-----+-----+-----+
               | M10 | M11 | M12 |
               +-----+-----+-----+ 

               +-----+-----+-----+
               | M20 | M21 | M22 |
               +-----+-----+-----+ 
```

Notice that during the execution of the matrix multiplication based on the code above, since ABC is being scanned in a row-major order, a single cache line is being used to compute a entries of the resultant matrix. However, at the same time, for every element ABC in the cache line, it must be multiplied with an element from XYZ in 3 different cache lines. Since our little computer's cache can only hold 3 cache lines at a time, every multiply will incur a cache miss.

```
Cache Content: Empty

Operation:     M[0,0] += A0 * X0

Cache Content: +----+----+----+        
               | A0 | B0 | C0 |    Miss     
               +----+----+----+ 

               +-----+-----+-----+
               | M00 | M01 | M02 | Miss
               +-----+-----+-----+ 

               +----+----+----+
               | X0 | Y0 | Z0 |    Miss
               +----+----+----+ 

Operation:     M[0,0] += B0 * X1

Cache Content: +----+----+----+        
               | A0 | B0 | C0 |    Hit        
               +----+----+----+ 

               +-----+-----+-----+
               | M00 | M01 | M02 | Hit
               +-----+-----+-----+ 

               +----+----+----+
               | X1 | Y1 | Z1 |    Miss
               +----+----+----+ 

Operation:     M[0,0] += C0 * X2

Cache Content: +----+----+----+        
               | A0 | B0 | C0 |    Hit     
               +----+----+----+ 

               +-----+-----+-----+
               | M00 | M01 | M02 | Hit
               +-----+-----+-----+ 

               +----+----+----+
               | X2 | Y2 | Z2 |    Miss
               +----+----+----+ 
```

For computing a single entry in the resultant matrix, we had to access memory 5 times (3 + 1 + 1), which is a total of 4 cache misses. 

Lets assume that a cache hit costs 1 time unit or tu, and a cache miss that results in a memory acees costs 200 tu. (This is based on the  "Latency Numbers Every Programmer Should Know")

The total time cost of our current algorithm will is 600 + 201 + 201 or 1002 tu for a single entry (or 3 iterations) in the resultant matrix.


To make the matrix multiplication algorithm more efficient, we change the order of the loops.

```c
        for (int k = 0; k < N; k++) {
for (int i = 0; i < N; i++) {
    for (int j = 0; j < N; j++) {
            M[i][j] += A[i][k] * B[k][j];
        }
    }
}
```

Notice that the layout of the matrix is still the same, the only difference is that the inner loop is now moved

```
Cache Content: Empty

Operation:     M[0,0] += A0 * X0


Cache Content: +----+----+----+        
               | A0 | B0 | C0 |    Miss     
               +----+----+----+ 

               +-----+-----+-----+
               | M00 | M01 | M02 | Miss
               +-----+-----+-----+ 

               +----+----+----+
               | X0 | Y0 | Z0 |    Miss
               +----+----+----+ 

Operation:     M[0,1] += A0 * Y0

Cache Content: +----+----+----+        
               | A0 | B0 | C0 |    Hit        
               +----+----+----+ 

               +-----+-----+-----+
               | M00 | M01 | M02 | Hit
               +-----+-----+-----+ 

               +----+----+----+
               | X0 | Y0 | Z0 |    Hit
               +----+----+----+ 

Operation:     M[0,2] += A0 * Z0

Cache Content: +----+----+----+        
               | A0 | B0 | C0 |    Hit     
               +----+----+----+ 

               +-----+-----+-----+
               | M00 | M01 | M02 | Hit
               +-----+-----+-----+ 

               +----+----+----+
               | X0 | Y0 | Z0 |    Hit
               +----+----+----+ 
```

After 3 iterations, we have computed 1/3 of 3 entries. This is equivalent to that amount of work required to compute a single entry. Notice that unlike the first algorithm, there are only 3 misses and the rest are cache hits. This will result in a runtime of (600 + 3 + 3) or 606 tu.

Let do a runtime analysis of the entire matrix muliplication.

1. Since the matrix operands are both 3x3, the resultant matrix will be of size 3x3.
2. Since the resultant matrix contain 9 entries, there will be 3 iterations per entry.

Original Algorithm:

cache: {[A0, B0, C0], [M00, M01, M02], [X0, Y0, Z0]}, 3 miss, 0 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X1, Y1, Z1]}, 1 miss, 2 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X2, Y2, Z2]}, 1 miss, 2 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X0, Y0, Z0]}, 1 miss, 2 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X1, Y1, Z1]}, 1 miss, 2 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X2, Y2, Z2]}, 1 miss, 2 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X0, Y0, Z0]}, 1 miss, 2 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X1, Y1, Z1]}, 1 miss, 2 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X2, Y2, Z2]}, 1 miss, 2 hits

cache: {[A1, B1, C1], [M10, M11, M12], [X0, Y0, Z0]}, 3 miss, 0 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X1, Y1, Z1]}, 1 miss, 2 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X2, Y2, Z2]}, 1 miss, 2 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X0, Y0, Z0]}, 1 miss, 2 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X1, Y1, Z1]}, 1 miss, 2 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X2, Y2, Z2]}, 1 miss, 2 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X0, Y0, Z0]}, 1 miss, 2 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X1, Y1, Z1]}, 1 miss, 2 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X2, Y2, Z2]}, 1 miss, 2 hits

cache: {[A2, B2, C2], [M20, M21, M22], [X0, Y0, Z0]}, 3 miss, 0 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X1, Y1, Z1]}, 1 miss, 2 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X2, Y2, Z2]}, 1 miss, 2 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X0, Y0, Z0]}, 1 miss, 2 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X1, Y1, Z1]}, 1 miss, 2 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X2, Y2, Z2]}, 1 miss, 2 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X0, Y0, Z0]}, 1 miss, 2 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X1, Y1, Z1]}, 1 miss, 2 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X2, Y2, Z2]}, 1 miss, 2 hits

Total: 33 miss, 48 hits
Runtime: 33(200) + 48(1) = 6648 tu.

Improved Algorithm:

cache: {[A0, B0, C0], [M00, M01, M02], [X0, Y0, Z0]}, 3 miss, 0 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X0, Y0, Z0]}, 0 miss, 3 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X0, Y0, Z0]}, 0 miss, 3 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X0, Y0, Z0]}, 2 miss, 1 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X0, Y0, Z0]}, 0 miss, 3 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X0, Y0, Z0]}, 0 miss, 3 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X0, Y0, Z0]}, 2 miss, 1 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X0, Y0, Z0]}, 0 miss, 3 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X0, Y0, Z0]}, 0 miss, 3 hits

cache: {[A0, B0, C0], [M00, M01, M02], [X1, Y1, Z1]}, 3 miss, 0 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X1, Y1, Z1]}, 0 miss, 3 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X1, Y1, Z1]}, 0 miss, 3 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X1, Y1, Z1]}, 2 miss, 1 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X1, Y1, Z1]}, 0 miss, 3 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X1, Y1, Z1]}, 0 miss, 3 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X1, Y1, Z1]}, 2 miss, 1 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X1, Y1, Z1]}, 0 miss, 3 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X1, Y1, Z1]}, 0 miss, 3 hits

cache: {[A0, B0, C0], [M00, M01, M02], [X2, Y2, Z2]}, 3 miss, 0 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X2, Y2, Z2]}, 0 miss, 3 hits
cache: {[A0, B0, C0], [M00, M01, M02], [X2, Y2, Z2]}, 0 miss, 3 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X2, Y2, Z2]}, 2 miss, 1 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X2, Y2, Z2]}, 0 miss, 3 hits
cache: {[A1, B1, C1], [M10, M11, M12], [X2, Y2, Z2]}, 0 miss, 3 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X2, Y2, Z2]}, 2 miss, 1 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X2, Y2, Z2]}, 0 miss, 3 hits
cache: {[A2, B2, C2], [M20, M21, M22], [X2, Y2, Z2]}, 0 miss, 3 hits

Total: 21 miss, 60 hits
Runtime: 21(200) + 60(1) = 4260 tu.

The runtime improved from 6648 to 4260, or a decrease of 35.92%.