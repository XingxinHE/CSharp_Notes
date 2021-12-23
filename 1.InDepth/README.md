

## C# in Depth

### 2. C#2

#### 2.1 Generics

:pushpin: Where `Generics` is heavily used?

- Collections

- Delegates, particularly in LINQ

- Asynchronous code

- Nullable value types

##### 2.1.1 Days before Generics

:page_facing_up: **Task** -> suppose you have the following task:

You need to create a collection of *strings* in one method (`GenerateNames`) and print those strings out in another method (`PrintNames`). 

:round_pushpin: **data**: `string`

:round_pushpin: **Function1** : `GenerateNames` . which generate names in such order and length

:round_pushpin: **Function2**: ``PrintNames` , which print the names from previous step



:pushpin: **Do it via `Array`**

```c#
static string[] GenerateNames()
{
    string[] names = new string[5];

    names[0] = "James";
    names[1] = "Sam";
    names[2] = "Carol";
    names[3] = "Kathy";
    names[4] = "Peter";

    return names;
}

static void PrintNames(string[] names)
{
    foreach(string name in names)
    {
        Console.WriteLine(name);
    }
}
```

**Pros**: It will be compiled fast since the length is all set.

**Cons**: You need to **allocate** the array with certain **length**. You can't change the length after initialization.



:pushpin: **Do it via `ArrayList`**

```c#
static ArrayList GenerateNames()
{
    ArrayList names = new ArrayList();

    names.Add("Tom");
    names.Add("Peter");
    names.Add("Kathy");

    return names;
}

static void PrintNames(ArrayList names)
{
    foreach(string name in names)  //here is an implicit cast from object to string
    {
        Console.WriteLine(name);
    }
}
```

**Pros**: Now the array is dynamic array which you don't have to specify its length.

**Cons**: What stored in `ArrayList` is `object` which means you can store not just `string`! It leads a serious problem that if the elements inside the `ArrayList` are not `string` and it will cause `InvalidCastException`.



:pushpin:**Do it via `StringCollection`**

```c#
static StringCollection GenerateNames()
{
    StringCollection names = new StringCollection();
    names.Add("Tom");
    names.Add("Bill");
    names.Add("Julia");
    return names;
}

static void PrintNames(StringCollection names)
{
    foreach(string name in names)
    {
        Console.WriteLine(name);
    }
}
```

**Pros**: Now it is 1️⃣ **type-safe** 2️⃣**dynamic array**.

**Cons**: But it still hard to implement the features since we have to define `IntegerCollection`, `FloatCollection`, and etc. But what if we want to add `Split()` function to every collection? We have to do it for all the collection! That's too bad!



##### 2.1.2 Using Generics

:pushpin:The definition of **parameters** and **arguments**

```c#
public void Method(string name, int value);

Method("Laura", 28);
```

*parameters*: declared in inputs, like `name` and `value` 

*arguments*: the actual variable and value puts into the function, like `"Laura"` is the argument for `name` parameter, `28` is the argument for the `value` parameter.



:pushpin:**type parameter** and **type argument**

Generics play an dual concept as well.

```c#
public class List<T>
{
    
}

List<string> names = new List<string>();
```

*type parameter*, `T`

*type argument*, `string`



:pushpin:**What is [arity][https://en.wikipedia.org/wiki/Arity]?**

Arity is the **number of arguments** or operands taken by a function or operation in logic, mathematics, and computer science.

Example:

A nullary function takes **no** arguments.

> ​	$f()=2$

A unary function takes **1** argument.

> ​	$f(x)=2x$

A binary function takes **2** arguments.

> ​	$f(x,y)=2xy$

A ternary function takes **3** arguments.

> ​	$f(x,y,z)=2xyz$

An $n$-ary function takes **n** arguments.

> ​	$f(x_1,x_2,...,x_n)=2\prod_{i=1}^{n}x_i$



:pushpin: **Arity** of Generic Types and Methods

```c#
public void Method(){};        //Nongeneric method (generic arity 0)
public void Method<T>(){};       //Method with generic arity 1
public void Method<T1, T2>(){};  //Method with generic arity 2
```



:pushpin: **Bad** practice of Generics

:x:

```c#
public void Method<TFirst>(){}
public void Method<TSecond>(){}
```

Compile-time **error**; Can’t overload solely by type parameter name.

:x:

```c#
public void Method<T, T>() {}
```

Compile-time **error**; duplicate type parameter T



:pushpin:**What can't be Generics?**

The following members can't be Generics:

- Fields
- Properties
- Indexers
- Constructors
- Events
- Finalizers



##### 2.1.3 Type Inference

In Chinese, it is "**类型推断**". Simply means the compiler will get to know what type is this variable. 

:pushpin: **How is type inference?**

It is a powerful technique!! Suppose you have the following function:

```c#
public static List<T> CopyAtMost<T>(List<T> input, int maxElements)
{
    List<T> output = new List<T>();
    int actualCount = Math.Min(input.Count, maxElements);
    for (int i = 0; i < actualCount; i++)
    {
        output.Add(input[i]);
    }
    return output;
}
```

And the first line of code uses *type inference*.

```c#
List<int> numbers = new List<int>();

