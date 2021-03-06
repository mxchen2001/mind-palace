# Branchless Programming

The use of if-then-else statements, switch cases, and even goto's are considered as branch operations. In the world of computing, the single operation that slows down the pipeline of instructions is the branch. The reason is because branch instruction depends on the result of the previous instruction. The whole concept of branch prediction is another topic that deserves its own discussion.

Imagine you have the following code:

```c
int isGreater(int a, int b) {
    if (a > b) {
        return a;
    } else {
        return b;
    }
}
```

Notice that there exist an if-else clause in the code.

```c
int isGreaterBL(int a, int b) {
    return a > b & a | a <= b & b;
}
```

We removed the branch by replacing the if-else clause with a bitwise operation.

Another cool example is the absolute value of an integer by Jobin Johnson.

```c
int abs(int a) {
    if (a < 0) {
        return -a;
    } else {
        return a;
    }
}
```

```c
int abs(int a) {
    int mask = a >> 31;
    a ^= mask;
    a -= mask;
    return a;
}
```