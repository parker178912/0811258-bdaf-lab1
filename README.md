# 0811258_bdaf_lab1
* In this assignment, you are tasked with writing a Python function that will generate a Merkle proof.

## Code explain :

### Function
```python=
    for level in range(height):
        #######  YOUR CODE GOES HERE                              ######
        #######     to hash internal nodes in the tree use the    ######
        #######     function hash_internal_node(left,right)       ######

        # If the position is even, then its sibling is on the right.
        if level_pos % 2 == 0:
            sibling = state[level_pos+1]
        # Otherwise, its sibling on the left.
        else:
            sibling = state[level_pos-1]

        # Add the sibling hash to the path.
        path.append(sibling)

        # Get parents from two children and append it to new state 
        # and get next level states.
        new_state = []
        for i in range(0, len(state), 2):
            new_state.append(hash_internal_node(state[i], state[i+1]))
        state = new_state

        # Update the position for the next level.
        level_pos = level_pos // 2

    # return a list of hashes that makes up the Merkle proof
    return path
```
* Explain for the sibling：
    When the position of the state are even (Ex: hABCD), then its sibling is on the right side (hEFGH) and the position is state+1 ; Otherwise, take hCD for example, the position of hCD is odd so its sibling is on the left side (hAB).
    
![](https://i.imgur.com/kb94UQr.png)
( source : [Merkle Tree 和 Merkle Root 介紹](https://academy.binance.com/zt/articles/merkle-trees-and-merkle-roots-explained) )
