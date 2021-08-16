# C# Notes:notebook_with_decorative_cover: Overview
The notes when I learned C#. It could also be a reference manual applied to daily basis.

`Quick Reference` is for you to recall the knowledge at once.

`Complete Notes` is for you to check the details.



# Table of Content

- Overview
- Recommend Books
- Quick Reference
  - C# Step by Step
  - C# in Depth
  - CLR via C#
- Complete Notes
  - Microsoft Visual C# Step by Step
  - C# in Depth
  - CLR via C#



# Recommend Books

| Book                             | Image                                                        | Level              |
| -------------------------------- | ------------------------------------------------------------ | ------------------ |
| Microsoft Visual C# Step by Step | <img src="https://raw.githubusercontent.com/miloyip/game-programmer/master/images/mvcsharpstepbystep8.jpg" style="zoom:33%;" /> | :star:             |
| C# in Depth                      | <img src="https://raw.githubusercontent.com/miloyip/game-programmer/master/images/csharpindepth3.jpg" style="zoom: 33%;" /> | :star::star:       |
| CLR via C#                       | <img src="https://raw.githubusercontent.com/miloyip/game-programmer/master/images/clrviacsharp4.jpg" style="zoom: 33%;" /> | :star::star::star: |



# Quick Reference

## C# Step by Step

### 1.Welcome to C#

1.1 Create a new **console application** using Visual Studio 2017

> ​	File - New - Project(Ctrl+Shift+N)
>
> ​	Select `Console App(.NET Framework)`

1.2 Create a new Universal Windows app

> ​	File - New - Project(Ctrl+Shift+N)
>
> ​	Select `Blank App (Universal Windows)`

1.3 Build the application

> ​	Build - Build Solution(Ctrl+Shift+B)

1.4 Run the application in debug mode

> ​	Debug - Start Debugging(F5)

1.5 Run the application without debugging

> ​	Debug - Start without debugging(Ctrl+F5)



### 2.Variables, operators, and expressions

2.1 Declare a variable

> ​	The code of declaration is in the following order:
>
> ​	data type -> variable name -> semicolon
>
> ​	`[type] [name];`
>
> ​	`int year;`

2.2 Declare a variable and give it an initial value

> ​	data type -> variable name -> assignment operator -> initial value -> semicolon
>
> ​	`[type] [name] = [value];`
>
> ​	`int year = 2021;`

2.3 Change the value of a variable

> ​	variable name -> assignment operator -> expression calculating the new value(right hand side)
>
> ​	`[name] = [right hand side]`
>
> ​	`year = 2020;`

2.4 Generate a string representation of the value in a variable

> ​	Using `To.String()` method

```c#
int intVar = 13;
string strVar = intVar.ToString.();
```

2.5 Convert a `string` to an `int/double`

> ​	Using `System.Int32.Parse` or `System.Double.Parse`
>
> ​	`int.Parse` and `double.Parse` for short

```c#
string strPI = "3.14159";
string strThirdteen = "13";
double dPI = double.Parse(strPI);
int thirdteen = int.Parse(strThirdteen);
```

2.6 Override the precedence of an operator

> ​	a.k.a. value inside the bracket computed first
>
> ​	`(3 + 5) * 2`

2.7 Assign the same value to several variables

> ​	the value is passed from right to left

```c#
int myInt4, myInt3, myInt2, myInt;
myInt4 = myInt3 = myInt2 = myInt = 10;
```

2.8 Increment or decrement a variable

> ​	using `++` or `--`
>
> ​	e.g.	`count++;`



### 3.Methods and applying scope

3.1 Declare a method

> ​	write inside the class

```
[return type] [method name] (date_type value1, data_type value2)
{
	//
}
```

> ​	e.g  :

```c#
int addValue(int leftHandSide, int rightHandSide)
{
    //
}
```

3.2 Return a value from within a method

> ​	use `return` key word

```c#
int addValue(int leftHandSide, int rightHandSide)
{
    return leftHandSide + rightHandSide;
}
```
> ​	Tips: even though you don't have to include a `return` at the end of a `void` function, it is suggested to do so. Since every method should return somethin. `void` method `return` void.

```c#
public void Method()
{
	//do something here...
    return;
}
```

3.3 Return multiple values from within a method

> ​	return multiple values as a tuple

```c#
(int min, int max) FindMinMax(int[] input)
{
	// finding min and max
    return (min, max);
}
```

