# Branch Prediction

Branches are a basic construct in the world of computing — they are used everywhere whether it is an `if` statement or a `for` loop, it is very rare that you will never run into a branch.

If branches are everywhere, what can we do to speed up them up? The answer here is **branch prediction**.

## Static Branch Predictors

There are some simple static branch predictor that can improve the performance when running a program. 

The **Backwards Taken Forward Not Taken** or BTFN prediction scheme states to always take the branch that leads to an earlier statement in the program. The major improvement we see is when we run into a *loop*.

## Dynamic Branch Predictor

The simplest form of dynamic branch predictor is the **Last Time Taken** prediction scheme. This scheme just says to take the choice of the previous branch, then update the bit with the actual direction of the branch. This prediction scheme only require a single additional bit.

A minor step up but a major performance increase is the **2-bit Saturating Counter**. The 2-bit counter represents the history of the branches we have seen where the MSB (most significant bit) is representative of how to take the branch; 1 is to take and 0 is to not take. When we take the branch, we will increment the counter until we reach `11` where we stop. Similar when we don't take the branch, we will decrement the counter untill we reach `00`. The saturating nature of this scheme stops the counters at `00` and `11`.

```
      +---+
    T |   |
      V   |  NT
     +-----+     
     | 00  |      
     +-----+     
    T |   ^ 
      V   |  NT
     +-----+     
     | 01  |      
     +-----+     
    T |   ^ 
      V   |  NT
     +-----+     
     | 10  |      
     +-----+     
    T |   ^ 
      V   |  NT
     +-----+     
     | 11  |      
     +-----+     
    T |   ^
      |   |
      +---+
```

A major step up is the **2 Level Dynamic Branch Predictor** by Yale Patt. This utilizes 2 new constructs, a *Branch History Register* or BHR and a *Pattern History Table* or PHT. The branch history register contains the history of previous branches where a 0 represents not taken and 1 represents taken. When we see the result of a new branch, the oldest history bit is shifted out and the new branch result if shifted into the register. Additionally, we have a pattern history table where for each history pattern we will index into a table where each entry is a 2-bit saturating counter. For a history register of length $n$, the pattern history table will be of size $2^n$.

A problem with the 2 level predictor occurs when 2 branches have the same pattern. A simple modification **GSHARE** can be performed, where the contents of the branch history register is XOR with random bits of the PC. This will hash the pattern such that common history patterns will map to different entries in the pattern history table.

I will talk about TAGE later.



