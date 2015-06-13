**Constants**
-------------
Constants are unchangeable variables in C# code. You have to assign the constant to a value when you declare it. The **const** keyword is used to define a constant.
You can define constant of almost any data type and you can define collection of constants as well. Let's look at the following example with string constant:

   

       ```
        using System;
       
        class Program
        {
            const string _html = ".html";
            const double _pi = 3.14159265359;
            double radius = 2;
            double circleArea;
            static void Main()
            {
        	// This causes a compile-time error:
        	// _html = "";
        
        	Console.WriteLine(_html);         // Access constant
        	Console.WriteLine(Program._html); // Access constant
        	circleArea = _pi * (radius*radius);
        	Console.WriteLine("Area: "+circleArea);
        	
        	radius=3;
            circleArea = _pi * (radius*radius);
        	Console.WriteLine("Area: "+circleArea);
            // _pi=4.764893 causes compile-time error as well
            }
        }
        ```
>**Tip:**
>Variable defined as const will simply be replaced by the value you assigned. The const variable won't be looked for by the compiler and it is retained in the assembly metadata.

You cannot assign const identifiers after compile-time. But you can access them as much as you want. The program above accesses the _html constant string in two ways. You can read a constant in the same way as a static variable.


**Advantages**
Constant fields have advantages in C# programs. They promote the integrity of your programs by telling the compiler not to allow you to change the values during runtime, which can result in fewer accidental bugs.

They also improve performance over regular variables in many cases, particularly when using integral types such as int. They eliminate accesses to memory that occur with fields and locals

##**In LSharp**
Using constants in LSharp may be useful in some situations where you are doing lots of calculations. This way, defining some of the values you might use as *const* might speed up the calculation process

*Reference*:  [http://www.dotnetperls.com/const
](http://www.dotnetperls.com/const)