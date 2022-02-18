# Dutch National Flag Problem

The Dutch National Flag Problem is a problem proposed by Dijkstra, a professor of computer science who taught at the University of Texas at Austin. The premise of the problem is that given balls that are randomly arranged with 3 colors: Red, White, and Blue. The goal is to sort the balls will be sorted in groups of Red, then White, then Blue. 

When I was first asked this question, I thought of using a linked-list where when you see a Red ball, you would append it to the front of the list and when you see a Blue ball, you will append it to the end of the list.

The optimal way is to keep track of 3 pointers:
1.  Front Pointer
2.  Middle Pointer
3.  End Pointer

Whenever you see a Red ball when indexing using the Middle Pointer, you will swap it with the Front Pointer and increment both pointers.
Whenever you see a Blue ball when indexing using the Middle Pointer, you will swap it with the End Pointer and decrement the End Pointer.
Whenever you see a White ball ..., you will increment the Middle Pointer.

You can interpret the pointers as:
1.  Front Pointer: the end of the current red ball partitions
2.  Middle Pointer: the end of the current white ball partition
3.  End Pointer: the start of the current blue ball partition

NOTE: Sometimes the a white ball will be swapped from the front pointer to the middle, when this happens during the next iteration, you will increment the middle pointer because it is in the correct place. This took me a while to fully understand.

```python
def dutch_flag(balls):
    front_pointer = 0
    middle_pointer = 0
    end_pointer = len(balls) - 1

    while middle_pointer <= end_pointer:
        if balls[middle_pointer] == 'Red':
            balls[front_pointer], balls[middle_pointer] = balls[middle_pointer], balls[front_pointer]
            front_pointer += 1
            middle_pointer += 1
        elif balls[middle_pointer] == 'Blue':
            balls[end_pointer], balls[middle_pointer] = balls[middle_pointer], balls[end_pointer]
            end_pointer -= 1
        else: # White ball
            middle_pointer += 1
```
