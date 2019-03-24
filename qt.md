[//]: # (#qt)
# syntax

1. reference qualifier
```cpp
class QString
{
public:
  ... 
  QString toLower() const &; // normal, returns a copy
  QString toLower() &&;      // rvalue, can convert in place!
  ...
};
```

2. qt string concatenation
```cpp
QString s1("Hello ");
QLatin1String s2("you'all ");
QString msg = s1 % s2 % "how are you doing?";
```

# techs
1. Access child by type and name
```cpp
numButtons[i] = Calculator::findChild<QPushButton*>(butName);
```
2. sender recognition in slots
```cpp
// this is a slot
void Calculator::NumPressed(){
    QPushButton* button = static_cast<QPushButton*>(sender());
    ...
}
```