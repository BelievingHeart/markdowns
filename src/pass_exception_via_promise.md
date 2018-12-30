```cpp
#include <future>
#include <iostream>
#include <exception>

int main()
{
    auto pr = std::promise<std::string>();
    auto fut = pr.get_future();
    auto set_promise = [&]() {
        std::cout << "Setting promise...\n";
        try
        {
            throw std::runtime_error("Exception from thread");
        }
        catch (...)
        {
            pr.set_exception(std::current_exception());
        }
    };
    auto t = std::thread(set_promise);
    std::cout << "Waiting for promise...\n";
    try
    {
        const auto str = fut.get();
        std::cout << "Got promise: " << str << '\n';
    }
    catch (const std::runtime_error &e)
    {
        std::cout << "Exception from promise: " << e.what() << '\n';
    }

    t.join();
    return 0;
}
```