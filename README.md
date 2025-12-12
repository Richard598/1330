我已经把你 zip 里的 ENGG1330 课件按章节扫了一圈（标题有 Terminology / Tuple / While / Strings / Functions / Recursion / Searching & Sorting / Triominos / More about Functions 等），下面给你整理成一份**期末复习用总笔记**。

> 说明：PDF 里很多是投影片+手写，机器读出来的文字不完整（中间有很多 `...`），所以我按**章节标题 + 典型 ENGG1330 内容 + 你「ENGG1330 Notes.pdf」中的提示**综合整理，侧重复习结构和易错点。

---

## 0. 整体框架（按你文件名）

* 1.pdf：Course Details & Motivation
* 2.x：Python 基础：Terminology, Literals, Variables, Operators, Expressions, Casting
* 3.x：Tuple / List / Dictionary / Set / While / For
* 4.x：Strings（介绍 / 操作 / 函数 / 不可变 / f-string / 示例：加密和排序）
* 5.x：ID / More Tuples / More Lists / File I/O
* 6.x：Built-in Functions / Modules / Tossing a Coin example
* 7.1 / 7.2：Functions / Passing immutable & mutable objects
* 8.pdf：Recursion
* 9.pdf：Searching & Sorting（线性/二分/冒泡/插入/选择排序）
* 10.pdf：Triominos（递归 + 分治 + 2D 数组）
* 11.pdf：More about Functions
* ENGG1330 Notes.pdf：大量 numbered exam tips（运算优先级、负数取模、`extend` vs `append`、`type()`、变量命名、`enumerate`、Tower of Hanoi、searching/sorting/recursion 等）

---

## 1. Python 基本术语（2.1 Terminology）

**术语：**

* Literal（字面量）：直接写在代码里的数据

  * 例：`3`, `3.14`, `"hello"`, `True`
* Variable（变量）：给数据起名，存储在内存中的位置

  * 例：`area = 10`
* Operator（运算符）：执行运算的符号

  * `+ - * / // % **`, `and or not`, `== < > <= >= !=`
* Expression（表达式）：由字面量 + 变量 + 运算符组合而成，有一个“值”

  * 例：`pi * (diameter/2) ** 2`

**易错点：**

* 表达式是“有值”的东西；`if`、`while` 不是表达式，是语句（statement）。
* `=` 是赋值，不是比较；比较用 `==`。

---

## 2. 字面量、变量、类型与运算符（2.2–2.6）

### 2.1 字面量 & 基本类型

* 整数：`int`，可以用下划线：`1_000_000`
* 浮点数：`float`，支持科学计数：`1.23e-4`
* 布尔：`True` / `False`
* 字符串：`"abc"` 或 `'abc'`
* `None`：表示空、没有值

### 2.2 变量与命名规则（2.3 Variables）

* 赋值：`x = 3`，右边先算表达式再赋给左边变量。
* 命名规则：

  * 只能用字母 / 数字 / 下划线，**不能以数字开头**。
  * 不能与关键字冲突：`for`, `if`, `else`, `assert`, `async`, `await` 等。
  * ENGG1330 Notes 里特别提到一些**看起来合法但有坑**的名字：如 `str`, `__`, `_x`, `_for` 等（注意不要覆盖内建函数名，比如 `str`、`list`）。

### 2.3 运算符（2.4.x）

1. **算术运算符**（2.4.1）

   * `+  -  *  /  //  %  **`
   * `//`：整除，向下取整
   * `%`：取模（余数）

   **负数取模（Notes 强调）**：
   Python 里 `a % b` 的结果与 `b` 同号；记住 pattern：

   ```python
   -5 % 3 == 1   # because -5 = (-2)*3 + 1
   ```

   题目可能考「负数 mod」的 pattern。

2. **赋值运算符**（2.4.2）

   * `=`, `+=`, `-=`, `*=`, `/=`, `//=`, `%=`, `**=`
   * `x += 1` 是 `x = x + 1` 的缩写。

3. **比较与布尔运算符**（2.4.3 & 2.4.4）

   * 比较：`== != < <= > >=`
   * 布尔：`and  or  not`
   * **短路**：

     * `a and b`：若 `a` 为 False，直接返回 `a`，不计算 `b`
     * `a or b`：若 `a` 为 True，直接返回 `a`
   * if/else 中常见组合：

     ```python
     if 0 < x <= 10:
         ...
     ```

4. **运算优先级（Notes 强调）**

   * 总体从高到低：
     `**` > 一元 `+ -` > `* / // %` > `+ -` > 比较 > `not` > `and` > `or`
   * 记一个简单版本：
     **括号永远最高，逻辑运算符优先级最低。**

5. **类型转换 & 方括号运算符（2.6 Casting and []）**

   * `int()`, `float()`, `str()`, `list()`, `tuple()` 等
   * `[]`：索引 / 切片。

     * `s[i]`：第 `i` 个元素（从 0 开始）
     * `s[a:b]`：从 `a` 到 `b-1` 的切片

---

## 3. 复合数据结构（3.x + 5.x）

### 3.1 Tuple（3.1, 5.2）

