# search-pattern
day 18 of my gfg 160 days challange

class Solution {
public:
    void computeLPS(string &pat, vector<int> &lps) {
        int m = pat.size();
        int len = 0;
        lps[0] = 0;
        int i = 1;
        
        while (i < m) {
            if (pat[i] == pat[len]) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len != 0) {
                    len = lps[len - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
    }
    
    vector<int> search(string &pat, string &txt) {
        int n = txt.size();
        int m = pat.size();
        vector<int> lps(m, 0);
        computeLPS(pat, lps);
        
        vector<int> result;
        int i = 0;
        int j = 0;
        
        while (i < n) {
            if (pat[j] == txt[i]) {
                i++;
                j++;
            }
            
            if (j == m) {
                result.push_back(i - j);
                j = lps[j - 1];
            } else if (i < n && pat[j] != txt[i]) {
                if (j != 0) {
                    j = lps[j - 1];
                } else {
                    i++;
                }
            }
        }
        
        if (result.empty()) result.push_back(-1);
        return result;
    }
};

