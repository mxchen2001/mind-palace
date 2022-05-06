# Aho-Corasick

Aho Corasick is a fast and efficient method for finding all substrings from a dictionary that exists in a string.  Named after Alfred V. Aho and Margaret Corasick, the algorithm utilizes a data structure called a trie in the format of a state machine to, in linear time, perform the search.

I recently got asked an interesting question that is a perfect fit for this algorithm.  I will discuss the question after explaining the algorithm.

## Algorithm

The basis for the algorithm is to construct a special trie.

1. Create the root node that is the empty string.
2. Starting with the first letter, construct $n$ neighboring nodes for which the value is the the parent node concatenated with the immediate letter following the parent for which the value of the contructed node is a string or substring from your dictionary.
3. Continue this process until you reach constructed all strings from your dictionary.
4. For every node, we will construct a failure edge that connects to a node that is closer to the root and contains as much of prefix characters up to the current letter.

### example

Let our dictionary contain the following words: 

<center>

$dict = \{cat,  car,  ate\}$

</center>

```plaintext
Trie:
    .
    ├── c
    │   ├── ca
    │   │   └── cat
    │   └── ca
    │       └── car
    └── a
        └── at
            └── ate

Failure edges:
    c -> .
    a -> .
    ca -> a
    at -> .
    ate -> .
    cat -> at
    car -> .
```

Lets take a look on how we constructed the failure edges.

1. For `['c', 'a']`, since the root node is only node above the current nodes, it will be the only failure nodes.
2. For `'ca'`, there are 3 possible nodes the failure edge can connect to, `['c', 'a', .]`. The longest substring that is a prefix of the current node is `'c'`, so we will connect the failure edge of `'ca'` to `'c'`.
3. For `'cat'`, the longest substring that is a prefix of the current node is `'ca'`, so we will connect the failure edge of `'cat'` to `'ca'`
4. For `['at', 'ate', 'car']`, the longest substring that is that is a prefix and which is a earlier node is the empty string, so we will connect the failure edge of those nodes to `'.'`
