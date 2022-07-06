# Chapter 11 Associative Containers





## 使用一个关系容器



##### `map`

- 键值对的集合
- 常指关系数列
- "a map from type A to type B"

##### `set`

- 键的集合



### 使用 `map`

- 跟顺序容器一样, 关系容器也是模板类
- 键可以代替数字作为关系数列的 subscripts
- `map` 可以使用范围 `for` 语句, 得到数个 `pair` 对象
  - 键值对的访问可以通过 `.first` 和 `.second` 方法



### 使用 `set`

- `set` 容器也是模板
- 它可以被列表初始化

```c++
myset.find(key);
// 使用如下命令判断key是否在myset中
if (myset.find(key) == myset.end()) {}
```

- `.find` 方法返回一个迭代器
- 若 `myset` 中包含 `key` 则返回指向 `key` 的迭代器
- 若不包含 `key` 则返回尾后迭代器





## 关系容器概述



- 包含有序和无序两类
- 所有的关系容器都支持容器的常规操作
- 不支持指定位置的操作
  - 例如 `push_front` 和 `push_back`
- 包含特有操作
- 迭代器是双向的



### 定义关系容器

- 声明时会调用构造函数
- 可以拷贝初始化
- 可以通过 vector 迭代器进行范围初始化
- 可以列表初始化
  - 每个 pair 都用大括号括起来

```c++
map<string, size_t> word_count;		// 空
set<string> exclude = {"the", "but", "and", "or", "an", "a"};
map<string, string> authors = {{"Joyce", "James"}, {"Austen", "Jame"}};
```

#### 初始化 multimap 或 multiset

- 键名不必唯一



### 键类型的要求

- `map`, `multimap`, `set`, `multiset` 均为**顺序**关联容器
- 顺序关联容器的键的类型必须是定义过比较方法的类型, 比较方法默认为小于 "<"



#### 顺序容器的键的类型

##### 比较的原则 - Strict Weak Ordering

- 如果 K1 小于 K2, 则 K2 不小于 K1
- 如果 K1 小于 K2 且 K2 小于 K3, 则 K1 小于 K3
- 如果 K1 不小于 K2 且 K2 不小于 K1, 则 K1 = K2
- 如果 K1 = K2 且 K2 = K3, 则 K1 = K3

#### 为键的类型使用比较函数

```c++
bool compareIsbn(const Sales_data &lhs, const Sales_data &rhs) {
    return lhs.isbn() < rhs.isbn();
}

multiset<Sales_data, decltype (compairIsbn)*> bookstore(compareIsbn);
```

- 声明 multiset 时要指定比较函数
- 比较函数通过指针指定, 即函数指针类型
- 使用 `decltype` 返回该函数指针类型
- 若要使 `decltype` 返回函数指针类型, 必须在最后加 `*` 号
- 通过这种指定比较方法的声明形式, 可以在添加元素时将他们按顺序排列
- `bookstore(compareIsbn)` 与 `bookstore(&compareIsbn)` 等价, 因为使用函数名时会在需要时自动转换为指针类型



### pair 类型

- pair 类型是模板类
- pair 类型的数据成员默认为 public
- map 类型中每个元素的类型是 pair

#### pair 类型的操作

##### 声明及定义

```c++
pair<T1, T2> p;
pair<T1, T2> p(v1, v2);
pair<T1, T2> p = {v1, v2};
makr_pair(v1, v2);
```

- 只进行声明时, 键与值将分别使用各自类型的默认初始值
- 可以调用 pair 类型的构造函数进行初始化
- 可以使用列表初始化
- 可以使用 `make_pair()` 函数构造一个新的 pair

##### 元素访问

- `p.first` 返回键
- `p.second` 返回值

##### 比较运算

- pair 类型之间支持 `<, <=, >, >=, ==, !=`



## 关系容器的操作





## 无序容器