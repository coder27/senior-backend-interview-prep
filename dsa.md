# DSA problems, by pattern

60 problems across 15 patterns. These are real, well-known problems — solve them on LeetCode itself (its judge and test cases do this better than any homegrown tool would). The one-line note next to each is a pattern hint, not a full spec.

A ⭐ marks a problem that may require LeetCode Premium.


## Arrays & Two Pointers

| Problem | Difficulty | Hint |
|---|---|---|
| [Two Sum](https://leetcode.com/problems/two-sum/) | medium | Given an array of integers and a target, return the indices of the two numbers that add up to the target. Aim for better than O(n^2). |
| [3Sum](https://leetcode.com/problems/3sum/) | medium | Given an array of integers, find all unique triplets that sum to zero. Discuss how sorting enables an O(n^2) two-pointer approach. |
| [Container With Most Water](https://leetcode.com/problems/container-with-most-water/) | medium | Given an array of heights representing vertical lines, find two lines that together with the x-axis form the container holding the most water. |
| [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) | hard | Given an elevation map, compute how much water it can trap after raining. Discuss the two-pointer approach vs. precomputed max-left/max-right arrays. |

## Sliding Window

| Problem | Difficulty | Hint |
|---|---|---|
| [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | medium | Given a string, find the length of the longest substring without repeating characters, using a sliding window with a character-index map. |
| [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) | hard | Given strings s and t, find the smallest substring of s that contains every character of t (with duplicates). Classic variable-size sliding window. |
| [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/) | medium | Given a string and a number k, find the length of the longest substring you can make of a single repeated character by replacing at most k characters. |
| [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/) | hard | Given an array and window size k, return the maximum of every window as it slides. Discuss the monotonic deque approach for O(n). |

## Binary Search

| Problem | Difficulty | Hint |
|---|---|---|
| [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) | medium | Given a sorted array rotated at an unknown pivot, search for a target in O(log n) without knowing the pivot ahead of time. |
| [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) | medium | Given a rotated sorted array with unique elements, find the minimum element in O(log n). |
| [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) | hard | Given two sorted arrays, find the median of the combined array in O(log(min(m,n))) using a binary-search-on-partitions approach. |
| [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) | medium | Given piles of bananas and h hours, find the minimum eating speed k such that Koko can finish all piles within h hours — binary search on the answer. |

## Linked Lists

| Problem | Difficulty | Hint |
|---|---|---|
| [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) | medium | Reverse a singly linked list, iteratively and then discuss the recursive version. |
| [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) | hard | Merge k sorted linked lists into one sorted list. Compare a heap-based approach to divide-and-conquer merging. |
| [Detect Cycle in a Linked List](https://leetcode.com/problems/linked-list-cycle-ii/) | medium | Detect whether a linked list has a cycle, and if so, find the node where the cycle begins, using Floyd's cycle detection. |
| [LRU Cache](https://leetcode.com/problems/lru-cache/) | medium | Design an LRU cache with O(1) get and put, using a hash map plus a doubly linked list. |

## Stacks & Queues

| Problem | Difficulty | Hint |
|---|---|---|
| [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) | medium | Given a string of brackets, determine whether every open bracket is closed by the same type in the correct order, using a stack. |
| [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) | medium | Given daily temperatures, for each day find how many days until a warmer temperature, using a monotonic stack. |
| [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/) | hard | Given bar heights of a histogram, find the area of the largest rectangle, using a monotonic stack of indices. |
| [Min Stack](https://leetcode.com/problems/min-stack/) | medium | Design a stack that supports push, pop, top, and retrieving the minimum element, all in O(1). |

## Trees & BSTs

| Problem | Difficulty | Hint |
|---|---|---|
| [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) | medium | Given a binary tree, determine whether it is a valid binary search tree, being careful about the full-subtree bound, not just immediate children. |
| [Lowest Common Ancestor of a BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) | medium | Given a BST and two nodes, find their lowest common ancestor, using the BST ordering property. |
| [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) | hard | Design an algorithm to serialize a binary tree to a string and deserialize it back to the original tree structure. |
| [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) | hard | Given a binary tree, find the maximum path sum where a path can start and end at any node, not necessarily through the root. |

## Heaps & Priority Queues

| Problem | Difficulty | Hint |
|---|---|---|
| [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) | medium | Find the kth largest element in an unsorted array. Discuss heap vs. quickselect trade-offs. |
| [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) | medium | Given an array, return the k most frequent elements using a heap or bucket-sort approach. |
| [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/) | hard | Design a structure that supports adding numbers one at a time and finding the median so far, using two heaps. |
| [Task Scheduler](https://leetcode.com/problems/task-scheduler/) | medium | Given tasks and a cooldown period between identical tasks, find the minimum time to finish all tasks, using a max-heap of task counts. |

## Graphs (BFS/DFS)

| Problem | Difficulty | Hint |
|---|---|---|
| [Number of Islands](https://leetcode.com/problems/number-of-islands/) | medium | Given a grid of land and water, count the number of islands (connected components of land), using BFS or DFS. |
| [Course Schedule](https://leetcode.com/problems/course-schedule/) | medium | Given courses with prerequisites, determine whether it's possible to finish all courses — cycle detection in a directed graph via topological sort. |
| [Clone Graph](https://leetcode.com/problems/clone-graph/) | medium | Given a reference to a node in a connected undirected graph, return a deep copy of the graph. |
| [Word Ladder](https://leetcode.com/problems/word-ladder/) | hard | Given a start word, end word, and a dictionary, find the length of the shortest transformation sequence changing one letter at a time, using BFS. |

## Backtracking

| Problem | Difficulty | Hint |
|---|---|---|
| [Subsets](https://leetcode.com/problems/subsets/) | medium | Given a set of distinct integers, return all possible subsets (the power set), using backtracking. |
| [Permutations](https://leetcode.com/problems/permutations/) | medium | Given an array of distinct integers, return all possible permutations, using backtracking with a used-elements set. |
| [N-Queens](https://leetcode.com/problems/n-queens/) | hard | Place n queens on an n x n board so that no two attack each other; return all distinct solutions, using backtracking with column/diagonal tracking. |
| [Word Search](https://leetcode.com/problems/word-search/) | medium | Given a 2D grid of letters and a word, determine if the word can be constructed from adjacent cells (no reuse), using backtracking DFS. |

## Dynamic Programming

| Problem | Difficulty | Hint |
|---|---|---|
| [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) | medium | Given an array of integers, find the length of the longest strictly increasing subsequence. Discuss O(n^2) DP vs. O(n log n) with binary search. |
| [Coin Change](https://leetcode.com/problems/coin-change/) | medium | Given coin denominations and a target amount, find the fewest coins needed to make that amount, or -1 if impossible. |
| [Edit Distance](https://leetcode.com/problems/edit-distance/) | hard | Given two strings, find the minimum number of insert/delete/replace operations to convert one into the other. |
| [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/) | medium | Given two strings, find the length of their longest common subsequence using a 2D DP table. |

## Greedy

| Problem | Difficulty | Hint |
|---|---|---|
| [Jump Game](https://leetcode.com/problems/jump-game/) | medium | Given an array where each element is the max jump length from that position, determine if you can reach the last index, using a greedy reachable-max approach. |
| [Gas Station](https://leetcode.com/problems/gas-station/) | medium | Given gas and cost arrays for a circular route, find the starting station index that lets you complete the circuit, or -1 if impossible. |
| [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) | medium | Given a set of intervals, find the minimum number to remove so the rest don't overlap, using a greedy sort-by-end-time approach. |
| [Partition Labels](https://leetcode.com/problems/partition-labels/) | medium | Given a string, partition it into as many parts as possible so each letter appears in at most one part, using greedy last-occurrence tracking. |

## Intervals

| Problem | Difficulty | Hint |
|---|---|---|
| [Merge Intervals](https://leetcode.com/problems/merge-intervals/) | medium | Given a collection of intervals, merge all overlapping intervals after sorting by start time. |
| [Insert Interval](https://leetcode.com/problems/insert-interval/) | medium | Given a set of non-overlapping sorted intervals and a new interval, insert it and merge as needed. |
| [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) ⭐ | medium | Given meeting time intervals, find the minimum number of conference rooms required, using a min-heap of end times. |
| [Employee Free Time](https://leetcode.com/problems/employee-free-time/) ⭐ | hard | Given schedules for multiple employees as lists of intervals, find the common free time across all of them. |

## Tries

| Problem | Difficulty | Hint |
|---|---|---|
| [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/) | medium | Implement a trie supporting insert, search, and startsWith operations. |
| [Word Search II](https://leetcode.com/problems/word-search-ii/) | hard | Given a 2D board and a list of words, find all words present on the board, using a trie combined with backtracking for efficiency. |
| [Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/) | medium | Design a data structure supporting adding words and searching with '.' as a wildcard for any single character, using a trie. |
| [Replace Words](https://leetcode.com/problems/replace-words/) | medium | Given a dictionary of roots and a sentence, replace each word with its shortest matching root, using a trie. |

## Union-Find (Disjoint Set)

| Problem | Difficulty | Hint |
|---|---|---|
| [Number of Provinces](https://leetcode.com/problems/number-of-provinces/) | medium | Given a matrix indicating direct connections between cities, find the number of provinces (connected groups), using union-find. |
| [Redundant Connection](https://leetcode.com/problems/redundant-connection/) | medium | Given a graph that was a tree with one extra edge added, find the edge that can be removed to make it a tree again, using union-find. |
| [Accounts Merge](https://leetcode.com/problems/accounts-merge/) | hard | Given accounts with names and emails, merge accounts that share at least one email, using union-find over email addresses. |
| [Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/) ⭐ | medium | Given n nodes and a list of edges, determine whether they form a valid tree (connected, no cycles), using union-find or BFS/DFS. |

## Bit Manipulation & Math

| Problem | Difficulty | Hint |
|---|---|---|
| [Single Number](https://leetcode.com/problems/single-number/) | medium | Given an array where every element appears twice except one, find that single element in O(n) time and O(1) space using XOR. |
| [Counting Bits](https://leetcode.com/problems/counting-bits/) | medium | Given n, return an array where each index i holds the count of set bits in i, using a DP relation on lower bits. |
| [Pow(x, n)](https://leetcode.com/problems/powx-n/) | medium | Implement pow(x, n) in O(log n) using fast exponentiation (exponentiation by squaring), handling negative n. |
| [Sqrt(x)](https://leetcode.com/problems/sqrtx/) | medium | Implement integer square root of a non-negative integer x without using a built-in power function, using binary search. |