List<int> chunk1 = CopyAtMost(numbers, 3);        //Use type inference
List<int> chunk2 = CopyAtMost<int>(numbers, 3);   //Explicitly specify the type
```

See? C# allow type inference to be used where otherwise the type arguments would have to be **explicitly** specified when creating.



:pushpin:**What should be aware of?**

Pay attention to `null`! The `null` literal **doesn’t have a type**, so type inference will:

:x: **fail** for 

```c#
Tuple.Create(null, 50); 
```

:heavy_check_mark: but **succeed** for

```c#
Tuple.Create((string) null, 50);
```



##### 2.1.4 Type Constraints

From above section, they are all Generic types but without any constraints. For example, you can infer any type in `List<T>`. But what if you have sort of **rules to limit the kinds of types**?



:memo: **Task**:

Write a method that formats a list of items and **ensures** the **items follow some sort of rules**. For example, to **format them in a particular culture** instead of the default culture of the thread. The `IFormattable` interface provides a suitable `ToString(string, IFormatProvider)` method.

:pencil2:**False Solution**:x::

```c#
static void PrintItems<T>(List<IFormattable> items)
```

What's wrong with this? It limits the types of arguments. For example, you can't put `List<decimal>` as arguments **although** `decimal` implements the interface `IFormattable`. The `List<IFormattable>` can't cast to `List<decimal>`.

:pencil2:**Correct Solution**:heavy_check_mark::

```c#
static void PrintItems<T>(List<T> items) where T : IFormattable
```

What is good about this? It doesn’t just change which types can be passed to the method. But it changes what is the "access" you can do with a value of type `T` within the method.



:pushpin:**What type constraints can do?**

The above example demonstrates type constraints of `interface`. So what else can type constraints do?

:one:  *Reference type constraint*. The type argument must be a **reference type**. `where T : classes/interfaces/delegates`

:two:  *Value type constraint*. The type argument must be a **non-nullable value type**. `where T : struct/enum`

:three:  *Constructor constraint*. The type argument must have a **parameterless** constructor. `where T : new()`

:four:  *Conversion constraint*. (I have no idea what it is...)  `where T : SomeType`



:pushpin:**A complicate example of Generics**

```c#
TResult Method<TArg, TResult>(TArg input) 
    where TArg : IComparable<TArg>
    where TResult : class, new()
```

`< >` what you see inside *angle brackets behind method name* are the **type parameters** been *used* in this Generic Method.

`TResult` is the Generic Type for `return` value

`TArg` is the Generic Type for the input of this function

`where TArg : IComparable<TArg>` means the Generic Type `TArg` must implement `IComparable<TArg>`

`where TResult : class, new()` means the Generic Type `TResult` must be a reference type with a parameterless constructor.



With above example, do you feel more comfortable with the follow code?

**Example** 1️⃣

```c#
public static Tuple<T1, T2> Create<T1, T2>(T1 item1, T2 item2)
```

- The name of this method is `Create`.

- Then the **type parameters** been *used* in this Generic Method are inside the `< >` which are `T1` and `T2`.

- The return value is `Tuple<T1, T2>`.

- The input argument is `(T1 item1, T2 item2)`.

**Example** 2️⃣

```c#
public static List<T> CopyAtMost<T>(List<T> input, int maxElements)
```

- The name of this method is `CopyAtMost`.

- Then the **type parameters** been *used* in this Generic Method are inside the `< >` which is `T`.

- The return value is `List<T>`.

- The input argument is `(List<T> input, int maxElements)`.



##### 2.1.5. The default and typeof operator



:pushpin:**Review `typeof()`**

The `typeof` operator obtains the `System.Type` instance for a type. 

The **argument** to the `typeof` operator must be :one:the **name of a type** or :two:a **type parameter**.

The **return** value is the **type**.

```c#
//suppose you have a method print its type
public static void PrintType<T>()
{
    Console.WriteLine(typeof(T));
}

