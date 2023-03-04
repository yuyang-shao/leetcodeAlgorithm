#剑指 Offer 53 - II. 0～n-1中缺失的数字
**方法一:二分查找**
```cpp
//本题相当于二分查找，当查找失败时begin或begin+1的值即为
//长度5的顺序的正确顺序是0 1 2 3 4 ，此时当begin==end时，指向4，输出5+1，若为0 2 3 4 5则为begin
//begin==end 时能找到第一个出现问题的地方
//二分法查找失败时还可能出现begin>end的情况，此时end或begin还可能越界(begin或许不会?)
class Solution {
public:
    int find(vector<int>& nums,int begin,int end){
        int mid = (begin + end)/2;
        int num;
        if(begin>=end){                       //>0 为了解决[1,2]的状况
            if(nums[begin]==begin)             //解决输入[0]
                return begin+1;
            if(nums[begin]>begin)
                return begin ;
        }
            
        if(begin<end){
            if(nums[mid]>mid){
                
                num = find(nums,begin,mid-1);
            }
            
            if(nums[mid]==mid)
                num = find(nums,mid+1,end);
        }
        return num;
    }
    int missingNumber(vector<int>& nums) {
        return find(nums,0,nums.size()-1);
    }
};
```