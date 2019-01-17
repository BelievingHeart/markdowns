[//]: # (#type_traits #SFINAE #enable_if #tag dispatch)
- [template specification](#template-specification)
- [tag dispatch](#tag-dispatch)
   c++ 14 way of SFINAE
- [template specification](#template-specification)
- [tag dispatch](#tag-dispatch)
- [enable_if at the template list](#enableif-at-the-template-list)
- [enable_if at the argument list](#enableif-at-the-argument-list)
- [enable_if at the return type](#enableif-at-the-return-type)
- [if constexpr](#if-constexpr)
- [check element type within a container](#check-element-type-within-a-container)
   c++ 17 way of SFINAE
- [if constexpr](#if-constexpr) 
- [check element type within a container](#check-element-type-within-a-container)

## template specification
```cpp 
template <typename T>
bool equal(T lhs, T rhs)
{
  return lhs == rhs;
}

template<>
bool equal<float>(float lhs, float rhs)
{
  return true;
}

int main()
{
  bool a = equal(1, 1);
  bool b = equal(4.2f - 0.2f, 4.f); // if specification not implemented, return false
  return a&&b;
}
```

## tag dispatch
```cpp
#include <type_traits>
template<typename T>
bool equal(T lhs, T rhs, std::true_type)
{
    return true;
}

template<typename T>
bool equal(T lhs, T rhs, std::false_type)
{
    return lhs == rhs;
}

template <typename T>
bool equal(T lhs, T rhs)
{
    return equal(lhs, rhs, std::conditional_t<std::is_floating_point_v<T>, std::true_type, std::false_type>{});
 //or return equal(lhs, rhs, std::is_floating_point<T>{});
}

int main()
{
    bool a = equal(1, 1);
    bool b = equal(4.2f - 0.2f, 4.f); 
    return a&&b;
}
```
## enable_if at the template list
```cpp
#include <type_traits>
template<typename T, typename = std::enable_if_t<!std::is_floating_point_v<T>>>
bool equal(T lhs, T rhs)
{
    return true;
}


int main()
{
    bool a = equal(1, 1);
    bool b = equal(4.2f - 0.2f, 4.f); // compile error
    return a&&b;
}
```
## enable_if at the argument list
```cpp
#include <type_traits>
template<typename T>
bool equal(T lhs, T rhs, std::enable_if_t<!std::is_floating_point_v<T>>* = nullptr)
{
    return true;
}


int main()
{
    bool a = equal(1, 1); // subsituton success, the third argument becomes void*
    bool b = equal(4.2f - 0.2f, 4.f); // subsitution failed, compile error
    return a&&b;
}
```
## enable_if at the return type
```cpp
#include <type_traits>

template <typename T>
auto float_only(T arg) -> std::enable_if_t<std::is_floating_point_v<T>,int> // return type is int if ...
{
    return arg;
}

int main()
{
    return float_only(1.f);
}
```

## if constexpr
From my library, `dispatcher.h`:
```cpp
 template <typename T1, typename T2>
    void process(std::pair<T1, T2> p) {
        // The statement within () must be type checking things
      if constexpr (std::is_same_v<T1, float>) { //Note: cppcheck has a bug here. This is not a syntax error
        _dispatcher->insert_outData({p.first,_func(std::move(p.second))});
      } else {
        _dispatcher->insert_outData(_func(std::move(p)));
      }
    }
```

## check element type within a container
[reference from UncleBens](https://stackoverflow.com/questions/1708867/check-type-of-element-in-stl-container-c): **Do not forget ==typename==**