//use this method
static void dowork()
{
    PrintType<int>();
    PrintType<IEnumerable>();
    PrintType<Dictionary<string, double>>();
}
```

The result will be:

```
System.Int32
System.Collections.IEnumerable
System.Collections.Generic.Dictionary`2[System.String,System.Double]
```



:pushpin: **Review of `default()`**

The **argument** of `default` must be the **name of a type** or a **type parameter**. 

The **return** value is the **default value of that type**.

```C#
//suppose you have a method display its default value
public static void DisplayDefaultValue<T>()
{
    var val = default(T);
    Console.WriteLine($"Default value of {typeof(T)} is {(val == null? "null" : val.ToString())}.");
}

//use this method
static void dowork()
{
    DisplayDefaultValue<int?>();
    DisplayDefaultValue<System.Numerics.Complex>();
    DisplayDefaultValue<System.Collections.Generic.List<int>>();
}
```

The result will be:

```
Default value of System.Nullable`1[System.Int32] is null.
Default value of System.Numerics.Complex is (0, 0).
Default value of System.Collections.Generic.List`1[System.Int32] is null.
```



:pushpin:**5** broad cases for **`typeof()`**

:one: No generics involved.

```c#
typeof(string)
```

:two: Generics involved but no type parameters

```c#
typeof(List<int>)
```

:three: Generics involved with type parameters

```c#
typeof(List<TItem>)
```

:four: Just a type parameter

```c#
typeof(T)
```

:five: Generics involved but no type arguments specified

```c#
typeof(List<>)
```

 

:pushpin:Intuition on **Open Generic Type**, **Generic Type** & **Closed Constructed Type**

Open Generic Type:

```c#
typeof(Dictionary<, >)
```

Generic Type:

```c#
typeof(Dictionary<TKey, TValue>)
```

Closed Constructed Type:

```c#
typeof(Dictionary<string, int>)
```



:pushpin: **Then what is the output of `typeof()`?**

:star: It will return what is the **Type** exactly when **compiled**. Taking following code as an example:

```c#
//create a method printing closed constructed type
public static void PrintClosedConstructedType()
{
    Console.WriteLine(typeof(int));
    Console.WriteLine(typeof(List<int>));
}

//create a method printing closed constructed type eventually but with generic method
public static void PrintGenericType<T>()
{
    Console.WriteLine("typeof(T) = {0}", typeof(T));
    Console.WriteLine("typeof(List<T>) = {0}", typeof(List<T>));
}

//create a method printing open generic type
public static void PrintOpenGenericType()
{
    Console.WriteLine(typeof(List<>));
    Console.WriteLine(typeof(Dictionary<,>));
}

static void dowork()
{
    Console.WriteLine("\nPrint Closed Constructed Type...");
    PrintClosedConstructedType();
    Console.WriteLine("\nPrint Generic Type...");
    PrintGenericType<int>();
    Console.WriteLine("\nPrint Open Generic Type...");
    PrintOpenGenericType();
}
```

The output is:

```
Print Closed Constructed Type...
System.Int32
System.Collections.Generic.List`1[System.Int32]

Print Generic Type...
typeof(T) = System.Int32
typeof(List<T>) = System.Collections.Generic.List`1[System.Int32]

Print Open Generic Type...
System.Collections.Generic.List`1[T]
System.Collections.Generic.Dictionary`2[TKey,TValue]
```

:star: That said, whenever code is executing within a *generic type* or *method*, the **type parameter** always **refers to** a **closed, constructed type**.



:mag:Let's take a look at the **format**:

