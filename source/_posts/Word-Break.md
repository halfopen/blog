title: Word Break
author: Halfopen
tags:
  - dp
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-09-17 22:34:00
---
### [139\. Word Break](https://leetcode.com/problems/word-break/description/)

Difficulty: **Medium**



Given a **non-empty** string _s_ and a dictionary _wordDict_ containing a list of **non-empty** words, determine if _s_ can be segmented into a space-separated sequence of one or more dictionary words.

**Note:**

*   The same word in the dictionary may be reused multiple times in the segmentation.
*   You may assume the dictionary does not contain duplicate words.

**Example 1:**

```
**Input:** s = "leetcode", wordDict = ["leet", "code"]
**Output:** true
**Explanation:** Return true because `"leetcode"` can be segmented as `"leet code"`.
```

**Example 2:**

```
**Input:** s = "applepenapple", wordDict = ["apple", "pen"]
**Output:** true
**Explanation:** Return true because `"`applepenapple`"` can be segmented as `"`apple pen apple`"`.
             Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```
**Input:** s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
**Output:** false
```



#### Solution

Language: **Java**

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        // dp[i]表示0-i可以切分
        boolean[] dp = new boolean[s.length()+1];
        //　初始化
        dp[0] = true;
        for(int i=1;i<=s.length();++i){
            for(int j=0;j<i;++j){
                // 如果0-j已经正常切分，并且j-i也是一个单词，那么 0-i可以切分
                if(dp[j] && wordDict.contains(s.substring(j, i))){
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.length()];
        
    }
}
```