title: Simplify Path
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-07-26 20:43:00
---
### [71\. Simplify Path](https://leetcode.com/problems/simplify-path/description/)

Difficulty: **Medium**



Given an absolute path for a file (Unix-style), simplify it.

For example,  
**path** = `"/home/"`, => `"/home"`  
**path** = `"/a/./b/../../c/"`, => `"/c"`

**Corner Cases:**

*   Did you consider the case where **path** = `"/../"`?  
    In this case, you should return `"/"`.
*   Another corner case is the path might contain multiple slashes `'/'` together, such as `"/home//foo/"`.  
    In this case, you should ignore redundant slashes and return `"/home/foo"`.



#### Solution

用栈模拟, `..` 出栈，其他压栈

Language: **Java**

```java
class Solution {
    public String simplifyPath(String path) {
        LinkedList<String> stack = new LinkedList<>();
        String fullPath = "";
        String[] paths = path.split("/");
        
        for(int i=0;i<paths.length; ++i){
            switch(paths[i]){
                case ".":
                    break;
                case "":
                    break;
                case "..":
                    if(stack.size()>0)stack.removeLast();
                    break;  
                default:
                    stack.addLast(paths[i]);
            };
        }
        if(stack.size()==0)return "/";
        for(String p:stack){
            fullPath = fullPath+"/"+p;
        }
        return fullPath;
    }
    
}
```