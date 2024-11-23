
![[Pasted image 20241123111527.png]]
### Test Cases
```
Input: arr[] = [10, 4, 3, 50, 23, 90]

Output: [90, 50, 23]

Input: arr[] = [10, 9, 9]

Output: [10, 9]

There are only two distinct elements

Input: arr[] = [10, 10, 10]

Output: [10]
```

### Approach - I 

- Change it to a set and sort it
- return the first 3 elements if the length is greater than or equal to 3
- else return the sorted array
-
```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
  public:
    vector<int> getThreeLargest(vector<int>& vec) {
        
        set<int> mySet(vec.begin(), vec.end());
        vector<int> v2(mySet.begin(), mySet.end());
        sort(v2.begin(), v2.end(), greater<int>());
        
        if (v2.size() > 2) {
            v2.resize(3);
        }
        return v2;
        
    }
};
```

### Approach - II :  Manual without using functions

- 3 vars(l1, l2, l3) as -1 of INT_MIN if it is desirable
- iterate through the array
- if current element greater than l1, update current element following by l2 and l3
- check for the cases when cur element is greater than l2 less than l1 and update l2 and l3
- check for the case when cur element is greater than l3 and less than l2. In this case update l3 only
- While printing if l1 ==  -1 then return {}, if l2 == -1 then return {l1}, if l3 == -1 then return {l1,l2} otherwise return all {l1,l2,l3}
-
```cpp
class Solution {
  public:
    vector<int> getThreeLargest(vector<int>& vec) {
        
        int l1 =  -1, l2 = -1, l3 = -1;
    
        for (int i = 0; i<vec.size(); i++) {
            if (vec[i] > l1) {
                l3 = l2;
                l2 = l1;
                l1 = vec[i];
            }else if (vec[i] > l2 && vec[i] < l1) {
                l3 = l2;
                l2 = vec[i];
            }else if(vec[i] > l3 && vec[i] < l2) {
                l3 = vec[i];
            }
        }
       
       
       if (l1 == -1) {
           return vector<int> {};
       }else if (l2 == -1) {
           return vector<int> {l1};
       }else if (l3 == -1) {
           return vector<int> {l1, l2};
       }else{
           return {l1, l2, l3};
       }
    }
};
```

### Revision Points
- Don't forget to check if the cur element is grater than second and third last element. Don't only check for cur elem > largest element

### Revision Snippets

```cpp
  for (int i = 0; i<vec.size(); i++) {
            if (vec[i] > l1) {
                l3 = l2;
                l2 = l1;
                l1 = vec[i];
            }else if (vec[i] > l2 && vec[i] < l1) {
                l3 = l2;
                l2 = vec[i];
            }else if(vec[i] > l3 && vec[i] < l2) {
                l3 = vec[i];
            }
        }
```

![[Pasted image 20241123162543.png]]

Voice Note:

![[Recording 20241123162748.m4a]]
