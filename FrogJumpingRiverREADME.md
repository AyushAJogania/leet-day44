# leet-day44

# Frog Jumping River: Dynamic Programming Approach

## Problem Description

The problem is about a frog trying to cross a river by jumping on stones. The frog starts on the first stone and wants to reach the last stone. It can only jump a certain distance k (k-1, k, or k+1) forward to the next stone if the stone exists. The goal is to determine if the frog can reach the last stone.

## Intuition

The frog can reach the last stone if, for each stone, there exists a previous stone from which it can jump to the current stone with a distance of k-1, k, or k+1 units.

## Approach

To solve this problem, we can use a dynamic programming approach. We will maintain a dictionary (set) to store the stones where the frog can jump from. For each stone, we iterate through all the previous stones and check if the frog can jump from any of those to the current stone. If yes, we add the current stone to the set of reachable stones.

## Algorithm

1. Initialize a set `reachable` containing only the first stone (position 0).
2. Iterate through each stone starting from the second one (index 1):
   a. For each previous stone `prev` in the `reachable` set:
      - Calculate the difference `diff` between the current stone and the previous stone.
      - Check if `diff - 1`, `diff`, or `diff + 1` is present in the `reachable` set. If yes, add the current stone to the set.
3. Finally, check if the last stone (position `stones.back()`) is present in the `reachable` set. If yes, return `true`, else return `false`.

## Complexity Analysis

- Time complexity: O(n^2), where n is the number of stones.
- Space complexity: O(n), as we are using a set to store the reachable stones.

## How to Use

To use the solution, you can follow these steps:

1. Initialize an array `stones` with the positions of stones in ascending order.
2. Call the `canCross` function, passing the `stones` array as an argument.
3. The function will return `true` if the frog can cross the river or `false` otherwise.

## Example

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

bool canCross(std::vector<int>& stones) {
    std::unordered_set<int> reachable;
    reachable.insert(0);
    
    for (int i = 1; i < stones.size(); ++i) {
        reachable.insert(stones[i]);
    }
    
    for (int i = 1; i < stones.size(); ++i) {
        for (int prev : reachable) {
            int diff = stones[i] - prev;
            if (reachable.count(diff - 1) || reachable.count(diff) || reachable.count(diff + 1)) {
                reachable.insert(stones[i]);
                break;
            }
        }
    }
    
    return reachable.count(stones.back());
}

```

Remember to modify the `stones` array according to the test case you want to check.

This solution should help you determine if the frog can successfully cross the river or not by using a dynamic programming approach.
