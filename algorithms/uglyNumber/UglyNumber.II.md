```
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> q(1,1);
        for(int i=0,j=0,k=0;q.size()<n;){
            int x=min(q[i]*2,min(q[j]*3,q[k]*5));
            q.push_back(x);
            if(q[i]*2==x)i++;
            if(q[j]*3==x)j++;
            if(q[k]*5==x)k++;
        }
        return q.back();
    }
};
```