```
System.Collections.Generic.List`1[System.Int32]
```

The ``List`1`` indicates that this is a *generic type* called `List` with **generic arity 1** (one type parameter), and the type arguments are shown in square brackets afterward.



##### 2.1.6 Generic type initialization

Just remember: :star: Each **closed, constructed type** is **initialized separately** and has its own independent set of static fields.

```c#
class GenericCounter<T>
{
    private static int value;

    static GenericCounter()
    {
        Console.WriteLine("Initializing counter for {0}", typeof(T));
    }

    public static void Increment()
    {
        value++;
    }

    public static void Display()
    {
        Console.WriteLine("Counter for {0} : {1}", typeof(T), value);
    }
}
//..
static void dowork()
{
    GenericCounter<int>.Increment();    //Trigger the static constructor!
    GenericCounter<int>.Increment();
    GenericCounter<int>.Display();

    GenericCounter<string>.Display();   //Trigger the static constructor!
    GenericCounter<string>.Increment();
    GenericCounter<string>.Display();
}
```

Since the `static` field is independent, the result is trivial.

```
Initializing counter for System.Int32
Counter for System.Int32 : 2
Initializing counter for System.String
Counter for System.String : 0
Counter for System.String : 1
```

:mag: Few things to focus:

1. the `GenericCounter<string>` value is independent of `GenericCounter<int>`.
2. the `static` constructor is run **every initialization(twice)**: once for each closed, constructed type.



:arrows_counterclockwise: But if I switch the `static` constructor to a normal constructor:

```c#
GenericCounter()
{
    Console.WriteLine("Initializing counter for {0}", typeof(T));
}

//..

static void dowork()
{
    GenericCounter<int>.Increment();
    GenericCounter<int>.Increment();
    GenericCounter<int>.Display();

    GenericCounter<string>.Display();
    GenericCounter<string>.Increment();
    GenericCounter<string>.Display();
}
```

The output would be different! The only difference is that the constructor **runs behind twice** while it doesn't output a message.

```
Counter for System.Int32 : 2
Counter for System.String : 0
Counter for System.String : 1
```



#### 2.2 Nullable value types

:star: **Big Picture**

*Regularity*: There are hundreds of questions on StackOverflow on `null`.

*Quote*: Tony Hoare introduced `null` references into Algol in 1965 and has subsequently called it his “billion-dollar mistake.”

*Everyday*: Countless developers have become frustrated when their code throws `NullReferenceException`(.NET).

##### 2.2.1. `null` = Absence of info

**:thinking:What are the cases using `null` in daily life?**

The following are some examples.

- :one:the form of a person including `born` and `death`
  - the person is not dead right now, `death=null`
  - the person's child was not born yet, `born=null`
- :two:the form of a customer including `company_info`
  - the person was not an employee currently, `company_info=null`



:pushpin:**Days before `null` in C#**

- :one:Use **a reserved value to represent missing data**. For example, you might use `decimal.MaxValue` in a price filter to represent “no maximum price specified.”
- :two:Keep a separate **Boolean flag to indicate** whether it has a real value or the value should be ignored. 

For case :one:, it is so common! For instance, the `Unset` property of `Point3d, Plane` are with extremely high value.

```c#
//
// Summary:
//     Gets a plane that contains Unset origin and axis vectors.
public static Plane Unset { get; }
```

For case :two:, it is also common! In the old repo, you see the programmer always check before the value.

:bangbang::warning: **Both are error prone!!** Unfortunately, both solution are **bad**. Why?:thinking: 

- case 1, you remember, it is ok:no_mouth:

```c#
//case 1.  you remember to do the check
var someValue = xxx;
if(the_value_valid)
{
    //do sth
}
else
{
    //do sth
}
operation(somevalue);
```

- case 2, you forget to check, **damn**!:dizzy_face::x:

```c#
//case 2.  you forget
operation(somevalue);
```

It’ll silently do the wrong thing and quite possibly **propagate the mistake to other parts of the system**. :warning:**Silent failure is the worst kind**, because it can be hard to track down and hard to undo. 



##### 2.2.2. `Nullable <T> struct` 

:pushpin:****

I prefer nice loud exceptions that stop the broken code in its tracks.