> ​	then the function returned multiple values can be used like this:

```c#
var input = new[] { -9, 0, 67, 100 };
var (minimum, maximum) = FindMinMax(input);
```

3.4 Return from a method before the end of the method

> ​	nothing special, but to remember, to block ends at where `return` is.

```c#
void PrintSomething()
{
    Console.WriteLine("1");	// √
    Console.WriteLine("1");	// √
    return;
    Console.WriteLine("3");	// x(this won't be printed.)
}
```

3.5 Define an expression bodied method

> ​	a.k.a. it just replace the `{}` and `return` by using `=>`

```c#
double CalculateFee(double dailyRate, int days)
{
    return dailyRate * days;
}
```

> ​	it will be:

```c#
double CalculateFee(double dailyRate, int days) => dailyRate * days;
```

3.6 Call a method

> ​	nothing special, just put the `methodName(argument1, argument2, ...);`

```c#
addValues(39, 3);
```

3.8 Use the Generate Method Stub Wizard

> ​	double click the method, right click, `Quick Action and Refactoring`(Ctrl+,)

3.9 Create a nested method( method in method )

> ​	as you can see there is a method `factorial` inside the method `CalculateFactorial`.

```c#
long CalculateFactorial(string input)
{
    //...
    long factorial(int dataValue)
    {
        if (dataValue == 1)
        {
            return 1;
        }
        else
        {
            return dataValue * factorial(dataValue - 1);
        }
    }
}
```

3.10 Display the Debug toolbar

> ​	anytime you can't find the icon of your tool. Go to **View - Toolbar** ...
>
> ​	in this case, **View - Toolbar - Debug**

3.11 Step into a method

> ​	

3.12 Step out of a method

3.13 Specify an optional parameter to a method

> ​	nothing special, just give an initial value when you define it

```c#
void optMethod(int first, double second = 0.0, string third = "Hello")
{
    //...
}
```

3.14 Pass a method argument as a named parameter

> ​	Since you already have some default argument, you don't want to assign it again...

```c#
optMethod(first: 100, third: "World");
```

> ​	as you can see, you can skip typing something for `second`.



### 4.Decision statements

4.1`==`, `!=` determine equivalent

```c#
thisYear == 2021;
```

4.2`>, >=, <, <=`Compare the value of two expressions

```c#
bool flag = 13 > 23;
```

4.3Declare a Boolean variable

```c#
bool isOdd;
```

4.4`AND` true

> ​	use `&&`

```c#
inRange = (lo <= number) && (number <= hi);
```

4.5`or` true

> ​	use `||`

```c#
outOfRange = (number < lo) || (hi < number);
```

4.6`if` statement

> ​	in short(not recommend)::x:

```c#
if (inRange)
	process();
```

> ​	complete written(recommend)::heavy_check_mark:

```c#
if (inRange)
{
    process;
}
```

4.7`switch` statement

> ​	it is sort of a gate, which controls the output

```c#
int choice;
switch(choice)
{
    case 0:
        //do something (if choice== 0)
        break;    
    case 1:
        //do something (if choice== 1)
        break;    
    default:
        //do something (if (choice !==0 && choice!=1))
        break;
}
```

> ​	tips: always leave `default` value



### 5.Compound assignment and iteration statements

5.1What is compound assignment

> ​	It is a shortcut for arithmetic operation and assignment.

```c#
variable += 13;  //equivalent to variable = variable + 13;
variable -= 10;  //equivalent to variable = variable - 13;
variable *= 13;  //equivalent to variable = variable * 13;
variable /= 13;  //equivalent to variable = variable / 13;
```

> ​	However, if there is multiple variable on the right hand side. I personally not recommend this shortcut.

5.2`while` loop

> ​	`while` something is `true`, do something

```c#
int i = 0;
while(i < 10)
{
    Console.WriteLine(i);
    i++;  //Please don't forget increment the condition!
}
```

5.3`for` loop

> ​	`[local variable]; [termination condition]; [incrementation(sometimes decrease)]`

```c#
for (int i = 0; i < 10; i ++)
{
    Console.WriteLine(i);
}
```

> ​	sometimes you can iterate backward or increment based on 2

```c#
for (int i = 10; i > 0; i--)
{
    //do something...
}
for (int i = 0; i < 10; i+=2)
{
    //do something...
}
```

5.4`do-while` loop

