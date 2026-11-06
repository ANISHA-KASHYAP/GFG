## 01. Distinct Permutations of String

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/permutations-of-a-given-string2041/1?utm_source=chatgpt.com)

### Problem Description

**Task:** Given a string s, which may contain duplicate characters, generate all possible unique permutations of the string.Note: You may return the permutations in any order.Examples:Input: s = "ABC"

#### Examples

##### Example 1

- **Output:**
```text
["ABC", "ACB", "BAC", "BCA", "CAB", "CBA"]
```
- **Explanation:** Given string ABC has 6 unique permutations.

##### Example 2

- **Input:**
```text
s = "ABSG"
```
- **Output:**
```text
["ABGS", "ABSG", "AGBS", "AGSB", "ASBG", "ASGB", "BAGS", "BASG", "BGAS", "BGSA", "BSAG", "BSGA", "GABS", "GASB", "GBAS", "GBSA", "GSAB", "GSBA", "SABG", "SAGB", "SBAG", "SBGA", "SGAB", "SGBA"]
```
- **Explanation:** Given string ABSG has 24 unique permutations.

##### Example 3

- **Input:**
```text
s = "AAA"
```
- **Output:**
```text
["AAA"]Explanation: No other unique permutations can be formed as all the characters are same.
```

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n! * n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-11-06 14:12:20
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:

    // Recursive function to generate permutations
    void solve(string &s, vector<int>& visited,
               string &temp, vector<string>& ans) {

        // BASE CASE:
        // If temp contains all characters,
        // one complete permutation is ready.
        if(temp.size() == s.size()) {
            ans.push_back(temp);
            return;
        }

        // Try every character
        for(int i = 0; i < s.size(); i++) {

            // If character is already used, skip it
            if(visited[i] == 1) {
                continue;
            }

            // Skip duplicate characters
            if(i > 0 && s[i] == s[i-1] && visited[i-1] == 0) {
                continue;
            }

            // STEP 1: CHOOSE
            // Mark current character as used
            visited[i] = 1;

            // Add character to temporary string
            temp.push_back(s[i]);

            // STEP 2: EXPLORE
            // Generate remaining permutations
            solve(s, visited, temp, ans);

            // STEP 3: UNDO (BACKTRACKING)
            // Remove last character
            temp.pop_back();

            // Mark character as unused
            visited[i] = 0;
        }
    }

    // Main function
    vector<string> findPermutation(string &s) {

        vector<string> ans;

        // Initially no character is used
        vector<int> visited(s.size(), 0);

        // Stores current permutation
        string temp = "";

        // Sort to bring duplicate characters together
        sort(s.begin(), s.end());

        // Start recursion
        solve(s, visited, temp, ans);

        return ans;
    }
};
```

*Generated on: 11/6/2026, 12:38:59 PM*