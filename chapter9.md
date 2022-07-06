## 9.1 Overview of the Sequential Containers

- 所有 **顺序容器** 均提供 **快速的顺序访问**
- 对于 **添加/删除元素** 和 **非顺序访问**, 不同容器的性能不同

### 顺序容器的特点

|       容器        | 特点                                    |
| :---------------: | --------------------------------------- |
| `vector (string)` | 随机访问<br />尾端快速插入/删除         |
|      `deque`      | 随机访问<br />首尾端快速插入/删除       |
|      `list`       | 双向顺序访问<br />任意位置快速插入/删除 |
|  `forward_list`   | 单向顺序访问<br />任意位置快速插入/删除 |
|      `array`      | 随机访问<br />无法添加/删除元素         |

- `vector/string` 使用连续内存
  - 根据索引可以很容易地计算元素地址
  - 但从中间插入会导致其后所有元素后移
  - 还可能涉及新的内存分配
- `list/forward_list` 的随机访问涉及链表遍历 `O(n)`
- `forward_list` 没有 `size()` 方法
- 现代 C++程序应多使用库容器而非原始结构

### 顺序容器的选择

- 默认选择使用 `vector`
- 如果空间开销是问题, 不要使用 `list/forward_list`
- 需要随机访问, 使用 `vector/deque`
- 涉及首尾端而非中间的插入/删除操作, 使用 `deque`
- 若程序在读取操作时需要在中间插入, 而随后需要随机访问的
  - 可考虑使用 `vector` 并从尾端插入, 而后使用 `sort` 方法排序
  - 若必须从中间插入, 考虑在读取阶段使用 `list`, 而后将内容复制到 `vector`
- 若程序同时需要在中间插入/删除和随机访问
  - 应比较二者的开销而后进行选择
  - 可以对两种情况分别进行测试
- 写代码时, 应多使用迭代器而不是索引, 因为前者可以适应所有的顺序容器

## 9.2 Container Library Overview

### 容器容纳类型的限制

- 大部分类型都可以被容纳
- 例如, 可以定义 `vector` 的 `vector`: `vector<vector<string>> lines`

> Although, we can store almost any type in a container, some container operations imporse requirements of their own on the element type. We can define a container for a type that does not support an operation-specific requirement, but we can use an operation only if the element type meets that operation's requirements.
