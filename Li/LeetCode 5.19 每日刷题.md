1、回文数
````Java
class Solution {
    public boolean isPalindrome(int x) {
        if(x<0)
        return false;
        int r = 0;
        int y = 0;
        int temp = x;
        while(temp != 0){
            r = temp%10;
            y = y*10+r;
            temp = temp/10;
        }
        return x == y;
    }
}
````
2、最长回文子串
````Java
class Solution {
    public String longestPalindrome(String s) {
        if(s == null || s.length()<1)
        return "";
        int start = 0;
        int end = 0;
        for(int i = 0;i<s.length();i++){
            int len1 = expandAroundCenter(s,i,i);
            int len2 = expandAroundCenter(s,i,i+1);
            int len = Math.max(len1,len2);
            if(len > end-start){
                start = i-(len-1)/2;
                end = i + (len/2);
            }
        }
        return s.substring(start,end+1);
    }
    private int expandAroundCenter(String s, int left, int right){
        int L = left;
        int R = right;
        while(L>=0 && R<s.length() && s.charAt(L)==s.charAt(R)){
            L--;
            R++;
        }
        return R-L-1;
    }
}
````
