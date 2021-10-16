# Tail Recusion

For algorithms that involve recursion, we can implement tail recursion in certain cases to reduce the memory usage of the program.

This usually applies to algorithms where the solution is computed at the last step of the recursion, where the solution is then propagated back down through each stack frame. Many times, we can implement recursive algorithms in a way that statisfies this property.

A simple example is computing the factorial of a number. 
```c
int factorial(int n) {
    if (n <= 1) return 1
    return n * factorial(n - 1);
}

int factorialTailRecur(int n, int current) {
    if (n <= 1) return current
    return factorialTailRecur(n - 1, current * n);
}
```

Notice the runtime of both the regular and tail recursion version of the algorithm is the same.

However, we can implement the tail recursion version of the factorial algorithm in a more memory efficient way. The runtime of the optimized tail recursive algorithm has the same time complexity as the both the regular and tail recursive version, but has a space complexity of O(1).

```c
int factorialTailRecurOpt(int n) {
    int current = 1;
    while(1) {
        if (n <= 1) return current
        current *= n;
        n -= 1;
    }
}
```

