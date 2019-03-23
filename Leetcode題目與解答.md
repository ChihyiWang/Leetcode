# Leetcode題目與解答

## 1.Jewels and stones(771)
>String J是擁有的石頭名稱，String S是鑽石名稱，看自己擁有的石頭有多少是鑽石。
### C++
#### My version
```
class Solution {
public:
    int numJewelsInStones(string J, string S) {
        int num = 0;
        for(char s: S){
            for(char j: J){
                if(s == j){
                    num++;
                }    
            }
        }
        return num;
    }
};
```
#### Other version
```
#1
class Solution {
public:
    int numJewelsInStones(string J, string S) {
        vector<int> map(128, 0);
        int res = 0;        
        for (char& c : J) map[c]++;
        for (char& c : S) if (map[c]) res++; 
        return res;
    }
};
#2
class Solution {
public:
    int numJewelsInStones(string J, string S) {
        int res = 0;
        unordered_set<char> setJ(J.begin(), J.end());
        for (char s : S) if (setJ.count(s)) res++;
        return res;
    }
};
```

### Java
#### My version
```
class Solution {
    public int numJewelsInStones(String J, String S) {
        int num = 0;
        for(char i : S.toCharArray()){
            for(char j : J.toCharArray()){
                if(i == j){
                    num++;
                }    
            }
        }
        return num;
    }
}
```
#### Other version
```
#很簡潔，但是速度比較慢..
class Solution {
    public int numJewelsInStones(String J, String S) {
        return S.replaceAll("[^" + J + "]", "").length();
    }
}

#用Hashset 因為contains()是O(1)
class Solution {
    public int numJewelsInStones(String J, String S) {
            int res = 0;
            Set setJ = new HashSet();
            for (char j: J.toCharArray()) setJ.add(j);
            for (char s: S.toCharArray()) 
                if (setJ.contains(s)) 
                    res++;
            return res;
    }
}
```

### Python
#### My version
```
class Solution(object):
    def numJewelsInStones(self, J, S):
        """
        :type J: str
        :type S: str
        :rtype: int
        """
        return sum([s in J for s in S])
        
```
#### Other version
```
class Solution(object):
    def numJewelsInStones(self, J, S):
        setJ = set(J)
        return sum(s in setJ for s in S)
```

## 2.*Hamming Distance(461)
>The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

>Given two integers x and y, calculate the Hamming distance.

>Note:
>0 ≤ x, y < 231.
>例如1(0001)跟4(0100)-->有兩個bit不一樣，output:2

### C++
#### My version
```
class Solution {
public:
    int hammingDistance(int x, int y) { //x = 4 y=1
        int xorr = x ^ y; //xorr = 0101
        int num = 0;
        while(xorr > 0){
            num += xorr & 1; //等於AND 0001 也就是取個位數-->1+0+1+0
            xorr >>= 1;  //向右移
        }
        return num;
    }
    
};
```
#### Other version
```
class Solution {
public:
    int hammingDistance(int x, int y) {
        return bitset<32>(x^y).count();
    }
};

class Solution {
public:
    int hammingDistance(int x, int y) {
        return __builtin_popcount(x^y);
    }
};

class Solution {
public:
    int hammingDistance(int x, int y) {
        int dist = 0, n = x ^ y;
        while (n) {
            ++dist;
            n &= n - 1;
        }
        return dist;
    }
};

```
### Java
#### My version
```
內容跟C++的一樣
```
#### Other version
```
public class Solution {
    public int hammingDistance(int x, int y) {
        return Integer.bitCount(x ^ y);
    }
}
```
### Python
#### My version
```
內容用C++的去改
```
#### Other version
```
#bin()回傳binary string, count是string的函數
class Solution:
    def hammingDistance(self, x: int, y: int) -> int:
        return bin(x^y).count('1')
class Solution:
    def hammingDistance(self, x: int, y: int) -> int:
        return sum(((x ^ y) >> n) & 1 for n in range(32))
        
```

## 3.Merge two binary tree(617)
### C++
#### My version
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
        if(!t1 && !t2){
            return NULL;
        }
        TreeNode *root = new TreeNode((t1?t1->val:0) + (t2?t2->val:0)); 
        root->left = mergeTrees(t1?t1->left:NULL, t2?t2->left:NULL);
        root->right = mergeTrees(t1?t1->right:NULL, t2?t2->right:NULL);
        return root;            
    }
};

```
#### Other version
```
#新的tree跟old tree共用node，可能會發生問題！
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
        if(t1==NULL)
            return t2;
        if(t2==NULL)
            return t1;
        
        t1->val += t2->val;
        t1->right = mergeTrees(t1->right, t2->right);
        t1->left = mergeTrees(t1->left, t2->left);
        
        return t1;
    }
};
```
### Java
#### My version
```
//把C++那邊的寫法修改成java語法(NULL->null, 箭頭變成., 沒有指標)
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if(t1 == null && t2 == null){
            return null;
        }
        TreeNode root = new TreeNode((t1 != null?t1.val:0) + (t2 != null?t2.val:0)); 
        root.left = mergeTrees(t1!= null?t1.left:null, t2!= null?t2.left:null);
        root.right = mergeTrees(t1!= null?t1.right:null, t2!= null?t2.right:null);
        return root;      
    }
}
```
### Python
#### My version
```
#轉換成python語法(?:轉換，null->None)
class Solution:
    def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
        if t1 == None and t2 == None:
            return None
        root = TreeNode((t1.val if t1 != None else 0) + (t2.val if t2 != None else 0))
        root.left = self.mergeTrees(t1.left if t1 != None else None, t2.left if t2 != None else None)
        root.right = self.mergeTrees(t1.right if t1 != None else None, t2.right if t2 != None else None)
        return root
```
#### Other version
```
# 可以用not來判斷是不是None，還有注意and的用法!!!
class Solution:
    def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
        if not t1 and not t2:
            return None
     
        root = TreeNode((t1.val if t1 else 0) + (t2.val if t2 else 0))
        root.left = self.mergeTrees(t1 and t1.left, t2 and t2.left)
        root.right = self.mergeTrees(t1 and t1.right, t2 and t2.right)
        return root
```

## 4.*Counting Bits(338)
> Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.
### C++
#### My version
```
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> ret(num+1, 0);
        for (int i = 1; i <= num; ++i)
            ret[i] = ret[i>>1] + (i & 1);
        return ret;
    }
};
```
#### Other version
```
https://leetcode.com/problems/counting-bits/discuss/119131/C++-Easy-to-Understand-Solution
理解用的網站
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> ret(num+1, 0);
        for (int i = 1; i <= num; ++i)
            ret[i] = ret[i&(i-1)] + 1;
        return ret;
    }
};
```

### Java
#### My version
#### Other version

### Python
#### My version
#### Other version


## 5. 
### C++
#### My version
#### Other version

### Java
#### My version
#### Other version

### Python
#### My version
#### Other version

## 6. 
### C++
#### My version
#### Other version

### Java
#### My version
#### Other version

### Python
#### My version
#### Other version

## 4. 
### C++
#### My version
#### Other version

### Java
#### My version
#### Other version

### Python
#### My version
#### Other version

## 4. 
### C++
#### My version
#### Other version

### Java
#### My version
#### Other version

### Python
#### My version
#### Other version

## 4. 
### C++
#### My version
#### Other version

### Java
#### My version
#### Other version

### Python
#### My version
#### Other version

## 4. 
### C++
#### My version
#### Other version

### Java
#### My version
#### Other version

### Python
#### My version
#### Other version