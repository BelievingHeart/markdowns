[//]: # (#cs #CSharp #C# #c# )
## sytax
1. Pass by array VS variadic length argument list
    ```cs
    void take_variadic_ints(params int[] args); // variadic argument list, treat them as normal array inside the callee
    void take_an_array(int[] args); // Equals to passing the pointer to the first element of the array
    ```

2. `ref` and `out` keyword
    ref tells the compiler that the object is initialized before entering the function, while out tells the compiler that the object will be initialized inside the function.

    So while ref is two-ways, out is out-only
    ```cs
    // The original pointer dosen't get copied and it is redirected to point to a new address
    void take_ref_of_pointer(ref int[] args){
        args = new []{5, 6, 7};
    }
    void take_copy_of_pointer(int [] args){
        args = new []{5, 6, 7}; // Only the copy of original pointer is redirected
    }

    static void Main(){
        int[] array = {1,2,3};
        take_copy_of_pointer(array); // After this array remains {1,2,3}
        take_ref_of_pointer(array); //After this array becomes {4,5,6}
    }
    ```

3. property set
    ```cs
    public int y
    {
        get => y;
        // `value` is a speciel variable that always refers to the right operand to the set expression
        set => y = value;
    }
    ```

4. `abstract` keyword
    (1) An abstract class can only be declare but not instantiate. That is, in the C++ view, a pointer of derived class can bind to that of its abstract class.
    (2) An abstract method has no implementation. If any class has any method declared abstract, the class itself must be declared abstract. A class that inherits from an abstract class with abstract methods but not actually implements all the abstract methods can't be instantiated.

5. `is` keyword
    ```cs
    // Class Player is derived from class Entity
    Entity e = new Player();
    Console.WriteLine(e is Player); //True
    Console.WriteLine(e is Entity); //True
    var p = (Player)e;
    Console.WriteLine(p is Player); //True
    Console.WriteLine(p is Entity); //True
    ```

6. `sealed` keyword
    `sealed` == `final` in C++

7. `interface`
    (1) No fields
    (2) No implementations
    (3) Methods declared in interface should not have `modifier`s
    `abstract`
    (1) Can have common data and functionalities(methods with implementation)
    (2) A class can only inherits from a single abstract class.

8. `LINQ` keywords
    ```txt
    (1) from <item> in <collection>
    (2) let <element> = item.getElement()
    (3) where <element[.attribute] satisfies some condiction>
    (4) orderby <element[.attribute]> [,<element[.attribute2]>...] [descending\ascending]
    (5) select <element[.attribute]> || select new {element.attribute1, element.attribute2 ...}
    ```
9. `LINQ projection` happens when we select an property of the element rather than the element itself.
    ```cs
    // The last statement of LINQ:
    select element.attribute1;
    ```

10. `LINQ` creates anonymous objects:
    ```cs
    // The last statement of LINQ:
    select new {a1 = element.attribute1, element.attribute2 ...};
    ```

11. `defer execution` of `LINQ`
    A `LINQ` structure works like a functor that takes as *reference* a thing that implements `IEnumerable`. It gets invoked only when it is iterated through by for-loop or foreach-loop.

12. extension methods


## terms
1. `concrete class`: A class that can be instantiated. If a class inherites from a abstract class, in order to become concrete class, it must implement all the abstract methods. If a class implements an interface, it must implements all the interface methods to become a concrete class.
2. `modifier`: it refers to 3 keywords: `public`, `private` and `protected`