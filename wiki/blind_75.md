# Blind 75
Spreadsheet: https://docs.google.com/spreadsheets/d/1A2PaQKcdwO_lwxz9bAnxXnIQayCouZP6d-ENrBz_NXc/edit#gid=0
YT Playlist: https://www.youtube.com/playlist?list=PLot-Xpze53ldVwtstag2TL4HQhAnC8ATf

* [✓] [Two Sum](https://leetcode.com/problems/two-sum/)
    * Hash map of num -> array idx. look up (total - num) as key.

* [✓] [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
    * Iterate through array, at each element take difference of current price and the min of elements to the left. 
    * Max of differences is highest profit.

* [✓] [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
    * Use a set and check for element membership in set as you iterate through the array.

* [✓] [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
    * Use a prefix and suffix product array

* [✓] [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
    * Track the local max = max(element, total + element), and the global_max = max(global_max, local_max) 

* [✓] [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
    * Similar to Kadane's algo, options at each element are max([x, x * min_product_so_far, x * max_product_so_far])

* [✓] [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
    * One half of the array is always sorted, search the non-sorted half 

* [✓] [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
    * One half of the array is always sorted. If the target is in the sorted range, look there, else look at the other half.

* [✓] [3Sum](https://leetcode.com/problems/3sum/)
    * Sort the list, for each element, run sorted 2Sum (left right pointer approach) against the remainder of the array. Move pointers forward such that they don't point to duplicates.

* [✓] [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
    * Initialize left, right pointers. Compute width * min_height as area. Track max area. Move the pointer that points to the min height.

* [✗] Sum of Two Integers
* [✓] Number of 1 Bits
    * O(n) - mask the least significant bit to check if it's a 1. Increment a counter. Shift right.
    * O(p) [p is the number of 1 bits] - x & (x - 1) will set the least sigificant 1 to 0. Do this until x == 0.

* [✗] Counting Bits
* [✗] Missing Number
* [✗] Reverse Bits

* [✓] Climbing Stairs
    * Fibonacci memoization. Base cases for 1 jump and 2 jumps, build up to n by taking jump_1 + jump_2. then jump_1 becomes the new result, jump_2 becomes old jump_1.

* [✓] Coin Change
    * Initialize array of len amount as the memo array. All entries except 0 initialize to MAX_INT. Iterate through range(0, amount + 1), for each iteration take the min of idx - each denom.

* [✓] Longest Increasing Subsequence
    * DP. At each idx, we either append to the longest preceding subsequence, or start a new one of length 1.
    * Keep a memo array of LIS up until index i. For each subsequent index idx, the LIS is the max of LIS at all previous LIS's for which nums[idx] is greater (or 1 if there are none).

* [✓] Longest Common Subsequence
    * 2D DP. If grid[i] == grid[j] increment lcs of grid[i - 1][j - 1], else take max of grid[i-1][j] or grid[i][j-1]

* [✓] Word Break Problem
    * Top down DP. Iterate through idxs of input word, check if the prefix substring is a word in the dict, recursively check if the rest of the string can be segmented. Check the memo cache before recursing.

* [✓] Combination Sum
    * Backtracking + dfs. Keep track of the path. In order to remove duplicates, reduce the candidates list to only include candidates to the right ([inclusive](inclusive)) of the current path node

* [✓] House Robber
    * DP - At each index, take max of results[idx - 1] or results[idx - 2] + result[idx]

* [✓] House Robber II
    * Run House Robber I on slice nums[:-1] and nums[1:]

* [✓] Decode Ways
    * Top down DP - Decode first character and possibly second character, recurse on the rest
    * Cache intermediate results in memo dict

* [✓] Unique Paths
    * DP grid. Sum adjacent cells.

* [✓] Jump Game
    * Greedy / DP. Iterate backwards from the end of array, track the nearest index that can get you to the end. If nums[idx] + idx > nearest_jump_idx, idx can reach the end.
 
* [✗] Clone Graph
* [✗] Course Schedule
* [✗] Pacific Atlantic Water Flow
* [✗] Number of Islands

* [✓] Longest Consecutive Sequence
    * Convert input to a set. Pop an element from set, sequence len = 1 + longest increasing(num_set, num + 1) + longest decreasing(num_set, num - 1). Helper functions should also consume the set elements.

* [✗] Alien Dictionary (Leetcode Premium)
* [✗] Graph Valid Tree (Leetcode Premium)
* [✗] Number of Connected Components in an Undirected Graph (Leetcode Premium)
* [✗] Insert Interval
* [✓] Merge Intervals
    * Sort intervals, then merge by comparing previous interval end against current interval beginning.

* [✗] Non-overlapping Intervals
* [✗] Meeting Rooms (Leetcode Premium)
* [✗] Meeting Rooms II (Leetcode Premium)

* [✗] Reverse a Linked List
    * Iterative: push nodes onto stack until end of LL. Pop nodes one by one and set their next pointer to the node at the top of the stack.
    * Recursive: set the next pointer for the next node to the current node recursively. Note that this should be done after the recursive call.

* [✗] Detect Cycle in a Linked List
* [✗] Merge Two Sorted Lists
* [✗] Merge K Sorted Lists
* [✗] Remove Nth Node From End Of List
* [✗] Reorder List
* [✗] Set Matrix Zeroes

* [✓] Spiral Matrix
    * Use left, right, top, bottom bounding indices. Continue until a bound is crossed, then change direction. Tighten the bounding box when a full round (4 turns) have been made.
  
* [✓] Rotate Image
    * Draw a matrix diagram
    * Rotate layer by layer with a layer min and max.
    * Rotate each side of the square from i in [min, max) (note that the corners belong to two sides, so the interval is half open)

* [✗] Word Search
* [✗] Longest Substring Without Repeating Characters
* [✗] Longest Repeating Character Replacement
* [✗] Minimum Window Substring

* [✓] Valid Anagram
    * Compare counters of both strings using two dicts. Dict lengths, keys and values should match.
    * Can do it with one dict. Convert first word to a dict, for second word, decrement counter for each character. Check that dict is empty at the end.
    * O(n logn) - Sort and compare both strings and compare for exact match.

* [✗] Group Anagrams
* [✓] Valid Parentheses
* [✗] Valid Palindrome
* [✗] Longest Palindromic Substring
* [✗] Palindromic Substrings
* [✗] Encode and Decode Strings (Leetcode Premium)
* [✗] Maximum Depth of Binary Tree

* [✓] Same Tree
    * Iterate over nodes recursively, compare node data, check that both nodes have the same shape

* [✓] Invert/Flip Binary Tree
    * Recursively call node.right = invert(node.left) and node.left = invert(node.right) 

* [✗] Binary Tree Maximum Path Sum

* [✓] Binary Tree Level Order Traversal
    * #1: Use BFS and recursively pass the tree level in each call. Keep a list / mapping of level -> node items in the level
    * #2: Use BFS and 2 queues, one processes nodes at the current level and the next processes child nodes. The queues switch once a level has been traversed.

* [✓] Serialize and Deserialize Binary Tree
    * Serialize: Use a preorder traversal and markers for null left or right nodes
    * Deserialize: Keep traversing and appending nodes to the left until you hit a null marker, at which point keep pointing at parent nodes until a non null is found and append that node to the right. Continue the process until the end of the string.

* [✗] Subtree of Another Tree
* [✗] Construct Binary Tree from Preorder and Inorder Traversal
* [✗] Validate Binary Search Tree
* [✗] Kth Smallest Element in a BST

* [✓] Lowest Common Ancestor of BST
    * BST DFS path to both nodes. Iterate through paths until they diverge. If they dont' diverge, return last element of shorter path.

* [✓] Implement Trie (Prefix Tree)
    * Use a dictionary of character -> TrieNode on each TrieNode
    * Keep a boolean flag on each node to indicate whether the node is a word or not

* [✗] Add and Search Word
* [✗] Word Search II

* [✓] Top K Frequent Elements
    * Map frequencies to elements
    * Use quickselect or heap extraction to get top k frequencies
    * Get the corresponding elements for each frequency

* [✗] Find Median from Data Stream



https://leetcode.com/problems/sum-of-two-integers/
https://leetcode.com/problems/number-of-1-bits/
https://leetcode.com/problems/counting-bits/
https://leetcode.com/problems/missing-number/
https://leetcode.com/problems/reverse-bits/
https://leetcode.com/problems/climbing-stairs/
https://leetcode.com/problems/coin-change/
https://leetcode.com/problems/longest-increasing-subsequence/
https://leetcode.com/problems/longest-common-subsequence/
https://leetcode.com/problems/word-break/
https://leetcode.com/problems/combination-sum/
https://leetcode.com/problems/house-robber/
https://leetcode.com/problems/house-robber-ii/
https://leetcode.com/problems/decode-ways/
https://leetcode.com/problems/unique-paths/
https://leetcode.com/problems/jump-game/
https://leetcode.com/problems/clone-graph/
https://leetcode.com/problems/course-schedule/
https://leetcode.com/problems/pacific-atlantic-water-flow/
https://leetcode.com/problems/number-of-islands/
https://leetcode.com/problems/longest-consecutive-sequence/
https://leetcode.com/problems/alien-dictionary/
https://leetcode.com/problems/graph-valid-tree/
https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/
https://leetcode.com/problems/insert-interval/
https://leetcode.com/problems/merge-intervals/
https://leetcode.com/problems/non-overlapping-intervals/
https://leetcode.com/problems/meeting-rooms/
https://leetcode.com/problems/meeting-rooms-ii/
https://leetcode.com/problems/reverse-linked-list/
https://leetcode.com/problems/linked-list-cycle/
https://leetcode.com/problems/merge-two-sorted-lists/
https://leetcode.com/problems/merge-k-sorted-lists/
https://leetcode.com/problems/remove-nth-node-from-end-of-list/
https://leetcode.com/problems/reorder-list/
https://leetcode.com/problems/set-matrix-zeroes/
https://leetcode.com/problems/spiral-matrix/
https://leetcode.com/problems/rotate-image/
https://leetcode.com/problems/word-search/
https://leetcode.com/problems/longest-substring-without-repeating-characters/
https://leetcode.com/problems/longest-repeating-character-replacement/
https://leetcode.com/problems/minimum-window-substring/
https://leetcode.com/problems/valid-anagram/
https://leetcode.com/problems/group-anagrams/
https://leetcode.com/problems/valid-parentheses/
https://leetcode.com/problems/valid-palindrome/
https://leetcode.com/problems/longest-palindromic-substring/
https://leetcode.com/problems/palindromic-substrings/
https://leetcode.com/problems/encode-and-decode-strings/
https://leetcode.com/problems/maximum-depth-of-binary-tree/
https://leetcode.com/problems/same-tree/
https://leetcode.com/problems/invert-binary-tree/
https://leetcode.com/problems/binary-tree-maximum-path-sum/
https://leetcode.com/problems/binary-tree-level-order-traversal/
https://leetcode.com/problems/serialize-and-deserialize-binary-tree/
https://leetcode.com/problems/subtree-of-another-tree/
https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/
https://leetcode.com/problems/validate-binary-search-tree/
https://leetcode.com/problems/kth-smallest-element-in-a-bst/
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/
https://leetcode.com/problems/implement-trie-prefix-tree/
https://leetcode.com/problems/add-and-search-word-data-structure-design/
https://leetcode.com/problems/word-search-ii/
https://leetcode.com/problems/merge-k-sorted-lists/
https://leetcode.com/problems/top-k-frequent-elements/
https://leetcode.com/problems/find-median-from-data-stream/
