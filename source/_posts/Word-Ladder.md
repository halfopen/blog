title: Word Ladder
author: Halfopen
tags:
  - leetcdoe
  - medium
categories:
  - 刷题
date: 2018-01-01 14:27:00
---
### [127\. Word Ladder](https://leetcode.com/problems/word-ladder/description/)

Difficulty: **Medium**

Given two words (_beginWord_ and _endWord_), and a dictionary's word list, find the length of shortest transformation sequence from _beginWord_ to _endWord_, such that:

1.  Only one letter can be changed at a time.
2.  Each transformed word must exist in the word list. Note that _beginWord_ is _not_ a transformed word.

每次只能改变一个字母，改变之后的单词必须在wordlist中,类似于数组的编辑距离，但是对结果进行的限制。

For example,

Given:  
_beginWord_ = `"hit"`  
_endWord_ = `"cog"`  
_wordList_ = `["hot","dot","dog","lot","log","cog"]`  

As one shortest transformation is `"hit" -> "hot" -> "dot" -> "dog" -> "cog"`,  
return its length `5`.

**Note:**  

*   Return 0 if there is no such transformation sequence.
*   All words have the same length.
*   All words contain only lowercase alphabetic characters.
*   You may assume no duplicates in the word list.
*   You may assume _beginWord_ and _endWord_ are non-empty and are not the same.

**<font color="red" style="display: inline;">UPDATE (2017/1/20):</font>**  
The _wordList_ parameter had been changed to a list of strings (instead of a set of strings). Please reload the code definition to get the latest changes.

#### Solution

使用层次遍历 bfs即可，因为Note里面有限定条件，因此不必自己构建无向图，按26个英文字母遍历即可。

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> wordSet = new HashSet<>(wordList); // 把list转成set,防止超时 contains由O(n)变为O(1)
        if(!wordSet.contains(endWord))return 0;
        int res = 1;
        LinkedList<String> q = new LinkedList<>();
        q.addLast(beginWord);      
        while(!q.isEmpty()){     
            int qSize = q.size();
            while(qSize-->0){
                String s = q.getFirst();
                for(int j=0;j<s.length();j++){
                    char[] temp = s.toCharArray();
                    for(int i=0;i<27;i++){
                        char c = (char)('a'+i);
                        temp[j] = c;
                        String word = String.valueOf(temp);
                        if(word.equals(endWord))return res+1;
                        if(wordSet.contains(word)){
                            q.addLast(word);
                            wordSet.remove(word);
                        }
                    }
                }
                q.removeFirst();
            }
            res++;
        }
        return 0;
    }
}
```