> ​	the difference between `do-while` loop and `while` loop is that: **`do-while` loop iterate at least once.**

```c#
int i = 0;
do
{
    Console.WriteLine(i);
    i++;
}
while(i < 10);
```



### 6.Errors and exceptions

6.1 Catch a specific exception

> ​	if you want to catch **specific** exception, you have to specify the type of exception

```c#
try
{
    //do something...
}
catch(FormatException fEx)
{
    //do something...
}
```

> ​	in convention, we denote `exception` to be `??Ex`

6.4 Catch all types of exceptions with one call

> ​	use `Exception` to cover all types of exception

```c#
try
{
    //do something...
}
catch(Exception ex)
{
    //do something...
}
```

6.2 Use `checked` to prevent overflow

> ​	 this is very handy in arithmetic computation for it prevent overflow

```c#
int number = Int32.MaxValue;
checked {number++};  //in this case, the overflow error will be caught
```

6.3 Throw an exception

> ​	use `throw` keyword

```c#
throw new FormatException(source);
```

6.4 Ensure code will always run even though with an exception

> ​	this is very handy

```c#
try
{
    //do something..
}
finally
{
    //this will be run no matter there is an exception above
}
```



### 7.Class and objects

7.1 Declare a `class`

```c#
class className
{
    //..
}
```

7.2 Declare a `constructor`

> ​	Write a method whose name is the same as the name of the class, and that **has no return type**

```c#
class Point
{
    //..place the field at here
    public Point(int x, int y)
    {
        //..
    }
}
```

7.3 Call a `constructor`

> ​	Use the `new` keyword and specify the constructor with an **appropriate set of parameters**

```c#
Point origin = new Point(10, 10);
```

7.4 Declare a `static` method

> ​	use the `static` keyword;  a `static` method is that you can call this method without initializing an instance of this class.

```c#
class Point
{
    //...
    public static int ObjectCount()
    {
        //...
    }
}
```

7.5 Call a `static` method

> ​	to call a `static` method, just : `[ClassName].[staticMethodName]`

```c#
int pointsCreatedSoFar = Point.ObjectCount();
```

7.6 Declare and acess a `static` field

```c#
class Point
{
    //...
    public static int ObjectCount;
}
```

> ​	and you can acess the static field by invoke it directly

```c#
int num = Point.ObjectCount;
```

7.7 Declare a `const` field

> ​	`const` is a constant value

```c#
class Math
{
    //...
    public const double PI = 3.14159;
}
```



### 8.Values and references

8.1 Copy a **value type** variable

> ​	when you copy value type, there are two distinct copies

```c#
int i = 13;
int copyi = i;
i++; //the change won't affect `copyi`
```

8.2 Copy a **reference type** variable

> ​	when you copy a reference type, you actually copied the `reference` of the variable

```c#
Curve arcCrv = new Curve();
Curve crv = arcCrv;
arcCrv.Translate();  //this not only translates `arcCrv` but also `crv`.
```

8.3 Declare a variable that can hold a value type or the `null` value

> ​	use `?` modifier

```c#
int? i = null;
```

8.4 Pass an argument to a `ref` parameter

> ​	the key word `ref` simply implies that the change will affect itself

```c#
static void doIncrement(ref int number)
{
    number++;
}
int i = 42;
doIncrement(ref i);  //i is changed
```

> ​	although the function `doIncrement` is a `void` function which returns nothing, 
>
> ​	we should pay attention to `ref` keyword. In this case, the `i` was incremented.

8.5 Pass an argument to an `out` parameter

> ​	it is very similar to `ref` keyword, my way to perceive this is that whenever you see `out`,
>
> ​	it is a decoration for output, you have to *prepare something for the output*.

```c#
using System.Linq;
static void duplicateTenTimes(int i, out List<int> duplicatedList)
{
    duplicatedList = Enumerable.Repeat(i, 10).ToList();
}

List<int>tenDuplicate = new List<int>();
duplicateTenTimes(10, out tenDuplicate); //at this point, the `tenDuplicate` has 10 copies of 10.
```

8.6 Box and unbox a value

> ​	you can see `box` as a way wrapping anything to a generic type, 
>
> ​	in this case we use `object`

```c#
object o = 42;
```

> ​	respectively, you can see `unbox` as way casting the generic type to specific type

```c#
int i = (int)o;
```

8.8 Cast an object safely

