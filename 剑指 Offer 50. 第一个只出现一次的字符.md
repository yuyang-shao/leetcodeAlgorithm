#剑指 Offer 50. 第一个只出现一次的字符
**方法一：unordered_map(遍历哈希表，增加一个关键字记录字符第一次出现的索引）**
- 执行时间32ms
```cpp
struct num{
    int count = 0;
    int index;
};
class Solution {
public:
    char firstUniqChar(string s) {
        for(int i = 0;i<s.length();i++){
            if(hashTable.count(s[i])){
                hashTable[s[i]].count++;

            }
            else{
                hashTable[s[i]].count = 1;
                hashTable[s[i]].index = i;
            }
        }
        unordered_map<char, num>::iterator it;
        int minIndex = 2147483647;
        for(it = hashTable.begin();it!=hashTable.end();it++){
            if(it->second.count==1&&it->second.index<minIndex){
                minIndex = it->second.index;
            }
        }
        if(minIndex<2147483647){
            return s[minIndex];
        }
        return ' ';
    }
    unordered_map<char, num> hashTable;
};
```
**方法二：方法一优化（遍历字符串)
- 执行时间反而变成44ms了
```cpp
class Solution {
public:
    char firstUniqChar(string s) {
        for(int i = 0;i<s.length();i++){
            if(hashTable.count(s[i])){
                hashTable[s[i]]++;
            }else
                hashTable[s[i]] = 1;
        }
        for(int i = 0;i<s.length();i++){
            if(hashTable[s[i]]==1)
                return s[i];
        }
        return ' ';
    }
    unordered_map<char, int> hashTable;
};
```
