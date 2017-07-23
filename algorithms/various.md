# Various
## Union-Find
We need efficient support for 2 operations on a set of N objects:
- Union command: connect 2 objects
- Connected query: is there a path connecting 2 objects?

### Quick Find
Implement it as an array whose entries represent the group the item belongs to.

- Union: replaces all occurencies of the second group with the firs
- Find: checks if the two elements belong to the same group

### Quick Union
The entries are represented as a forest of trees, in which all the elements of a tree are.

We represent the forest as an array whose entries are the parent of the element in the tree. Root nodes will have themselves as parents.

- find: check if the 2 elements have the same root
- union: set one element's parent to the other element's root

#### Improvements
- weighting: always connect the smallest tree to the root of the tallest
- flattening the tree

### Applications
