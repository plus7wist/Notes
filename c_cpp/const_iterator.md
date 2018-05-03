# C++0x 容器的常量迭代器改进建议

http://www.open-std.org/JTC1/SC22/WG21/docs/papers/2004/n1674.pdf

## 引入

C++11 给出了 `auto` 关键字，可以简化类型推导。C++0x 时代的迭代器遍历可以按照如下的样子简化：

```c++
for (std::vector<T>::iterator it = v.begin(); it != v.end(); ++it) {
    // working with it
}
for (auto it = v.begin(); it != v.end(); ++it) {
    // working with it
}
```

但是当循环不需要修改 v 的对象，而只是读取，那么常见的合适实践是使用常量迭代器。

```c++
for (std::vector<T>::const_iterator it = v.begin(); it != v.end(); ++it) {
    // working with it
    // read only
}
```

然而，这种遍历难以用 `auto` 简化。

这主要的矛盾是 `const_iteator` 和 `const iterator` 是两个不同的类型。`const auto` 不能得到 `const_iterator`。事实上，迭代器作为一个类似指针的对象，它的 const 限定限定在指针本身上，而 `const_iterator` 限定在指针指向的内容上。

这个问题在使用泛型算法的时候也会引发不适。`std::for_each(v.begin(), v.end(), task)` 中，如果 v 不是常量类型，算法对 v 的使用是否是只读的，取决于 task 的声明。

## 建议

建议扩充容器的接口，提供 cbegin 和 cend，用以显式访问常量迭代器。

## 设计选项

1. 提供新的成员函数。

   ```c++
   for (auto it = v.cbegin(); it != v.cend(); ++it) {
       // read only
   }
   ```

2. 提供泛型适配器

   ```c++
   template<class C>
   inline typename C::const_iteator cbegin(C const &c) {
       return c.begin();
   }
   ```

   这个解法十分简洁，而且不需要修改容器。只不过它不太符合 C++ 的设计习惯，导致 begin 和 cbegin 不对称。

   提供一个函数而不是成员函数，也就允许用户重载。特别是这种做法还可以适配原生数组，只要提供这样一个重载。

   ```c++
   template<class T, size_t N>
   inline T const *cbegin(T const (&a)[N]) {
       return a;
   }

   template<class T, size_t N>
   inline T const *cend(T const (&a)[N]) {
       return a+N;
   }
   ```

   允许这种重载是优点还是缺点取决于看问题的角度。如果 cbegin 设计为泛型适配器，那么 begin 和 rbegin 等也需要设计类似的泛型适配器。

最终 C++11 提供了成员函数版本的 cbegin/cend，同时提供了泛型适配器的 begin/end。C++14 给出了它们对数组的支持，并且添加了 cbegin 和 cend（还有对应的反向迭代器）的泛型适配器。
