# DAY_9-Nth-Digit

Find the Nth Digit (Java)
This repository contains a Java solution to the LeetCode problem "400. Nth Digit", which involves finding the n-th digit in the infinite sequence of integers concatenated together: 123456789101112....

Problem Statement
Given an integer n, return the n-th digit of the sequence formed by concatenating all the positive integers.

Example:
Input: n = 11
Output: 0
Explanation: The 11th digit in the sequence is '0' (from number 10).

Approach
The core idea is to skip over entire blocks of digits (1-digit numbers, 2-digit numbers, etc.) until we find the block that contains the n-th digit.

Key Steps:
Block Skipping:

1-digit numbers: 1–9 → 9 digits

2-digit numbers: 10–99 → 90×2 = 180 digits

3-digit numbers: 100–999 → 900×3 = 2700 digits
(and so on)

Find the exact number that contains the n-th digit once the correct block is found.

Extract the digit from that number using string indexing.

Code Overview
java
Copy
Edit
public int findNthDigit(int n)
Parameters:

n: The position (1-based index) of the digit in the infinite sequence.

Returns:

The integer value of the digit at the n-th position.

Time and Space Complexity
Time Complexity: O(log n)
Efficiently skips entire digit blocks.

Space Complexity: O(1)
Uses constant space aside from string conversion for a single number.



class Solution {
    public int findNthDigit(int n) {
        long digitInNum = 1, start = 1, end = 9;

        // Skip over blocks of digits until we find the right block
        while (n > digitInNum * end) {
            n -= digitInNum * end;  // Remove this block from n
            digitInNum++;            // Move to the next block (more digits)
            start *= 10;             // Start of the next block
            end *= 10;               // End of the next block
        }

        long num = start + (n - 1) / digitInNum;  // Find the exact number
        String numStr = Long.toString(num);       // Convert number to string
        return numStr.charAt((n - 1) % (int) digitInNum) - '0';  // Get the nth digit
    }
}
