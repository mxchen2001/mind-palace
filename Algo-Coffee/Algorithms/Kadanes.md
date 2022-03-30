# Kadanes

Kadanes Algorithm is used to find the maximum sum of a subarray in an array. This is a classic dynamic programming problem that seems like it shouldn't work but ends up working somehow.

Lets take the following example
<center>

$\text{array} = [-2,1,-3,4,-1,2,1,-5,4]$

</center>

In this case the largest contiguous sum is $6$ which include $[4,-1,2,1]$. The naive solution would be to find every contiguous subarray and choose the one with the largest sum, which is an $O(n^2)$ solution. However, with Kadanes algorithm, we can solve this in $O(n)$ time.

I think the best way to understand any dynamic programming problem is to construct a table. Although for this problem, we don't need to construct a table since the recursive statement only depends on the immediate previous value and the data grows 1 dimensional.

The recursive statement is the following where $\text{array}$ is the data we are working with.

<center>

$\text{kad}(i) = \left\{
\begin{array}{ll}
        \text{array}(i) & \text{if } i = 0 \\
        \max(\text{array}(i),\text{array}(i) + kad(i - 1)) & \text{else }\\
\end{array} 
\right.$

</center>

### Example
Lets use the example above.

<center>

$\text{array} = [-2,1,-3,4,-1,2,1,-5,4]$

</center>

We will first construct an empty table the same size as the array.

<center>

$\text{opt} = [-\infty,-\infty,-\infty,-\infty,-\infty,-\infty,-\infty,-\infty,-\infty]$

</center>

We will first fill in the base case where the index is 0.

<center>

$\text{opt} = [-2,-\infty,-\infty,-\infty,-\infty,-\infty,-\infty,-\infty,-\infty]$

</center>

Now since we must use the recursive statement, let's breakdown what it is we are doing. Notice that the recursive statement is for $kad(i)$, which is the returns the largest subarray that ends at index $i$. The actual body of the recursive state is $\max(\text{array}(i),\text{array}(i) + kad(i - 1))$, or in otherwords, the maximum subarray at index $i$ is either the maximum subaarray from the previous index plus the element at the current index, or just the element at the current index.

Knowing this, we can fill in the rest of the table.

<center>

$\text{opt} = [-2,1,-2,4,3,5,6,1,5]$

</center>

We can the scan the table and find the largest value, which represents the largest subarray.

### Optimization

There is something special about Kadanes algorithm such that we don't necessarily need to construct a table. All we need to do is to keep track of the current global max (which is the largest subarray so far) and the current local max (which is the largest subarray ending at the previous index). This will save us some memory.

```py
def kadanes(array):
    # Initialize the global and local max with the base case
    global_max = array[0] 
    local_max = array[0] 

    # Loop through the rest of the array and apply the recursive statement
    for i in range(1,len(array)):
        local_max = max(array[i], local_max + array[i]) 
        global_max = max(global_max, local_max)

    return global_max 
```

This happens to be a [leetcode problem](https://leetcode.com/problems/maximum-subarray/).