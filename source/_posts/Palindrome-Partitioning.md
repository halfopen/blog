title: Palindrome Partitioning
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-09-14 19:46:00
---
### [131\. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/description/)

Difficulty: **Medium**



Given a string _s_, partition _s_ such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of _s_.

**Example:**

```
**Input:** "aab"
**Output:**
[
  ["aa","b"],
  ["a","a","b"]
]
```

在每一步都可以判断中间结果是否为合法结果，用回溯法。
一个长度为 n 的字符串，有 n − 1 个地方可以砍断，每个地方可断可不断，因此复杂度为
O(2n−1)

abc其实只有两个地方可以选择　a|b|c，但是在结束的时候，要单独考虑，把后面的结果加进去


#### Solution

Language: **Java**

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new LinkedList<>();
        // 先输出所有划分
        dfs(s, 0, "", new LinkedList<String>(), result);
        return result;
    }
    
    public void dfs(String s, int pos, String tmps, LinkedList<String> tmpl, List<List<String>>result){
        char c = s.charAt(pos);
        //System.out.println(c+" "+pos+" "+tmps+ " "+tmpl.size());
        if(pos>=s.length()-1){
            if(tmps.length()==0){
                // tmpl.addLast(tmps);
                tmpl.addLast(""+c);
            }
            else{
                if(!isPalindrome(tmps+c))return;
                tmpl.addLast(tmps+c);
            }
            result.add(new LinkedList<String>(tmpl));
            return ;
        };
​
​
        // 断开,把tmps+c加入tmpl, tmps清空
        tmpl.addLast(tmps+c);
        // 如果tmps+c是回文
        if(isPalindrome(tmps+c))dfs(s, pos+1, "", new LinkedList<String>(tmpl), result);
        tmpl.removeLast();
       // 不断开，把c加入tmps
        dfs(s, pos+1, tmps+c, new LinkedList<String>(tmpl), result);
        
    }
    
    public boolean isPalindrome(String str){
        int s = 0, e=str.length()-1;
        while(s<e){
            if(str.charAt(s)!=str.charAt(e))return false;
            s++;
            e--;
        }
        return true;
    }
}
```