> ​	1.First choice, use `is` keyword to check if the cast success

```c#
WrappedInt wi = new WrappedInt();
//...
object o = wi;
if (o is WrappedInt temp)
{
	//...
}
```

> ​	2.Second choice, use `as` to perform the cast, and check if it is `null`

```c#
WrappedInt wi = new WrappedInt();
//...
object o = wi;
WrappedInt temp = o as WrappedInt;
if (temp != null)
{
    //...
}
```



### 9.Enumerations and structures

:star: Remember, the biggest difference between `struct` and `class` is that: **Structs are value type** whereas **Classes are reference type**.

9.1 Declare an enumeration

> ​	use the `enum` keyword => name of this `enum` => enumeration **literal** names

```c#
enum Days = {Sunday, Monday, Tuesday, Wednesday, Thursday, Friday};
```

9.2 Declare an enumeration variable

```
Days today;
```

9.3 Assign an enumeration variable to a value

```c#
today = Sunday;		//WRONG!! on the rhs, the compiler can't detect what is "Sunday" literally.
today = Days.Sunday;//Correct.
```

9.4 Declare a structure type

> use the keyword `struct` => the name of the `struct` =>  the body of the `struct` (the constructors, methods, and fields).  [similar to class]

```c#
struct Point3d
{
    internal double _x, _y, _z;
    public Point3d(double x, double y, double z)
    {
        this._x = x;
        this._y = y;
        this._z = z;
    }
}
```

9.5 Declare a structure variable

```c#
Point3d pt;
```

9.6 Initialize a structure variable to a value

> ​	nothing special, similar to `class`

```c#
Point3d = new Point3d(0, 1, 2);
```



### 10.Arrays

> ​	:star: What is the biggest difference betweem `Array` and `List`?
>
> ​			`Array` is fixed size once it is initialized. `List` is dynamic, you can `either` add or `remove` items from it.

10.1 **Declare** an array variable

> ​	[data_type] [name_of_array];

```c#
bool[] flags;
```

10.2 **Create an instance** of an array

> ​	when you create an **instance**, you have to explicitly define the amount of the array.

```c#
bool[] flags = new bool[10];
```

10.3 **Initialize** the elements of an array to specific values

> ​	when you **initialize** the array, you have to assign specific values

```c#
int[] numPI = {3, 1, 4, 1, 5, 9};
```

10.4 Find how many elements in an array

> ​	use `Length` property

```c#
int[] numPI = {3, 1, 4, 1, 5, 9};
int numPIAmount = numPI.Length;  //here you got 6
```

10.5 Access a single array element

> ​	use the `[]` to access particular element

```c#
int num = numPIAmount[2];  //here you got 4
```

10.6 Loop over an array

> ​	use `for` loop or `foreach` loop

```c#
bool[] flags = { true, false, true, false };
for (int i = 0; i < flags.Length; i++)
{
    Console.WriteLine(flags[i]);
}
foreach (bool flag in flags)
{
    Console.WriteLine(flag);
}
```

10.7 Declare a **multidimensional array** variable

> ​	use something like this `[,]`

```c#
int[,] table;
table = new int[4, 6];  //initialize an 4*6 array
```

10.8 Declare a **jagged array** variable

> ​	use something like this `[][]`

```c#
int[][] items;
items = new int[4][];
items[0] = new int[3];
items[1] = new int[10];
items[2] = new int[40];
items[3] = new int[25];
```

:star: Intuitively, the difference between *multidimensional array* and *jagged array* is that the

*multidimensional array* is like a **square** with anything aligned.

*jagged array* is like zig-zag **non-symmetric shape**.

```c#
public class ArrayHolder
{
    int[,] multiDimArray =  {{1,2,3,4},
                             {5,6,7,0},
                             {8,0,0,0},
                             {9,0,0,0}
                            };
    int[][] jaggedArray = { new int[] {1,2,3,4},
                            new int[] {5,6,7},
                            new int[] {8},
                            new int[] {9}
                          };
}
```



### 11.Parameter arrays

> ​	By using the `params` keyword, you can specify a [method parameter](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/method-parameters) that takes **a variable number of arguments**. :warning: However, the parameter type **must be a single-dimensional array**.

