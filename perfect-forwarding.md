[//]: # (#std::forward #forwarding referenc #perfect forwarding)
```cpp
#include <iostream>

struct X
{
    X() = default;
    X(X&&) {std::cout << "Moving...\n";};
    X(const X&) {std::cout << "Copying...\n";}
};

template <typename T>
void forwardRef_stdForward(T &&x)
{
  g(std::forward<T>(x));
}

template <typename T>
void forwardRef(T &&x)
{
  g(x);
}

template <typename T>
void forwardRef_stdForward_forwardRef(T &&x){
  h(std::forward<T>(x));
}

template <typename T>
void forwardRef_forwardRef(T &&x){
  h(x);
}

template <typename T>
//void g(T x)   // Accept by value
void g(const T& x)  //Accept by genetic reference
{ }

template <typename T>
void h(T&& t){
}

int main()
{
  
  X x;
  std::cout << "rvalue will be moved if std::forward exists at the end of forwarding pipeline\n";
  forwardRef_stdForward(X{}); // moving
  forwardRef(X{}); // copying

  std::cout << "std::forward in between two forwarding references is redundant\n"
  << "No copy or move will happen within the forwarding pipeline\n";
  forwardRef_stdForward_forwardRef(x);
  forwardRef_forwardRef(x);
  forwardRef_stdForward_forwardRef(X{});
  forwardRef_forwardRef(X{});

  std::cout << "lvalue will be copied at the end of forwarding pipeline regardless of the last std::forward\n";
  forwardRef_stdForward(x); // copying
  forwardRef(x); // copying
}
```