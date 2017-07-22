# Various
## Union-Find
We need efficient support for 2 operations on a set of N objects:
- Union command: connect 2 objects
- Connected query: is there a path connecting 2 objects?

### Quick Find
Implement it as an array whose entries represent the group the item belongs to.

- Union: replaces all occurencies of the second group with the first. `O(n)`
- Find: checks if the two elements belong to the same group. `O(1)`