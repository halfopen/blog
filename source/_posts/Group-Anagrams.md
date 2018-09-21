title: Group Anagrams
author: Halfopen
date: 2018-09-20 21:44:50
tags:
---
### [49\. Group Anagrams](https://leetcode.com/problems/group-anagrams/description/)

Difficulty: **Medium**



Given an array of strings, group anagrams together.

**Example:**

```
**Input:** `["eat", "tea", "tan", "ate", "nat", "bat"]`,
**Output:**
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]```

**Note:**

*   All inputs will be in lowercase.
*   The order of your output does not matter.



#### Solution

Language: **Java**

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> ret = new ArrayList<>();
        HashMap<String, List<String>> map = new HashMap<>();
        
        for(String s:strs){
            String k = hash2(s);
            List<String> l = null;
            // 一个经典的写法
            map.computeIfAbsent(k, (k)->new ArrayList()).add(s);
            // if(!map.containsKey(k)){
            //     l = new ArrayList<>();
            //     l.add(s);
            //     map.put(k, l);
            // }else{
            //     l = map.get(k);
            //     l.add(s);
            // }
            
        }
        
        for(Map.Entry<String, List<String>> e:map.entrySet()){
            ret.add(e.getValue());
        }
        return ret;
    }
    
    public String hash(String s){
        char[] ca = s.toCharArray();
        Arrays.sort(ca);
        return new String(ca);
    }
    // 可以用hash方法，统计每个字符出现的字数
    String hash2(String s){
        int[] a = new int[26];
        for(char c : s.toCharArray()) a[c-'a']++;
        return Arrays.toString(a);
    }
}
```