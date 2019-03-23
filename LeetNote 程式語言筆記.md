# LeetNote 程式語言筆記
# 三者的比較表


|| C++ | Java | Python
| - | - | - | - |
|結尾分號|YES|YES|NO|
|string只能用雙引號|YES|NO|NO|
|string的宣告方式|import string; string s1("Ex")或string s1; 不能有括號。如果要用new的話前面要變成pointer,ex.string *s1 = new string("fsd")|String s1 = "Ex";String s1 = new String(); String s1 = new String("") 但不可String s1;|s1 = "Ex"|
|string長度|s1.length()|s1.length()|len(s1)|
|string元素|s1\[0\]or s1.at(0)|s1.charAt(index數)|s1\[0\]|
|foreach用法|for(char a:s1)|for(char a: s1.toCharArray())|for a in s1:|
|substring|s1.substr(1, 3) 1是index值 3是長度|s1.substring(1,4) 4是end index(不包括)|s1[1:4] 4是end index(不包括)|
|class裡的函數|class Solution { public: int fun(string J){;}};|class Solution{public int fun(String J) {;}}|class Solution(object):def fun(self, J):|
|輸出|cout<<"T"<<endl;|System.out.println("T")|print("T")|
|List|無|無|arr = [1, 2]|
|陣列|int arr[] = {1, 2};(不可以寫int[] arr = {1, 2})或int* arr = new int[size];|int[] arr = {1, 2};或 int[] arr = new int[長度]，如果不指定長度則一定要初始化|numpy.array([1, 2])|
|陣列長度|無法直接取得，要自己數|陣列名稱.length|len(list名稱)|
|位元操作(幾個'1')|bitset<32>(x).count();|Integer.bitCount(x)|bin(x).count('1')  #bin()回傳binary string, count是string的函數|
|NULL大小寫|NULL|null|沒有null只有None|
|判斷是否為空|如果是int或指針，可用if(!a)或if(a==NULL)|不可用if(!a),一定要寫if(a == null)，java的!運算子只能用在boolean上|if a is None或 if not a|
|判斷string是否為空的|s1.empty(),此外string無法初始化為NULL|s1 ==null \|\| s1.isEmpty()|if s1: print("not empty") 或 if s1 == "":|
|ternary ?:|?:|?:|沒有?:語法，而是用 x=1 if 條件 else 2|

# JAVA
```
console.log('main')

```

This is [Geego Official][0] reference-style link.
This is [Geego Blog][1] reference-style link.

[0]: http://www.geego.com.tw/ "Geego Official Site"
[1]: http://blog.geego.com/ "Geego Blog"

# C++

## 位元運算
### bitset
>初始化：bitset<bit大小>b1;

>判斷'1'個數： count();
ex.b1.count()

>判別bitet 位元數大小
b.size();

>判別是否有 '1' 
b.any();

>判別是否沒 '1' 
b.none();

>判別 '0' 之個數
cnt = b.size() - b.count();
## vector
## list
## set



# Python
## 邏輯運算子
### and
> A and B回傳的並不是boolean，如果A跟B都有值，則回傳最後那個也就是B，如果A或B有一個是負的，回傳None。