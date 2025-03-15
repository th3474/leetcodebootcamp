//Problem 1: String to Integer (atoi)
class Solution {
public:
    int myAtoi(string s) {
        int i = 0;
        int length = s.size();
        while (s[i] == ' ')
        {
            ++i;
        }
        int anstype = 1;
        if (s[i] == '-' || s[i] == '+')
        {
            if (s[i] =='-')
            {
                anstype = -1;
            }
            i++;
        }
        double sum = 0;
        while (i < length && s[i] >= '0' && s[i] <= '9')
        {
            sum = sum * 10 + (s[i] - '0');
            i++;
        }
        if (anstype == -1)
        {
            sum = -1 * sum;
        }
        if (sum > INT_MAX)
        {
            return INT_MAX;
        }
        else if (sum < INT_MIN)
        {
            return INT_MIN;
        }
        return int(sum);
    }
};

//Problem 2: Find All Anagrams in a String
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        if len(p) > len(s): return []
        pCount, sCount = {}, {}
        for i in range(len(p)):
            pCount[p[i]] = 1 +pCount.get(p[i], 0)
            sCount[s[i]] = 1 +sCount.get(s[i], 0)

        res = [0] if sCount == pCount else []
        l = 0
        for r in range(len(p), len(s)):
            sCount[s[r]] = 1 + sCount.get(s[r], 0)
            sCount[s[l]] -= 1

            if sCount[s[l]] == 0:
                sCount.pop(s[l])
            l += 1
            if sCount == pCount:
                res.append(l)
        return res

//Problem 3: Reverse Words in a String
class Solution:
    def reverseWords(self, s: str) -> str:
        words = s.split()
        res = []

        for i in range(len(words) - 1, -1, -1):
            res.append(words[i])
            if i != 0:
                res.append(" ")
                
        return "".join(res)