```c#
public class MyClass
{
    public static void IntParams(params int[] list)  //with `params` keyword, the length of array can be dynamic
    {
        for (int i = 0; i < list.Length; i++)
        {
            Console.Write(list[i] + " ");
        }
        Console.WriteLine();
    }
    public static void objParams(params object[] list)
    {
        for (int i = 0; i < list.Length; i++)
        {
            Console.Write(list[i] + " ");
        }
        Console.WriteLine();
    }

    static void Main()
    {
        //output: 1 2 3 4
        IntParams(1, 2, 3, 4);
        
        //output: 1 a test
        objParams(1, 'a', "test");

        //output: a blank line
        objParams();

        //output: 5 6 7 8 9
        int[] myIntArray = { 5, 6, 7, 8, 9 };
        IntParams(myIntArray);  //the length can be varied

        //output: 2 b test again
        object[] myObjArray = { 2, 'b', "test", "again" };
        objParams(myObjArray);  //you can pass different types elements in it

        // output: error!!! no output!!
        IntParams(myObjArray);  //this cannot be compiled
        
        //output: System.Int32[]
        objParams(myIntArray);  // No error, but!! the entire integer array becomes the 1st element of the params array.
    }
}
/*
Output:
    1 2 3 4
    1 a test

    5 6 7 8 9
    2 b test again
    System.Int32[]
*/
```



### 12.Inheritance

12.1 Create a derived class from a base class

> ​	use the colon `:`

```c#
class BaseClass
{
    public BaseClass(int x, int y)
    {
        //ctor...
    }
}

class DerivedClass : BaseClass
{
	public DerivedClass(int x, int y) : base(x, y)
    {
    }
    // if you want to inherit the constructor from the BaseClass,
    // then you don't need to write the code here, leave it blank.
}
```

12.2 Declare a `virtual` method in the `base` class and `override` it in the `derived` class

> ​	Remember:
>
> ​				`virtual` in the `base` class
>
> ​				`override` in the `derived` class

```c#
class Mammal
{
    public virtual void Breathe()
    {
    	//the general method for Mamml
    }
	//...
}

class Whale : Mammal
{
    public override void Breathe()
    {
    	//override the breathe method rather than using the general breathe
    }
	//...
}
```

12.3 Define an extension method for a type

> ​	:question: What is `extension method` in the first place? 
>
> ​			It is the `.` method you use everyday! Like `.Select()`, `.ToString()`, `.OrderBy()`.
>
> ​	:star: To conclude, the `extension method` is a **static method** which **extends** some sort of method by invoke the dot `.`
>
> ​	For example, I can write my own `countStringLength` method by decorating the `variable` with **this**.:star2::star2:
>
> ​	:question: What is `this` keyword? 
>
> ​	The `this` keyword refers to **the current instance of the class** and is also used as a modifier of the first parameter of an extension method.

```c#
namespace ExtensionMethods
{
    static class Util
    {
        public static int Negate(this int i)
        {
        	return -i;
        }
    }
}
```

> ​	so you see `this String str` is decorated with `this`, which means the variable can be the current instance of the class!!

```c#
using ExtensionMethods;  //bring the Extension method here
//...
int ten = 10;
int nine = ten.Negate();  //now you can use `.Negate()` method without writing this method inside a class
```



### 13.Interfaces and abstract classes

:star: the concept of `interface` is a little bit similar to `.header` file in C++, which is **a must for such class to implement it**.

13.1 Declare an interface

> ​	use `interface` keyword

```c#
interface IDemo
{
    string GetName();
	string GetDescription();
}
```

13.2 Implement an interface

> ​	implement the class to fulfill interface **explicitly**

```c#
class Test : IDemo
{
    public string IDemo.GetName()
    {
    	//...
    }
    public string IDemo.GetDescription()
    {
    	//...
    }
}
```

> ​		implement the class to fulfill interface **implicitly**

```c#
class Test : IDemo
{
    public string GetName()
    {
    	//...
    }
    public string GetDescription()
    {
    	//...
    }
}
```

13.3 `abstract` class which **can only be a base class**

> ​	use the `abstract` keyword. **You cannot create an instance from an abstract class**.
>
> ​	:question: OK, so what is the purpose to create an `abstract` class?
>
> ​	:star:It means **to be a template**. For example, you define a class call `Felidae猫科动物`, but `Felidae` should be treated as a family of mammals! There 		is no 	such instance of `Felidae`.

```c#
abstract class Felidae
{
    //...
    public virtual void Sound();
}

public class Cat : Felidae
{
    //...
    public override void Sound()
    {
        Console.WriteLine("Meow Meow~");
    }
}
```