* 有序、**不可变**：

  ```python
  t = (1, 2, 3)
  ```
* 可以切片：`t[1:3]`
* 单元素 tuple：`(1,)` —— 注意逗号！
* 常见用途：函数多返回值：

  ```python
  return x, y
  ```

  * ENGG1330 Notes 提醒：返回 tuple 直接 `print` 时，会带括号。

### 3.2 List（3.2, 5.3）

* 有序、可变：

  ```python
  lst = [1, 2, 3]
  ```
* 常用操作：

  ```python
  lst.append(x)      # 尾部加一个元素
  lst.extend([3,4])  # 追加多个元素（Notes 特别提到这个用法）
  lst.insert(i, x)
  lst.pop()
  lst.remove(x)
  lst.sort()
  lst.reverse()
  ```
* 切片：`lst[a:b:step]` 返回新列表。
* **易错：`append` vs `extend`**

  ```python
  l = [1,2]
  l.append([3,4])   # [1,2,[3,4]]
  l.extend([3,4])   # [1,2,3,4]
  ```

### 3.3 Dictionary（3.3）

* key-value 对，key 必须**可哈希+唯一+不可变**（Notes 有提到“unique immutable key”）。
* 基本操作：

  ```python
  d = {"a": 1, "b": 2}
  d["c"] = 3
  d.get("x", 0)
  d.keys(), d.values(), d.items()
  ```
* 遍历时常用：

  ```python
  for k, v in d.items():
      ...
  ```

### 3.4 Set（3.4）

* 集合：无序、不重复元素。
* 常见操作：

  ```python
  s = {1,2,3}
  s.add(4)
  s.remove(2)
  a | b   # 并集
  a & b   # 交集
  a - b   # 差集
  a ^ b   # 对称差
  ```

---

## 4. 控制流：while / for（3.5, 3.6）

### 4.1 while

```python
while condition:
    ...
```

* 必须保证循环条件**会变化**，否则死循环。
* 常见：输入直到满足条件、计数循环。

### 4.2 for & range & enumerate

```python
for i in range(n):
    ...
for i in range(start, end, step):
    ...
```

* `range(n)` 生成 `0,1,...,n-1`
* **enumerate（Notes 特别提到）**：

  ```python
  for i, value in enumerate(lst):
      ...
  ```

**易错点：**

* 上界是 **不包含的**（off-by-one）。
* 有些题目要求输出“值” vs “长度 `len()`”，Notes 里多次提醒要分清到底问什么。

---

## 5. 字符串（4.x）

### 5.1 基本性质

* 字符串是**不可变**的：不能 `s[0] = 'a'`
* 常见操作：

  ```python
  s[i]      # 索引
  s[a:b]    # 切片
  len(s)
  s + t
  s * n
  ```

### 5.2 常用方法（4.2, 4.3）

* `s.strip()`, `s.lower()`, `s.upper()`
* `s.find(sub)`, `s.index(sub)`
* `s.split()`, `' '.join(list_of_strings)`
* `s.replace(old, new)`

### 5.3 f-string & 格式化（4.4）

```python
name = "Alice"
age = 20
print(f"My name is {name}, age = {age}")
```

* 与 `format`、`%` 相比更简单，注意花括号 `{}`。

### 5.4 例子：简单加密 & 排序（4.5）

* Caesar cipher：给字符加上偏移量；练习：

  * 使用 `ord()/chr()`，循环处理每个字符。
* 字符串排序：用 `sorted(s)` 或对字符串列表调用 `sort(key=...)`。

---

## 6. ID / 引用 / File I/O（5.1, 5.4）

### 6.1 `id()` 与别名

* `id(obj)`：返回对象在内存中的“身份”
* 可变对象（list, dict, set）赋值会产生别名：

  ```python
  a = [1,2]
  b = a     # a, b 指向同一列表，id(a) == id(b)
  ```
* 要复制 list：`b = a[:]` 或 `b = list(a)` 或 `copy.copy(a)`。

### 6.2 文件 I/O（5.4）

基本模板：

```python
# 读取
with open("input.txt", "r", encoding="utf-8") as f:
    data = f.read()          # 整个文件
    # 或 for line in f: ...

# 写入（覆盖）
with open("output.txt", "w", encoding="utf-8") as f:
    f.write("something\n")

# 追加
with open("log.txt", "a", encoding="utf-8") as f:
    f.write("append\n")
```

* 模式：`"r"`, `"w"`, `"a"`, `"rb"`, `"wb"` 等。
* `with` 会自动关文件。

---

## 7. 内建函数 & 模块（6.x）

### 7.1 常见内建函数（6.1）

* `len`, `type`, `int`, `float`, `str`, `list`, `tuple`, `dict`, `set`
* `sum`, `max`, `min`, `sorted`
* `any`, `all`
* `range`, `enumerate`, `zip`
* Notes 里的小实验：对不同对象用 `type()` 看结果；注意类型判断。

### 7.2 模块与 `import`（6.2, Tossing a Coin）

```python
import math
import random
from math import sqrt, pi
```

