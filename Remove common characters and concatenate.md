Given two strings s1 and s2. Modify both the strings such that all the common characters of s1 and s2 are to be removed and the uncommon characters of s1 and s2 are to be concatenated.  
**Note:** If all characters are removed print -1.

**Example 1:**

**Input:**
s1 = aacdb
s2 = gafd
**Output:** cbgf
**Explanation:** The common characters of s1
and s2 are: a, d. The uncommon characters
of s1 and s2 are c, b, g and f. Thus the
modified string with uncommon characters
concatenated is cbgf.
	

```

class Solution
{
    public:
    //Function to remove common characters and concatenate two strings.
    string concatenatedString(string s1, string s2) 
    { 
        unordered_map<char, int> m; 
    	string res = ""; 
    
    	//using map to store all characters of s2 in map.
    	for (int i = 0; i < s2.size(); i++) 
    		m[s2[i]] = 1; 
    
    	//finding characters of s1 that are not present in s2
    	//and appending them to result.
    	for (int i = 0; i < s1.size(); i++) 
    	{ 
    		if (m.find(s1[i]) == m.end()) 
    			res += s1[i]; 
    		else
    			m[s1[i]] = 2; 
    	} 
    
    	//finding characters of s2 that are not present in s1
    	//and appending them to result.
    	for (int i = 0; i < s2.size(); i++) 
    		if (m[s2[i]] == 1) 
    			res += s2[i]; 
    			
    	if(res == "")
    	res = "-1";
    	
    	//returning the result.
    	return res; 
    } 
};
```