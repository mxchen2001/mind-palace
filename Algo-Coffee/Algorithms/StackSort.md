# Stack Sort

Given a stack of numbers, you are tasked with sorting this stack of numbers in non-decreasing order where the bottom element of the stack is smallest number. The constraints are that you can only use stack operation PUSH and POP and you cannot use loops (for, while, do while, goto, ...).

At first this problem can seem difficult since PUSH and POP can only modify the top of the stack. 

Imagine you have a stack of exams that you must sort by students last names. You can't reach into the middle of the stack because doing so will disturb the papers above it and cause those papers will fall on the ground. Therefore you can only take from the top.

You take a look at the first exam and see "Fred Foo". You decide to put Fred's exam down and start a new 'stack' of papers. Next you see "Bob Bar". Since "B" is before "F" in the alphabet, you can just put the paper on top of the new stack. Your current stack is:

```
     +-----+     
     | Bar |      
     +-----+     
     | Foo |      
     +-----+    
```

The next exam on the original stack is "Dave Dos". You realize that "D" is after "B" in the alphabet, so you take Bob's exam and lift it up so you can put Dave's exam below. Next you realize that "D" is before "F" in the alphabet, so you can just put the paper ontop of Fred's exam. Then since you are holding Bob's exam paper and already placed Dave's paper in the correct place, you will put Bob's exam  ontop of Dave's exam.

```
     +-----+     
     | Bar |      
     +-----+     
     | Dos |      
     +-----+    
     | Foo |      
     +-----+    
```
The act of lifting Bob's paper can be considered a POP, the act of putting Dave's paper down can be considered a PUSH, and the act of putting Bob's paper back can also be considerd a PUSH. Realize that everytime we take a paper from the first stack and put it on the second stack, we are adding to a stack of paper that are already sorted in alphabetical order.

The second constraints is that we are not allowed to use any loops. Since the stack of numbers to be sorted is not known in advance, we must turn to recursion.

The beauty of recursion comes from the assumption that everytime we transfer an element from the original stack to the new stack, the new stack is already in sorted order. All we are doing is inserting the element into the correct position by poping values that come before it then push them back in order to keep the stack sorted for the next value.


We will take this intuition and apply it to sort a stack of numbers.

```python
"""
insert_stack() recursively inserts an element into a sorted stack using PUSH and POP operations.
"""
def insert_stack(stack, el):
    # if the stack is empty, or we have reach the correct placement of the element
    if len(stack) == 0 or stack[-1] < el:
        stack.append(el)
        return

    last = stack.pop()
    insert_stack(stack, el)
    stack.append(last)
    return

"""
sort_stack() recursively clears the original stack, thereby creating the "new" stack.
Note: the original stack element exists in "last" variable of each stack frame.
"""
def sort_stack(stack):
    last = stack.pop()
    sorted_stack = sort_stack(stack)
    insert_stack(sorted_stack, last)
    return sorted_stack
```