* `random.randint(a, b)`：**包括 a 和 b**（Notes 特别强调：inclusive）
* Tossing a Coin 例子：用 `random.random()` 或 `randint(0,1)` 模拟实验。

---

## 8. 函数（7.1, 7.2, 11）

### 8.1 函数定义与调用

```python
def func_name(param1, param2=0):
    # docstring (optional)
    ...
    return value
```

* `return` 可以返回单个值或 tuple。
* 没有写 `return` 或 `return` 不带值时，返回 `None`。

### 8.2 参数传递：可变 vs 不可变（7.2）

* 不可变类型（int, float, str, tuple）：

  * 在函数内修改的是**局部变量**，原变量不变。
* 可变类型（list, dict, set）：

  * 在函数内对对象本身的修改（`append`, `pop`, `update`）会影响外面。
  * 易错题：改变 list 元素 vs 重新绑定：

    ```python
    def f(lst):
        lst.append(1)   # 改变原 list

    def g(lst):
        lst = [1,2]     # 重新绑定，不影响外面的变量
    ```

### 8.3 作用域 & `global`（11）

* 函数内部定义的是局部变量；外面看不到。
* 想在函数内部修改全局变量，需要 `global x`（课程中一般不推荐）。

---

## 9. 递归（8）

### 9.1 递归模式

一个典型递归函数有两部分：

1. **Base case（基本情况）**：简单到可以直接给出答案。
2. **Recursive case（递归情况）**：把问题变成一个规模更小的同类问题。

例子：阶乘

```python
def fact(n):
    if n == 0:
        return 1          # base case
    else:
        return n * fact(n-1)  # recursive case
```

### 9.2 常见递归例子

* sum of list
* Fibonacci（了解思路即可）
* Tower of Hanoi（Notes 中特别提到）
* Triominos（10.pdf 中的平面填充问题，典型的分治递归题）

**注意：**

* 一定要有 base case，否则无限递归 -> RecursionError。
* 每次递归必须缩小问题规模。

---

## 10. Searching & Sorting（9.pdf）

### 10.1 线性查找（Linear Search）

```python
def linear_search(lst, target):
    for i, x in enumerate(lst):
        if x == target:
            return i
    return -1
```

* 适用于任何列表（无序也可）。
* 复杂度：O(n)

### 10.2 二分查找（Binary Search）

* 前提：列表**有序**。
* 思路：每次比较中点，丢弃一半。

```python
def binary_search(lst, target):
    lo, hi = 0, len(lst) - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        if lst[mid] == target:
            return mid
        elif lst[mid] < target:
            lo = mid + 1
        else:
            hi = mid - 1
    return -1
```

* 复杂度：O(log n)

### 10.3 排序算法

1. **Bubble Sort（冒泡排序）**
2. **Insertion Sort（插入排序）**
3. **Selection Sort（选择排序）**

重点理解：

* **核心思想 + 外层/内层循环范围**
* **最好/最坏/平均复杂度**通常都是 O(n²)（这些简单排序）

额外：内建排序 `list.sort()` 和 `sorted()` 使用 Timsort，平均 O(n log n)。

---

## 11. Triominos（10.pdf）

* 典型的递归/分治例子：在一个 2^k × 2^k 棋盘上铺 L 形小块，挖去一个方格。
* 思路：

  1. 把棋盘分成 4 个象限。
  2. 中间用一个 L 形块“占据”三个象限的中心方格，把问题分成 4 个更小的子问题。
  3. 对每个子棋盘递归解决。

这题更像“思维训练”，重在理解递归分治思想和二维数组的操作。

---

## 12. 《ENGG1330 Notes.pdf》里的常见陷阱总结

根据我能读取到的零散文字，这个文件主要是在提醒**考试中的 trick points**，可以归纳成几类：

1. **运算相关**

   * 负数取模的结果 pattern
   * 运算符优先级（特别是 `not` / `and` / `or` 的顺序）
   * `//` vs `/` 区别
   * 逻辑表达式里是返回布尔值还是原值（短路）

2. **数据结构 & 函数**

   * `tuple` 的切片、打印形式（带括号）
   * `list.append` vs `list.extend`
   * `enumerate` 的用法
   * 返回值是 tuple 时要怎么解包、怎么打印
   * `id` / aliasing 的问题（同一对象的多个变量）

3. **类型 & 变量**

   * 用 `type()` 测试不同表达式的类型
   * 哪些是合法变量名，哪些不合法（有些故意设计很像）
   * 不要覆盖内建函数名：`str`, `list`, `sum` 等

4. **输出格式**

   * 题目特别强调 `'\n'` 结尾或空格位置
   * 有些题看起来是要“值”，其实是要 `len()`，或者反之（Notes 反复提醒要看清是“特定值还是长度”）

5. **递归 & 算法**

   * Tower of Hanoi 逻辑
   * searching, sorting, recursion 核心思路——要会读伪代码/trace，而不一定要你背完整代码。

---

如果你愿意，我可以在下一步帮你把这份总纲再拆成：

* **「两页 A4」超精简考前速查版**
* 或者按「题型」分类的 checklist（例如“给你一段代码，问输出是什么”时要检查的 10 条规则）。
