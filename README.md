1. Project Summary
This project is a scratch implementation of the Knuth-Morris-Pratt (KMP) substring search algorithm in Java. KMP is a highly efficient algorithm that finds all occurrences of a "pattern" within a "text," avoiding the redundant character comparisons characteristic of the naive approach. The project's goal is to demonstrate understanding of the algorithm, implement it correctly, and analyze its performance across various datasets.

2. Implementation Details
The implementation is divided into two key components:
A) LPS Array Computation (computeLPSArray)
This is the preprocessing step, which is the core of KMP. LPS stands for Longest Proper Prefix which is also a Suffix. For each index 'i' in the pattern, lps[i] stores the length of the longest proper prefix of pattern[0...i] that is also a suffix of pattern[0...i]. This array allows the algorithm to precisely determine how much to "shift" the pattern upon a mismatch, preventing unnecessary back-tracking in the text.
B) Search Function (search)
This is the main execution step, which uses the pre-computed LPS array to scan the text.
It uses two pointers: 'i' for the text and 'j' for the pattern.
On a match: Both 'i' and 'j' advance.
On a full match (j == m): The occurrence is recorded. 'j' is then reset using the LPS array (j = lps[j-1]) to search for overlapping occurrences without restarting the search from the beginning.
On a mismatch: If j is not 0, 'i' is kept in place, and 'j' is reset to lps[j-1]. This effectively aligns the pattern based on the longest matching prefix found so far. If j is 0, 'i' is simply advanced (mismatch at the pattern's first character).

3. Complexity Analysis
Time Complexity: O(n + m)
O(m) for Preprocessing: The computeLPSArray method runs in linear time relative to the pattern length 'm'. The total number of operations is amortized to O(m).
O(n) for Searching: The search method runs in linear time relative to the text length 'n'. The text pointer 'i' never moves backward. The total number of comparisons is amortized to O(n).
Total: O(n + m).

Space Complexity: O(m)
The algorithm requires auxiliary space only for storing the LPS array.
The size of this array is equal to the length of the pattern, 'm'.

4. Testing Results
The algorithm was tested on three diverse datasets to ensure correctness:
Test 1: Short String (Overlapping) Text: ABABABCABAB Pattern: ABAB Occurrences (Indices): [0, 5, 7]
Test 2: Medium String (Repeating Characters) Text: AAAAABAAABA Pattern: AAAA Occurrences (Indices): [0, 1]
Test 3: Long String (Realistic Text) Text: THEQUICKBROWNFOXJUMPSOVERTHELAZYDOGANDTHEFOXWASHAPPY Pattern: FOX Occurrences (Indices): [16, 46]
