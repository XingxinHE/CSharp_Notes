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

## Microsoft Visual C# Step by Step

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

