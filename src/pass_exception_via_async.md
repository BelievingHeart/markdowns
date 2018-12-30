```cpp
#include <exception>
#include <future>
#include <iostream>

int main() {
  auto set_promise = [](bool throw_or_not) {
    if (throw_or_not) {
      std::cout << "Throwing from thread\n";
      throw std::runtime_error("Exception form thread");
    } else {
      return std::string("Hello from thread");
    }
  };
  auto fut = std::async(set_promise, true);
  std::cout << "Waiting for promise...\n";
  try {
    const auto str = fut.get();
    std::cout << "Got promise: " << str << '\n';
  } catch (const std::runtime_error &e) {
    std::cout << "Exception from promise: " << e.what() << '\n';
  }
  return 0;
}
```