13.4  A `sealed` class that **cannot be a base class**

```c#
sealed class Horse
{
    //...
}
```



### 14.Garbage collection and resource management

14.1 Write a destructor

> ​	use the `~` prefix. In the meantime, the method of destructor can't have access modifier!!(such as `public`)

```c#
class Example
{
    //..
    ~Example()
    {
    }
}
```

14.2 Call the destructor is invalid

> You can’t call a destructor. **Only the garbage collector can call a destructor**.

14.3 :x:Force garbage collection (**not recommended**)

```c#
GC.Collect;
```

14.4 Release a resource at a known point in time

> :warning:cons: this is at the risk of resource leaks if an exception interrupts the execution
>
> How to do it? => Write a **disposal method** (a method that disposes of a resource) and **call it explicitly** from the program.

```c#
class TextReader
{
    //...
    public virtual void Close()
    {
    	//write the disposal method here
    }
}
class Example
{
    void Use()
    {
        TextReader reader = ...;
        
        reader.Close();  // call it explicitly to dispose a resource
    }
}
```

14.5 Support exception-safe disposal in a class

> ​	that said, to implement the `IDisposable` interface

```c#
class SafeResource : IDisposable
{
	//...
    public void Dispose()
    {
    // Dispose resources here
    }
}
```

14.6 Implement exception-safe disposal for an object that implements the `IDisposable` interface

> ​	:star: This is the recommended option in garbage collection.
>
> ​	How to do that? => Create the object in a `using` statement

```c#
using (SafeResource resource = new SafeResource())
{
    // Use SafeResource here
    // ...
}
```



### 15.Properties

:star: Big picture: The design of property in C# is to inherit the `get()` and `set()` method in C++, but in an efficient, elegant and safe way.

15.1 Declare a read/write `property` for a structure or class

> ​	define the `type` of that property with `get` and `set`
>
> ​	`get`: able to read
>
> ​	`set`: able to write

```c#
struct ScreenPosition
{
	//...
    public int X
    {
        get { ... } // or get => ...
        set { ... } // or set => ...
    }
    //...
}
```

> ​	property with only `get` keyword is **read-only**
>
> ​	property with only `set` keyword is **write-only**

15.2 Declare a property in an `interface`

> ​	just write down the `get` and `set`

```c#
interface IScreenPosition
{
    int X { get; set; }
    int Y { get; set; }
}
```

> ​	the class implemented the interface will look like this:

```c#
struct ScreenPosition : IScreenPosition
{
    private int _x;
    private int _y;
    
    public int X
    {
        get => this._x;
        set => this._x = value;
    }
    public int Y
    {
        get => this._y;
        set => this._y = value;
    }
}
```

15.3 Create an automatic property

> ​	In the class or structure that contains the property, define the property with empty `get` and `set` accessors.
>
>    :heavy_check_mark:This is a very handy feature!

