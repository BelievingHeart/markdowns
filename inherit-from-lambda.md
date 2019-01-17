[//]: # (#variadic using #deduction guide #decay_t #visitor #generic lambda)
 1. [conventional implementation](#conventional-implementation)
 2. [variadic implementation](#variadic-implementation) **variadic_using** **deduction_guide** **decay_t**
 3. [visitor that inherit from lambda](#visitor-that-inherit-from-lambda) **visitor**
 4. [visitor that combines generic lambda and constexpr](#visitor-that-combines-generic-lambda-and-constexpr) **generic_lambda**
 5. [the final version of visitor](#the-final-version-of-visitor)

## conventional implementation
```cpp
#include <type_traits>
#include <iostream>

template <typename L1, typename L2>
struct LambdaCombined : L1, L2
{
    using L1::operator();
    using L2::operator();
    LambdaCombined(L1 l1, L2 l2)
            :L1(std::move(l1)),L2(std::move(l2)){}
};

int main()
{
  auto l1 = []{return 5;};
  auto l2 = [](int i){return 10*i;};
  LambdaCombined lambda{l1,l2};
  std::cout<<lambda()<<'\n'<<__TIME__;
  return lambda();
}
```

## variadic implementation
```cpp
#include <type_traits>
#include <iostream>
#include <memory>

template <typename ...B>
struct LambdaCombined : B...
{
    // variadic using syntax
    using B::operator()...;
    
    template<typename ...L>
    LambdaCombined(L&&...l)
    :B(std::forward<decltype(l)>(l))...{}
};

// class template deduction guide
template<typename...T>
LambdaCombined(T...) -> LambdaCombined<std::decay_t<T>...>;

int main()
{
    auto l1 = []{return 5;};
    auto l2 = [](int i){return 10*i;};
    LambdaCombined lambda{l1,l2,     // by copy
        [ptr = std::unique_ptr<int>()](float f){return f/10.f;}  // by move
    };
    std::cout<<lambda(629.f)<<'\n';
    return lambda();
}
```

## visitor that inherit from lambda

```cpp
#include <type_traits>
#include <iostream>
#include <memory>
#include <variant>
#include <array>
#include <algorithm>

template <typename ...B>
struct Visitor : B...
{
    // variadic using syntax
    using B::operator()...;
    
    template<typename ...L>
    Visitor(L&&...l)
    :B(std::forward<decltype(l)>(l))...
    {}
};

// deduction guide
template<typename...T>
Visitor(T...) -> Visitor<std::decay_t<T>...>;

int main()
{
    std::array<std::variant<int, double, std::string>, 5> arr{1, 2.3, 4, "hello", 5};
    
    // count numbers of individual type using Visitor
    int int_count = 0, string_count = 0, double_count = 0;
    Visitor visit_count{
        [&int_count](const int& arg){int_count++;},
        [&string_count](const std::string& arg){string_count++;},
        [&double_count](const double& arg){double_count++;},
    };
    std::for_each(std::begin(arr), std::end(arr), [&visit_count](const auto& v){
        std::visit(visit_count, v);
        });
    for(const auto& ele : {int_count, string_count, double_count})
    {
        std::cout<<ele<<' ';
    }std::cout<<'\n';
    
    return int_count;
}
```

## visitor that combines generic lambda and constexpr
```cpp
#include <type_traits>
#include <iostream>
#include <memory>
#include <variant>
#include <array>
#include <algorithm>

int main()
{
    std::array<std::variant<int, double, std::string>, 5> arr{1, 2.3, 4, "hello", 5};
    
    // count numbers of individual type using Visitor
    int int_count = 0, string_count = 0, double_count = 0;
    auto visit_count = [&int_count, &string_count, &double_count](const auto& value){
        if constexpr(std::is_same_v<int, std::decay_t<decltype(value)>>){
            int_count++;
        }else if constexpr(std::is_same_v<double, std::decay_t<decltype(value)>>){
            double_count++;
        }else{
            string_count++;
        }
    };
    std::for_each(std::begin(arr), std::end(arr), [&visit_count](const auto& v){
        std::visit(visit_count, v);
        });
    for(const auto& ele : {int_count, string_count, double_count})
    {
        std::cout<<ele<<' ';
    }std::cout<<'\n';
    
    return int_count;
}
```

## the final version of visitor
```cpp
#include <iostream>
#include <variant>

template <typename ... Base>
struct Visitor : Base ...
{
    using Base::operator() ...;
};

template <typename ... T>
Visitor(T ...) -> Visitor<T ...>;

int main()
{
    constexpr auto visitor = Visitor{
        // Note that the return type of every lambda should be the same
            [](int a)->int{return a+10;},
            [](double a)->int{return 10.0*a;}
    };

    std::cout<<std::visit(visitor, std::variant<int, double>{9.0})<<'\n';
}
```

