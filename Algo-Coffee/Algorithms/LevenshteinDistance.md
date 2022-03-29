# Levenshtein Distance

The levenshtein distance between 2 strings represent the minimal differences that must be applied to the first string to get it to be equivalent to the seconds string.

The 3 operations that be applied are (1) Insertion, (2) Deletion, (3) Swap. An insertion and deletion can be at any point in the string and a swap is just changing an existing letter. There is a recursive equation that is used in a **dynamic programming** fashion to determines the levenshtein distance of 2 strings.

<center>

$\text{lev}_{s1, s2}(i,j) = \left\{
\begin{array}{ll}
        \max(i,j) & \text{if }\min(i,j) = 0 \\
        \text{lev}(i-1,j-1) & \text{if } s1[i] = s2[j]\\
        \min\left\{
        \begin{array}{l}
            \text{lev}_{s1, s2}(i - 1,j) + 1 \\
            \text{lev}_{s1, s2}(i,j - 1) + 1 \\
            \text{lev}_{s1, s2}(i - 1,j - 1) + 1 \\
        \end{array}
        \right. & \text{else}
\end{array} 
\right.$

</center>

Let's breakdown this equation and how it works. 
1. The variables $i$ and $j$ are the inclusive terminating indices of a string. You must consider these to be be 1-indexed where the first character has an index of 1. If it is not clear why we are doing this, I think it will make more sense when we do an example as the reason is highly motivated by the recursive nature of levenshtein distance.
2. The $\max(i,j)$ can be considered the base case. The condition necessary for this is that the minimal index of either $i$ or $j$ is 0; or in otherwords, comparing 2 strings where at least 1 string is the empty string. In the case that one string is an empty string, the levenshtein distance will just be the length of the other string. This also holds true when both strings are empty string.
3. The other base case is when the character is the same, $s1[i] = s2[j]$. In this case, the levenshtein distance does not increase.
4. If the condition in (2) was not met, we are then given the choice of 3 additional functions, where we will that the minimum of the 3.
    - $\text{lev}_{s1, s2}(i - 1,j)$ is insertion/deletion
    - $\text{lev}_{s1, s2}(i,j - 1)$ is insertion/deletion w.r.t the other string.
    - $\text{lev}_{s1, s2}(i - 1,j - 1)$ is a swap

### example
The classical example for levenshtein distance is finding the distance between "kitten" and "sitting". There are several good exampled layed out online. I will go over the example using "france" and "strange".
Note that `#` represents a empty string
```
  i 0 1 2 3 4 5 6 7 
j   # s t r a n g e
0 #
1 f
2 r
3 a
4 n
5 c
6 e
```

1. Lets compute the base cases. The base cased include the first column and the first row, where the $\min(i,j)=0$. Consider $i=3$ and $j=0$. The minimum length is $0$ and the max is $3$. The intuition behind this is because inorder to transform and empty string `""` to `"str"` is 3 insertions of `s`,`t`, and `r`

```
  i 0 1 2 3 4 5 6 7 
j   # s t r a n g e
0 # 0 1 2 3 4 5 6 7
1 f 1
2 r 2
3 a 3
4 n 4
5 c 5
6 e 6
```
2. Next we must apply the recursive case to the subsequent missing spots. 

Consider $i=1$, $j=1$. Since neither index is $0$ and the characters at those indices don't match, we are left with the following.
<center>

$\text{lev}(1,1) = \min\left\{
    \begin{array}{ll}
        \text{lev}(0,1) + 1 \\
        \text{lev}(1,0) + 1 \\
        \text{lev}(0,0) + 1 \\
    \end{array} 
\right.$

</center>

- $\text{lev}(0,1) + 1$ represents a table lookup at $(0,1)$ where we store the number of moves necessary to get the substring with terminating indices of $i=0$ and $j=1$ to match. We then add 1 to represent an insertion.
- $\text{lev}(1,0) + 1$ represents a table lookup at $(1,0)$ where again, the necessary moves are store. This time the insertion can be thought of with respects to the other substring.
- $\text{lev}(0,0) + 1$, in the case where the two characters are different, represent swapping out a letter to be another. This can be with respects to either word.

<center>

$\text{lev}(1,1) = \min\left\{
    \begin{array}{ll}
        1 + 1 \\
        1 + 1 \\
        0 + 1 \\
    \end{array} 
\right. \text{ or } 1$

</center>

We will then repeat this process for all the missing entries.

```
  i 0 1 2 3 4 5 6 7 
j   # s t r a n g e
0 # 0 1 2 3 4 5 6 7
1 f 1 1 2 3 4 5 6 7
2 r 2 1 2 2 3 4 5 6
3 a 3 2 2 3 2 3 4 5
4 n 4 3 3 3 3 2 3 4
5 c 5 4 4 4 4 3 3 4
6 e 6 5 5 5 5 5 5 3
```

The levenshtein distance will be the number in the bootom right on the table. In this case its 3. We can confirm this because be inspection: (1) swap `f` and `s`, (2) insert `t` after the first swap then (3) swap `c` for `g`.