```c#
public class Customer
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

> ​	now this class can be used as a sort of data container!!

```c#
var customerBob = new Customer
{
    Id = 1,
    FirstName = "Bob",
    LastName = "Smith"
}
var customerDavid = new Customer
{
    Id = 3,
    FirstName = "David",
    LastName = "Rutten"
}
```



### 16.Indexers

:star: Big picture: What is the purpose of indexer?

​				It aims to **deconstruct the integer to binary value**(`1/0` and `true/false`) which is very **flexible**!

:pushpin:Fun fact: What the heck is integer, binary, hex, etc?

​				We use `decimal system十进制` in our daily life, e.g. "I am `26` years old." In the following context, the `hex`, `binary` are all another form, so to speak, of `decimal system`. Nothing special, that is it. `hexadecimal 十六进制` is 16-base. `binary` is 2-base.

16.1 Specify an integer value using binary or hexadecimal notation

> `0b0` for **binary** values prefixes.
>
> `0x0` for **hexadecimal** values prefixes. 
>
> Include `_` separators to make values easier to read.

```c#
uint moreBinData = 0b0_11110000_01011010_11001100_00001111;
uint moreHexData = 0x0_F0_5A_CC_0F;
```

16.2 Display an integer value as its binary or hexadecimal representation

> ​	Use the `Convert.ToString()` method, and specify 2 (for binary) or 16 (for hexadecimal) as the number base.

```c#
uint moreHexData = 0x0_F0_5A_CC_0F;
Console.WriteLine($"{Convert.ToString(moreHexData, 2)}");
// displays 11110000010110101100110000001111
// so `0x0_F0_5A_CC_0F` is `11110000010110101100110000001111` although they are in different base.
```

16.3 Create an indexer for a class or structure

> ​	use the keyword `this` and **square bracket `[]`**

```c#
struct RawInt
{
    //...
    public bool this [ int index ]
    {
        get { ... }
        set { ... }
    }
    //...
}
```

16.4 Define an indexer in an interface and implement it

> ​	define it:

```c#
interface IRawInt
{
	bool this [ int index ] { get; set; }
}
```

> ​	**implicitly** implement it:

```c#
struct RawInt : IRawInt
{
    //...
    public bool this [ int index ]
    {
        get { ... }
        set { ... }
    }
    //...
}
```

> ​	**explicitly** implement it:

```c#
struct RawInt : IRawInt
{
    //...
    bool IRawInt.this [ int index ]
    {
        get { ... }
        set { ... }
    }
    //...
}
```



### 17.Generics

17.1 Instantiate an object by using a generic type

> ​	when you see `<>` , it means this is used in a generic way

```c#
Queue<int> myQueue1 = new Queue<int>();
Queue<double> myQueue2 = new Queue<double>();
Queue<string> myQueue3 = new Queue<string>();
List<int> myList1 = new List<int>();
List<double> myList2 = new List<double>();
List<string> myList3 = new List<string>();
```

> ​	as you can see, the `Queue` can contain `int`, `double`, and `string` etc. That is due to the design of `Queue` and `List`
>
> ​	:star:it use `T` notated as **generic**.

```c#
public class Queue<T> : IEnumerable<T>, ICollection, IEnumerable
{
    //...
}
public class List<T> : IList<T>, ICollection<T>, IList, ICollection, IReadOnlyList<T>, IReadOnlyCollection<T>, IEnumerable<T>, IEnumerable
{
    //...
}
```

17.2 Create a new generic type

```c#
public class Tree<T>
{
 	//...   
}
```

17.3 :star:**Restrict** the type **that can be substituted** for the generic type parameter

> ​	It means that if you want to use this generic formwork, the data-type you set my implement something.
>
> ​	The following means the `T` in the `Tree` must implement `IComparable<T>`

```c#
public class Tree<T> where T : IComparable<T>
{
	//...
}
```

17.4 Define a generic method

> ​	put `<T>` before the `()`

```c#
static void InsertIntoTree<T>(Tree<T> tree, params T[] data)
{
    //...
}
```

17.5 Invoke a generic method

> ​	just put the data type you use to replace the `T`

```c#
InsertIntoTree<char>(charTree, 'Z', 'X');
```

17.6 Define a **covariant** interface

> ​	Specify the `out` qualifier for covariant type parameters. Reference the covariant type parameters only as the return types from methods and not as 	the types for method parameters:

```c#
interface IRetrieveWrapper<out T>
{
	T GetData();
}
```

17.7 Define a **contravariant** interface

> ​	Specify the `in` qualifier for contravariant type parameters. Reference the contravariant type parameters only as the types of method parameters and 	not as return types:

```c#
public interface IComparer<in T>
{
	int Compare(T x, T y);
}
```



:pushpin: A note on `T`. Here the `T` is literal symbol of `Generic`. What really does represent `Generic` is `< >`. See the following example:

```c#
public class Tree<T>
{
 	//...   
}
public class Tree<TItem>
{
 	//...   
}
```

They are the same in functionality no matter used `T` or `TItem`. I personally prefer `T` for simplicity.



### 18.Collections

> ​	The frequently used collections in C# are:
>
> 	- 

18.1 Create a new collection

> ​	use `List<T>` as an example

```c#
List<PlayingCard> cards = new List<PlayingCard>();
```

18.2 Add an item to a collection

> ​	`List<T>` use `Add`
>
> ​	`HashSet<T>` use `Add`
>
> ​	`Dictionary<T,T>` use `Insert`
>
> ​	`Queue<T>` use `Enqueue`
>
> ​	`Stack<T>` use `Push`

```c#
HashSet<string> employees = new HashSet<string>();
employees.Add("John");

LinkedList<int> data = new LinkedList<int>();
data.AddFirst(101);

