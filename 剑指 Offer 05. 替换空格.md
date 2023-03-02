#剑指 Offer 05. 替换空格
**方法一 用一个新的数组保存
- 用空间换时间
```c
char* replaceSpace(char* s){
    int count = 0,length =0;
    while(s[length]){
        if(s[length]==' ')
            count++;
        length++;    
    }
    length = length + 1;    //数组下标从0开始，所以长度应该加1
    int newLength = length+2*count+1;       //字符串结尾有'\0'
    char *temps = (char*)malloc(newLength*sizeof(char));
    int i = 0,j = 0; // i代表temp当前位置，j代表s当前位置
    while(s[j]){
        if(s[j]==' '){
            temps[i] = '%';
            temps[i+1] = '2';
            temps[i+2] = '0';
            i = i+3;
        }
        else{
            temps[i++] = s[j]; 
        }
        j++;
    }
    temps[i] = '\0';
    return temps;
}
```

**方法二：c++ STL 库函数
```c++
class Solution {
public:
    string replaceSpace(string s) {
        string s1 = "%20";
        int i =0,length = s.length();
        while(i<length){
            if(s[i]==' '){
                // printf("%c",'1');
                s.replace(i,1,s1);
                length = length + 2;
            }
            i++;
        }
        return s;
    }
};
```

