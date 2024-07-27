# LEETCODE-Strings-2976
Sure, let's walk through the code step-by-step to understand how it works and then perform a dry run with an example.

## Step-by-Step Explanation

### Initial Setup
1. **Initialization**:
   - `ans` is initialized to 0 to store the total minimum cost.
   - `dist` is a 2D array to store the minimum cost to change each character 'a' to 'z' to another character 'a' to 'z'. It's initialized to `Long.MAX_VALUE` to represent infinite cost initially.

2. **Populate `dist` with Given Costs**:
   - For each transformation provided in the `original` and `changed` arrays along with their respective costs, update the `dist` array with the minimum cost for that transformation.

### Floyd-Warshall Algorithm
3. **Floyd-Warshall Algorithm**:
   - This is used to find the shortest paths between all pairs of characters. It updates the `dist` array to ensure that the minimum cost for transforming any character to any other character is computed.

### Compute Total Cost
4. **Calculate the Cost to Transform `source` to `target`**:
   - For each character in the `source` string, check if it matches the corresponding character in the `target` string. If they match, no cost is added.
   - If they don't match, check the cost in the `dist` array. If the cost is `Long.MAX_VALUE`, it means the transformation is impossible, and the function returns -1.
   - Otherwise, add the transformation cost to `ans`.

### Return the Result
5. **Return the Total Cost**:
   - Return the total minimum cost stored in `ans`.

## Dry Run Example

Let's take an example to dry run the function:
- `source = "abc"`
- `target = "bca"`
- `original = ['a', 'b', 'c']`
- `changed = ['b', 'c', 'a']`
- `cost = [1, 1, 1]`

### Initial Setup
1. Initialize `dist` to `Long.MAX_VALUE` for all pairs.
2. Populate `dist` with the given costs:
   - `dist[0][1] = 1` (cost to change 'a' to 'b')
   - `dist[1][2] = 1` (cost to change 'b' to 'c')
   - `dist[2][0] = 1` (cost to change 'c' to 'a')

### Floyd-Warshall Algorithm
3. Update `dist` using the Floyd-Warshall algorithm. The relevant updates would be:
   - `dist[0][2] = dist[0][1] + dist[1][2] = 1 + 1 = 2` (cost to change 'a' to 'c' through 'b')
   - `dist[1][0] = dist[1][2] + dist[2][0] = 1 + 1 = 2` (cost to change 'b' to 'a' through 'c')
   - `dist[2][1] = dist[2][0] + dist[0][1] = 1 + 1 = 2` (cost to change 'c' to 'b' through 'a')

### Compute Total Cost
4. Calculate the cost to transform `source` to `target`:
   - `source[0] = 'a'`, `target[0] = 'b'`: cost is `dist[0][1] = 1`, so `ans = 1`
   - `source[1] = 'b'`, `target[1] = 'c'`: cost is `dist[1][2] = 1`, so `ans = 2`
   - `source[2] = 'c'`, `target[2] = 'a'`: cost is `dist[2][0] = 1`, so `ans = 3`

### Return the Result
5. Return `ans`, which is 3.

This dry run confirms that the function correctly calculates the minimum cost to transform `source` to `target` using the given transformation rules and costs.