Stack<int> numbers = new Stack<int>(); numbers.Push(99);
```

18.3 Remove an item from a collection

> ​	 `Remove` is used in `List<T>`, `HashSet<T>`, `Dictionary<T, T>`
> 
> ​	 `Dequeue` is used in `Queue<T>`
> 
> ​	 `Pop` is used in `Stack<T>`

```c#
HashSet<string> employees = new HashSet<string>();
//..
employees.Remove("John");

LinkedList<int> data = new LinkedList<int>();
//..
data.Remove(101);

Stack<int> numbers = new Stack<int>();
//..
int item = numbers.Pop();
```

18.4 Find the number of elements in a collection

> ​	use `Count`

```c#
List<PlayingCard> cards = new List<PlayingCard>();
//...
int noOfCards = cards.Count;
```

18.5 Locate an item in a collection

> ​	*array notation* is used in *dictionary-oriented collections*.
>
> ​	`Find` is used in *lists*.

```c#
Dictionary<string, int> ages = new Dictionary<string, int>();
ages.Add("John", 47);
int johnsAge = ages["John"];
```

> ​	in case there is a class named `Person`

```c#
public class Person
{
    public int ID { get; set; }
    public string Name { get; set; }
    public double Height { get; set; }
}
```

> ​	you can find the info in a list by `Find` using `System.Linq`

```c#
List<Person> personnel = new List<Person>();
Person Simon = new Person { ID = 3, Name = "Simon Botazzi", Height = 173.2 };
personnel.Add(Simon);
Person match = personnel.Find(p => p.ID == 3);  //there you go, you find Simon by searching ID==3
```

:warning:Note: The `Stack<T>`, `Queue<T>`, and `HashSet<T>` collection classes **do not** support searching, although you can test for membership of an item in a hash set by using the `Contains` method.



18.6 Iterate through the elements of a collection

> ​	Use a `for` statement or a `foreach` statement

```c#
LinkedList<int> numbers = new LinkedList<int>();
//...
for (LinkedListNode<int> node = numbers.First; node != null; node = node.Next)
{
    int number = node.Value;
    Console.WriteLine(number);
}
//...
foreach (int number in numbers)
{
	Console.WriteLine(number);
}
```



### 19.Enumerating collections

19.1 Make class enumerable which support the `foreach` construct

> ​	Implement the `IEnumerable` interface and provide a `GetEnumerator` method that returns an IEnumerator object.

```c#
public class Tree<T> : IEnumerable<T>
{
    //...
    IEnumerator<T> GetEnumerator()
    {
    	//...
    }
}
```

19.2 Implement an enumerator without using an iterator

> ​	Define an enumerator class that implements the `IEnumerator` interface, and that provides the `Current` property and the `MoveNext` method (and 	optionally the `Reset` method).

```c#
public class TreeEnumerator<T> : IEnumerator<T>
{
    //...
    T Current
    {
        get
        {
        	//...
        }
    }
    bool MoveNext()
    {
    	//...
    }
}
```

19.3 Define an enumerator by using an iterator

> ​	Implement the enumerator to indicate which items should be returned (using the `yield` statement) and in which order.

```C#
IEnumerator<TItem> GetEnumerator()
{
    for (...)
    {
    	yield return ...
    }
}
```



### 20.Delegate and Event

:star: `delegate` is literally an agent which can be seen as **delegate** of function.

:star: `delegate` is a pointer to method.



20.1 Declare a delegate type

> ​	just put the `delegate` ahead the decoration of the function.

```c#
delegate void myDelegate();
```

20.2 Create an instance of a delegate with initialization

> ​	:pushpin: Big picture: why do we need `delegate`? 
>
> ​			because sometime we don't know which method we should use. Imagine **delegate is a variable of method** rather than value.

```c#
//there are 2 methods defined
public double Add(double lhs, double rhs) => lhs + rhs;
public double Subtract(double lhs, double rhs) => lhs - rhs;

//declare an delegate whose parameter must match whom you want to use
public delegate double ArithmeticOperation(double lhs, double rhs);

//initialized
ArithmeticOperation operation;
bool flag = false;

//now the method operation is decided by the boolean value
public void AutoSelectOperation()
{
    if (flag)
    {
        operation = Add;
    }
    else
    {
        operation = Subtract;
    }
}

//use the delegate method
double result = operation(10, 3);  //since flag=false, the operation points to subtract
								   //so the result = 7
```

20.3 Declare an event

