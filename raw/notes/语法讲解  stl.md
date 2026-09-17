c++:stl

#### vector
相当于一个可变的数组。
```c++
    vector<int> a; //一维
	vector<int> c(10);//大小为10
    vector<vector<int> > c; //二维
    a.assign(10, 1); //长度设为10，每个值为1
    a.push_back(5); //在末尾插入元素
    a.pop_back(); //弹出末尾的元素
    int l = a.front(), r = a.back(); //首元素和尾元素
    vector<int>::iterator itl = a.begin();//首迭代器
    vector<int>::iterator itr = a.end();//尾迭代器
    a.size(); //容器的大小
    a[0]; //容器元素
    a.insert(a.begin() + 2, 1); //在元素之前添加一个数字
    a.erase(a.begin() + 2); //删除元素，2个元素可区间删除
    a.clear(); //清空
    reverse(a.begin(), a.end()); //翻转
    for (auto it: a) {}
```

#### deque

少用，时间复杂度常数很高，空间也高

在vector的基础上，新增
```c++
push_front()//在首部插入元素
pop_front()//在首部弹出元素
```


#### map

按首元素进行排序. 从小到大。
因此如果首元素是自定义的类型，需要重载()。
时间复杂度是logn级别的。用红黑树实现的。

```c++
    map<int,int> a;
    map<string,float> b;
	map<int,int,greater<int>> c;//从大到小
    a[5];//可直接访问空的，会新增，默认元素0
    a.erase(5);//删除元素
    a.count(2);//元素个数
    a.size();//大小
    a.clear();//清空
    map<int,int>::iterator itl=a.begin();//首迭代器
    map<int,int>::iterator itr=a.end();//尾迭代器
    itl->first;//第一个值
    itl->second;//第二个值
    for (auto it:a) {
        it.first;
        it.second;
    }
```

#### unordered_map
在map的基础上，没有排序。
因此没有首迭代器和尾迭代器
时间复杂度O(1)-O(n)
尽量不用，有出题人故意卡O(n),导致tle。

#### set
当排好序且去重的数组
时间复杂度logn

```c++
    set<int> a;
    set<int,greater<int>> b;
    a.insert(1);//插入元素
    a.erase(2);//删除元素
    a.count(3);//元素个数
    a.size();//大小
    a.clear();//清空
    a.lower_bound(3);//二分，大于等于，直接返回元素
    a.upper_bound(3);//二分，大于，直接返回元素
```

#### unordered_set
在map的基础上，没有排序。
因此没有首迭代器和尾迭代器,二分
时间复杂度O(1)-O(n)
尽量不用，有出题人故意卡O(n),导致tle。

#### queue
```c++
    queue<int> q;
    q.push(1);//插入一个元素
    q.pop();//弹出
    q.front();//首元素
    q.back();//尾元素
    q.size();//大小
    queue<int> p;
    q.swap(p);//没有clear，用swap来清空
```

#### stack
```c++
    stack<int> q;
    q.push(1);//插入一个元素
    q.pop();//弹出
    q.top();//栈顶元素
    q.size();//大小
    stack<int> p;
    q.swap(p);//没有clear，用swap来清空
```

#### list
```c++
    list<int> a;
    a.push_back(10);//尾部插入元素
    a.push_front(20);//头部插入元素
    a.pop_front();//头部弹出
    a.pop_back();//尾部弹出
    a.remove(10);//删除所有值
    a.erase(a.begin());//删除位置
    a.reverse();//翻转
    for (auto it:a){}
    list<int>::iterator itl = a.begin();
    list<int>::iterator itr = a.end();
    advance(itl, 2);//注意不能+2，可以++，--,往右移两格
    a.insert(itl, 5);//插入
    a.size();//大小
    a.front();//头元素
    a.back();//尾元素
```