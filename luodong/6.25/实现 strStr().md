# [28. 实现 strStr()](https://leetcode-cn.com/problems/implement-strstr/)




### 代码实现


~~~java
//法一：子串逐一比较
class Solution {
  public int strStr(String haystack, String needle) {
    int L = needle.length(), n = haystack.length();
    //考虑haystack和needle为空串的时候【不然下面会越界】
    if(L==0 && n==0)
        return 0;
    if(L==0)
        return 0;
    for (int start = 0; start < n - L + 1; ++start) {
      //只有子串的第一个字符跟 needle 字符串第一个字符相同的时候才需要比较
      if(haystack.charAt(start) != needle.charAt(0))
        continue;
      if (haystack.substring(start, start + L).equals(needle)) {
        return start;
      }
    }
    return -1;
  }
}

//法二：双指针
class Solution {
  public int strStr(String haystack, String needle) {
    int L = needle.length(), n = haystack.length();
    if (L == 0) return 0;

    int pn = 0;
    while (pn < n - L + 1) {
      // find the position of the first needle character
      // in the haystack string
      while (pn < n - L + 1 && haystack.charAt(pn) != needle.charAt(0)) ++pn;

      // compute the max match string
      int currLen = 0, pL = 0;
      while (pL < L && pn < n && haystack.charAt(pn) == needle.charAt(pL)) {
        ++pn;
        ++pL;
        ++currLen;
      }

      // if the whole needle string is found,
      // return its start position
      if (currLen == L) return pn - L;

      // otherwise, backtrack
      pn = pn - currLen + 1;
    }
    return -1;
  }
}
~~~