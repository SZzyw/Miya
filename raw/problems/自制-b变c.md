题目：
给定三个数组a,b,c。当`a[i]<=a[j]`并且`b[i]<=b[j]`时(i,j没要求)，将`a[i]，a[j]`交换，`b[i]，b[j]`交换，问能否将b数组变为c数组，可以输出Yes,不行输出No
数据范围：1<=n<=1e6    1<=a\[i\],b\[i\],c\[i\]<=1e8
保证b的内容与c的内容是相等的，只是顺序不一样。

思路：
由于数据范围比较大，我们先对a,b,c进行离散化，注意要相对顺序不变，这样对比较就没有影响，因此不会影响答案

因为i，j没有影响，因此我们可以通过一个a小b小的值将比这个值大的都放好位置,就是把这个数作为一个中转站
例如：一个长度为4的数组`a[1]=1,b[1]=1`，那我们可以将b数组转换成任意数组
a: 1 2 3 4
b: 1 4 2 3
c: 4 1 3 2

这样思路就很明确了，我们可以用并查集将这些数组合在一起，在一起的数可以任意交换
但如何组合在一起呢，总不能for套for找吧

正所谓当有两个变值的时候，先遍历一个，另一个通过别的方法来快速实现，这样就不会$n^2$了

我们先`a[i],b[i],c[i]`看作一个整体，按a从小到大排序，由于i,j没有要求，因此对答案无影响
那么此时只要`i<j&&b[i]<=b[j]`就满足了要求
再根据之前的结论，我们可以找到b小的，这个值之后的都可以放在一个集合里面。
因此：我们可以通过从b最小的进行讨论，也就是1，假设1的下标为i，那么i以后的我都可以放在一个集合里面。都在一个集合里，我就可以保留一个该集合里b最大的保留下来，剩下的都删了。接着再讨论2，3，4....
那如果讨论的数比如10，后面有个数是8不就没法连接了。是的，而且后面的数都不用遍历了，因为8我们之前已经讨论过了，说明后面的数都<=8,没有>10的数
删除操作，我们当然不能真的删了，可以使用并查集跳着走的特性，把这一段都跳过去。       因此讨论2，3，4....时我们只需要讨论`i!=f[i]`的情况。

```c++
#include <bits/stdc++.h>
using namespace std;
struct DSU {
    vector<int> father,mmax;
    DSU(int n) {
        father.assign(n, 0);
        mmax.assign(n, 0);
        for (int i=0;i<n;i++)
            father[i] = i;
    }
    int find(int x) {
        int root=x;
        while (father[root]!=root)
            root=father[root];
        while (father[x]!=x) {
            int nxt=father[x];
            father[x]=root;
            x=nxt;
        }
        return root;
    }
    void unite(int x, int y) {
        int fx=find(x), fy=find(y);
        if (fx!=fy) {
            father[fx]=fy;
            mmax[fy]=max(mmax[fy],mmax[fx]);
        }
    }
};
struct Discrete {
    vector<int> arr;
    Discrete(vector<int> &v) {
        arr=v;
        sort(arr.begin(), arr.end());
        arr.erase(unique(arr.begin(), arr.end()), arr.end());
    }
    int find(int x) {
        return lower_bound(arr.begin(), arr.end(), x) - arr.begin();
    }
};
void solve() {
    int n;
    cin>>n;
    vector<array<int,3>> v(n);
    vector<int> a(n),b(n),c(n),mp;
    mp.assign(n,n+10);

    for (int i=0;i<n;i++)
        cin>>v[i][0];
    for (int i=0;i<n;i++)
        cin>>v[i][1];
    for (int i=0;i<n;i++)
        cin>>v[i][2];
    sort(v.begin(), v.end());

    for (int i=0;i<n;i++)
        a[i]=v[i][0];
    Discrete aa(a);
    for (int i=0;i<n;i++)
        a[i]=aa.find(a[i]);
    for (int i=0;i<n;i++)
        b[i]=v[i][1];
    Discrete bb(b);
    for (int i=0;i<n;i++) {
        b[i]=bb.find(b[i]);
        mp[b[i]]=min(mp[b[i]],i);
    }
    for (int i=0;i<n;i++)
        c[i]=v[i][2];
    Discrete cc(c);
    for (int i=0;i<n;i++)
        c[i]=cc.find(c[i]);

    DSU dsu(n);
    dsu.mmax=b;

    for (int i=0;i<bb.arr.size();i++) {
        int x=mp[i];
        if (x!=dsu.find(x))
            continue;
        int y=x+1;
        while (y<n) {
            y=dsu.find(y);
            if (dsu.mmax[y]<i)
                break;
            dsu.unite(x,y);
            y++;
        }
    }

    for (int i=0;i<n;i++) {
        int x=mp[c[i]];
        if (dsu.find(x)!=dsu.find(i)) {
            cout<<"No"<<endl;
            return;
        }
    }

    cout<<"Yes"<<endl;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    solve();
    return 0;
}
```
