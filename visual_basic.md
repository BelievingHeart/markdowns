[//]: # (#vb #visual basic)

# weirdos
1. Arithmetic operations
- `/`: floating point divide
- `\`: integer divide, simple truncate
- `Mod`: modulus
- `^`: exponentiation

2. `Public` and `Private`
- Very alike with C++ while using in Class
- In Module, `Private` means `static` in C++ while `Public` variables can be shared with other translation units

3. `&` means string concatenation
- concat string with string
- concate string with number

4. numbers can be implicitly convert to string
- string can alse be implicitly convert to number
- `&=` supported

5. `vbCrLf` is the new line constant

6. Array like std::vector
- resize
```vb
Dim arr(10) As Integer
arr(1) = 100
Redim Preserve arr(50) ' Preserve original values
Redim arr(0 TO 4) ' throws away original values

Dim members = new Strings(){"Bob", "Jone", "Barber"} ' immediate initialization
```

7. Stack
- declare
```vb
Dim theStack As Stack(of String)
```
- declare and default initialize
```vb
Dim theStack As New Stack(of String)()
```

8. List
- declare and initialize
```vb
Dim theList As new List(of Integer)() = {1, 2, 3}
```

9. Dictionary
- declare and default initialize
```vb
Dim dict As new Dictionary(of String, Interger)()
```

10. stack and queue can not be initialized with initializer list

11. use `Stop` keyword to make a breakpoint

12. passing parameters
```vb
Public Sub func(input As Integer) ' == byVal input As Integer
    ...
End Sub

Public Function func1(ByRef arr() as Integer) As Integer
    ...
End Function
```

13. Explicitly converting enumerations to String gets ==text==
```vb
Public Enum Vehicle
    Car
    Plane
End Enum

Dim v As new Vehicle() = Vehicle.Car
MessageBox.show(v) ' Shows 0
MessageBox.show(v.toString()) 'Shows "Car"
```

14. Default arguments
- Default parameter must come last with an `optional` keyword
```vb
Public Sub func(ByVal i As Interger, Optional ByRef j As String = "hello")
```

15. Variadic arguments
```vb
' declare
Public Function sum(ParamArray values() as Single) As Single
    Dim total As Single = 0
    for each value As Single In values
        total += value
    Next
    return total
End function

' invoke
Dim total As Single = sum(1,2,3,4)
```

16. trivially initialize an object
```vb
Class Person
    Public name, city, street As String
End Class

Dim Jone As Person with{
    .name = "Jone",
    .city = "Shenzhen",
    .street = "Dalang"
}
```

17. Simple Events
- An event exists in a class A like a method
- Just declare, no implmentation
- to raise the event, use `RaiseEvent` keyword
- to handle the event, first delclare `Public/Private WithEvent obj As A` in the Class that will handle the event
```vb
Class A
    Public event someSignal() ' Declare an event

    Public Sub someMethod_that_raisesEvents()
        if some_condition
            RaiseEvent someSignal()
        End if
    End Sub
End Class

Class B
    Public WithEvents a As A ' Declare a with events

    ' To handle a particular event of a, select the dropdown of Class A then select that event
```

18. Detailed Events
- A detailed event is raised and handled with informations associated with **Who raise the event** and **The information of the event**
- The event-raiser passes in `Me` as the first argument of the event to specify **Who raise the event**
- **The information of the event** is packed in other class call `args`

19. reference type
- value types: basic data types
- reference types: containers, the second argument of any events

20. shadow and override
```vb
' shadow
Public shadows Sub funcName()

End Sub

' override, first the base class should has the same method with keyword `overridable`
Public overrides Sub funcName()

End Sub
```

21. abstract vs interface, inherits vs implements
- `abstract` and `interface` in C++ refers to the same thing, `c++ abstract`. While in vb, `abstract` == `c++ non-pure abstract`, `interface` == `c++ pure abstract`
- In vb, a class *inherits* from `abstract` class and *implements* `interface` class
- Both *inherits* and *interface* create a child class that can be bound to a parent class.

22. string formatting
    ```vb
        $"This is a number: {value}"
    ```

23. ternary expression
    ```vb
        Dim isGrownUp As Boolean = if(age > 18, true, false)
    ```

24. type checking
    ```vb
    if TypeOf Me.ActiveControl is Button Then Me.Close()
    ```


## file parsing
```vb
fileOpen(1, "hello.txt", openMode.output) 'openMode.output overides existing file
printLine(1, "hello world") ' write to "hello.txt"
fileClose(1)
```

## sort
1. list sort
```vb
Dim players as new List(of Player)
' TODO: initialize players

players.sort(function(a, b) a.x.compareTo(b.x))
```
```vb
newPlayers = players.OrderBy(Function(a) a.x).ToList()
```

## select
- Description: select a subset of a collection(or container)
```vb
        ' Player has 3 members: x,y,z
        Dim players As New List(Of Player)
        Const numPlayer As Integer = 10

        for i As Integer = 0 To numPlayer
            players.Add(New Player(i, 10 - i, 0))
        Next

        ' "where" is used to filter samples "select" is used to filter features
        Dim players_subset = From p As Player In players
                where p.y > 5
                Select p.x, p.y
                Order by p.x ' sort with "Order by" keyword

        for Each p in players_subset
            console.WriteLine(p.y)
        Next
```

## lambda expression
```vb
Dim say = Sub(message As String)
                MessageBox.Show(message)
            End Sub
say("hello")
```

## generic programming
1. class
```vb
Public Class PriorityQueue(of T)
...
End Class
```
2. function
```vb
Public Sub say(of T)(ByRef t1 As T, ByRef t2 As T)
...
End Sub
```

## overide method
```vb
Public Overrides Function ToString() As String
' String is of ref type, the returned thing is a reference
    return firstName & " " & lastName
End Function
```