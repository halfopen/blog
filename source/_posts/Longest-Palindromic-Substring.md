title: Longest Palindromic Substring
author: Halfopen
tags:
  - leetcode
categories:
  - 刷题
date: 2017-11-22 22:05:00
---
### [5\. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)

最长回文子串

Difficulty: **Medium**

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

**Example:**

```
**Input:** "babad"

**Output:** "bab"

**Note:** "aba" is also a valid answer.
```

**Example:**

```
**Input:** "cbbd"

**Output:** "bb"
```

#### My Solution
- 暴力枚举，会直接超时
```java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length()<=1)return s;
        String ls="";
        for(int i=0;i<s.length();i++){
            for(int j=i+1;j<=s.length();j++){
                String curr = s.substring(i,j);
                if(isPalindrome(curr)){
                    if(curr.length()>ls.length()){
                        ls = curr;
                    }
                }
            }
        }
        return ls;
    }
    
    public boolean isPalindrome(String s){
        for(int i=0;i<s.length();i++){
            if(s.charAt(i)!=s.charAt(s.length()-i-1)){
                return false;
            }
        }
        return true;
    }
}
```
- 动态规划，时间复杂度O(n^2)

用dp[i][j]来表示substring(i,j+1)是否为回文串，如果s[i+1][j-1]==1，且s[i]==s[j]，则s[i][j]=1

那么有递推公式  dp[ i ][ j ] = dp[ i + 1][ j - 1] && s[ i ] == s[ j ]
初始化条件 dp[i][i]=1, dp[i][i+1]=1，如果s[i]==s[i+1]

超时
```java
class Solution {
        public String longestPalindrome(String s) {
            if(null==s)return null;
            if(s.length()<=1)return s;
            String ls=s.substring(0,1);
            
            int length = s.length();
            int maxLenth = 1;
            
            int[][] dp = new int[length][length];
            
            // init dp[i][i],dp[i][i+1]
            for(int i=0;i<length;i++){
                dp[i][i]=1;
                if(i+1<length && s.charAt(i)==s.charAt(i+1)){
                    dp[i][i+1]=1;
                    ls = s.substring(i,i+2);
                }
            }
            
            // dp
            for(int len=3;len<=length;++len){
                for(int i=0;i<length-len+1;++i){
                    //System.out.println("sub:"+s.substring(i,i+len-1));
                    int j = i+len-1;
                    if(s.charAt(i)==s.charAt(j)&&dp[i+1][j-1]==1){
                        dp[i][j]=1;
                        if(maxLenth<j-i+1){
                            maxLenth = j-i+1;
                            ls = s.substring(i,j+1);
                        }
                    }else{
                        dp[i][j]=0;
                    }
                }
            }
            System.out.println(ls);
            return ls;
        }

}

```

- 中心点拓展，时间复杂度O(n^2)

回文串的特点是有一个对称中心 aba对称中心为b  aa对称中心为a和a之间的间隙，因此要对回文串两种情况进行判断


```java
class Solution {
    int maxlen = 0;
    int low = 0;
    public String longestPalindrome(String s) {
        if(s.length() < 2) {
            return s;
        }
        String res = "";
        int max = 0;
        for(int i = 0; i < s.length()-1; i ++) {
            extendPali(s, i, i);
            extendPali(s, i, i+1);
        }
        return s.substring(low, low+maxlen);
        
    }
    public void extendPali(String s, int left, int right) {
        while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left --;
            right ++;
        }
        int len = right-left-1;
        if(len > maxlen) {
            low = left+1;
            maxlen = len;
        }
    }
}

```


- Manacher 时间复杂度O(n)
```java
class Solution {
        public String longestPalindrome(String s) {
            if(null==s)return null;
            if(s.length()<=1)return s;
            String ls="";
            int maxLen=1;
            int maxPosition=1;
            
            String st="#";
            for(int i=0;i<s.length();++i){
                st+=s.substring(i,i+1)+"#";
            }
            int maxRight=0, pos=0;
            int[] RL = new int[st.length()];
            for(int i=0;i<st.length();++i){
                //
                if(i<maxRight){
                    RL[i] = Math.min(RL[2*pos-i], maxRight-i);
                }else{
                    RL[i] = 1;
                }

                // expand
                while(i-RL[i]>=0 && i+RL[i]<st.length() && st.charAt(i-RL[i])==st.charAt(i+RL[i])){
                    RL[i]++;
                }

                // update
                if(i+RL[i]>maxRight){
                    maxRight = i+RL[i];
                    pos = i;
                }

                // save the longest substring
                if(RL[i]-1> maxLen){
                    maxLen = RL[i]-1;
                    maxPosition = i;
                }
            }
            ls = st.substring(maxPosition-maxLen, maxPosition+maxLen+1).replaceAll("#", "");
            return ls;
        }

}
```

http://blog.csdn.net/feliciafay/article/details/16984031