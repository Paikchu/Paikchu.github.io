# 5. Longest Palindromic Substring

Algorithm: 双指针
Data Structure: String
Difficulty: Medium
Last Review Time: September 5, 2022 1:42 PM
No: 5

# 中心扩散

分两种情况：

1. Palindromic substring 的中心为单个字母, eg. bab
2. 中心为两个字母并排，eg. abba
    
    ```cpp
    class Solution {
    public:
        string longestPalindrome(string s) {
            // 中心扩散
            int ans = 0;
            int start = 0;
            int len = s.size();
            for(int p = 0; p < len; ++p){
    						// 第一种情况，单个字母在中间
                int sublen = 0;
                int i;
    						// 需要注意此处循环从i=1开始
                for(i = 1; p + i < len && p - i >= 0; ++i){
                    if(s[p-i] == s[p+i])
                        sublen += 2;
                    else
                        break;
                }
                sublen += 1;// 此处+1为字符串中心的单个字母
                if(ans < sublen){
                    ans = sublen;
                    start = p - i + 1;
                }
    						// 第二种情况，两个字母并排
                sublen = 0;
                if(s[p+1] == s[p]){
                    for(i = 0 ; p+i+1 < len && p-i >= 0; ++i){
                        if(s[p+i+1] == s[p-i])
                            sublen += 2;
                        else
                            break;
                    }
                    if(ans < sublen){
                        ans = sublen;
                        start = p - i + 1;
                    }
    
                }
            }
            return s.substr(start, ans);
        }
    };
    ```