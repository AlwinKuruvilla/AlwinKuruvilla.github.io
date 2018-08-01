C# NOTES
========
VARIABLES 
	The simplest way to declare a variables is "string title;", where: 
	[Type Assignment] = "string"
	[Variable Name] = "title". 
	You can also give the variable:
	[Access modifier] = "public"
	[Value] = '"C# Essential Training"'

	Variables in C# can be implicitly typed which means that the compiler will figure out what the type will be based on the assignment. You do this by using the "var" keyword as the [Type Assignment].

	Access modifiers are used to limit the visibility of properties, methods, and fields so they are not unintentionaly changed. There are 4 access modifiers:
		1) Public
			- Can be accessed outside the class
		2) Protected
		3) Private
			- Can be accessed only within the class
		4) Internal
			- This is the default

	For a "string" remember to use the double quotes as single quotes are only for a "char" value.
    
PRIMATIVES (These are actually static objects in C#. They have properties and methods))
	For an "int" this value is 32-bit and is signed. To declare an unsigned "int" use "uint" as the type. uint.MaxValue > int.MaxValue. You can use "short" for a 16-bit signed integer ("ushort" for unsigned) and "long" for a 64-bit integer ("ulong" for unsigned) 

	If you need fractions use "float" (remember to add an "f" at the end of the number).
	You can also us "double".
			_____________________________________________________
			|  8-bit  |  16-bit  | 32-bit | 64-bit  |  128-bit  |
	Signed  : "sbyte" < "short"  < "int"  < "long"  < "decimal" |
	Unsigned: "byte"  < "ushort" < "uint" < "ulong" < "decimal" |
			-----------------------------------------------------

	The decimal has shorter range (-7.9 x 10^28 to 7.9 x 10^28) but more percision (28-29 significant digits) than the float (-3.4 x 10^38 to 3.4 x 10^38, 7 sig digits)

STATIC
	A static class allows you to use properties and methods without instaniating it. For example, if you type in "string." you'll see left of static properties and methods, however if you type 'string str = "Hello."' and then "str.", you'll see a lot more methods and properties.

Hint: "String" and "string" are equivalent types. ("String" is how it is in Ja)

STRINGS
		var testString = " abCDefg  ";
	- testString.Trim() --> "abCDefg"
		- This will chop off the extra spaces at the begining and end.
	- testString.TrimStart() --> "abCDefg  "
		- This will chop off the extra spaces at the end.
	- testString.ToUpper() --> " ABCDEFG  "
		- This will make it all uppercase
	- testString.ToLower() --> " abcdefg  "
		- This will make it all lowercase
	- testString.Substring(int StartingPostion, [int LengthWanted])
		- This will give you the substring from the "StartingPosition" (Remember that strings are just an   array of chars, therefore counting starts at 0) to the end of the string unless you specify the "LengthWanted".
	- testString.Length --> 10
		- This will give the number of chars in the total string.

	Concatenation & StringBuilder
	-----------------------------
	Concatenation is done with the + symbol or you can use StringBuilder.
		var sb = new StringBuilder(); 
		sb.Append("It was the best of times,");
		sb.Append("it was the worst of times.");
		sb.ToString(); --> "It was the best of times,it was the worst of times."

		sb = new StringBuilder("It was the best of times,");
		sb.AppendLine("it was the worst of times,");
		sb.AppendLine("it was the age of wisdom,");
		sb.ToString(); -->
			It was the best of times,it was the worst of times,
			it was the age of wisdom,
		-Note: in this case, the carriage return and new line did not appear after the first line.

		sb = new StringBuilder();
		sb.AppendLine("It was the best of times,");
		sb.AppendLine("it was the worst of times,");
		sb.AppendLine("it was the age of wisdom,");
		sb.ToString(); -->
			It was the best of times,
			it was the worst of times,
			it was the age of wisdom,

		-Note: there is a carriage return and new line at the very end.

	Formatting Strings
	------------------
		Note: you'll need to use the MSDN docs to get formatting styles

		var city = "NY"; var temp = 80.3f; var currentDt = DateTime.Now;

		string.Format("City is {0}, Temp is {1}, Time is {2}", city, temp, currentDt) -->
			City is NY, Temp is 80.3, Time is 7/26/2018 12:22:32 AM

		string.Format("City is {0}, Temp is {1}, Time is {2:t}", city, temp, currentDt) -->
			City is NY, Temp is 80.3, Time is 12:22 AM

		string.Format("City is {0}, Temp is {1}, Time is {2:T}", city, temp, currentDt) -->
			City is NY, Temp is 80.3, Time is 12:22:32 AM

		string.Format("City is {0}, Temp is {1:0.00}, Time is {2:T}", city, temp, currentDt) -->
			City is NY, Temp is 80.30, Time is 12:22:32 AM

	Parsing Strings
	---------------
		int.Parse("10") 		--> 10
		int.Parse("10,102") 	--> Error!
			- You can only use int.Parse on a string of only numbers

		var test = "10,102";
		int.Parse(test.Replace(",","")) --> 10102

		int myOutput;
		int.TryParse("10,102", out myOutput)
			- TryParse returns a bool. If the first parameter can't be parsed it will return false. 
			- If the first parameter can be parsed, it will set the "out" variable (myOutput in this case) to the parsed value.

MATH
	Math Operations
	---------------
	+	Addition
	-	Subtraction
	*	Multiplication
	/	Division
	%	Modulus

	i++ 	Increment i by 1 and store value in i.
	i-- 	Decrement i by 1 and store value in i.
	i+=5	Increment i by 5 and store value in i.
	i-=5	Decrement i by 5 and store value in i.
	i*=5	Multiply i by 5 and store value in i.
	i/=5	Divide i by 5 and store value in i.

	Math.Abs(-5) 	--> Absolute Value of 5
	Math.Pow(5, 2) 	--> 5 raised to the power of 2
	Math.Round(5.2)	--> Round to nearest integer
	Math.Floor(5.8) --> Round down to 5
	Math.Ceiling(5.2) --> Round up to 6

CONSTANTS & ENUMERATIONS
	Constants are values that never change. The are usefully when you want to save memory.	
		const float PI = 3.14f
	
	Enumerations are useful when you want numbers to represent values.
		enum weekDays { Monday, Tuesday, Wednesday, Thursday, Friday }
		var someDay = weekDays.Monday;
		- someDay will have the value of 0.

		enum weekDays { Monday = 1, Tuesday, Wednesday, Thursday, Friday }
		var someDay = weekDays.Monday;
		- someDay will have the value of 1.
		
		You can explicitly set each value if you want.

DATES & TIMES
	When you create a new instances of DateTime, you have a varity of methods to call on it as well as the abilities to perform mathematical operations on it.

	var date = new DateTime(year, [month], [day], [hour], [minute], [sec])
	DateTime.now - date 	--> The time difference between the two points.
	date.AddMinutes 		--> Add minutes to date.

SOLUTIONS
	Solutions are just a collection of projects. (Console apps, Desktop apps, Web apps).

NAMESPACES (Packages in Java)
	Organizes code and prevent name space collision. When you create a different folders and you want to use classes with that folder, you denote it with a "." for example: 
		English.Notebook notebook1
		Math.Notebook notebook2
	Each Notebook class is contained in two different folders

	When you are setting up references, the "using" key will be followed by the folder tree separated by ".".

AUTO-IMPLEMENTED PROPERTIES - *Research more*
	Used when you want to add encapsulation to your properties but there is no need for logic.
		string Name { get; set; }

PROPERTIES
	The getters and setters are used so that no one can change variables to something invalid. When creating the getter and setter for a variable we follow this template:

		private string _twitterAddress;  			--> Backing Variable
		private string TwitterAddress {				
			get { return _twitterAddress }
			set {
				if (value.StartsWith("@")) {		--> Magic Part
					_twitterAddress = value;
				}
				else {
					throw new Exception("Must begin with @");
				}
			}
		}

		- Backing Variable - Needed to contain the actual value set in the property declaration. Notice the 
		- Magic Part - The value "value" is a keyword that is part of the language and is used when we have getters and setters for properties.

CONSTRUCTOR (ctor)
	The point of a constructor is to handle initialization and they are named after the class. There are NO return types for constructors. You can add as many construtors to a class as necessary (overloaded). You just need to make sure that the method signature is different for each one. (Different number or types of arguments for each one.)

METHODS/FUNCTIONS
	Methods are like constructors but can be named anything. They can be overloaded too. 

	Function Bodied Expression:
	---------------------------
	These two functions are equivalent:

		public float AverageScores(float a, float b, float c) => (a + b + c) / 3;

		public float AverageScores(float a, float b, float c) {
			return (a + b + c) / 3;
		}

	The first is what we call a function bodied expressions.

	Static Methods:
	---------------
	When you add the word "static" to a method, we no longer need to instantiate it to use it. (No longer need to use the "new' keyword).

	Overriding ToString:
	--------------------
	The ToString() method is on the Object class, therefore we need to override to make sure that ToString() does what we want it to.

		public override string ToString() {
			var sb = new Str
			return base.ToString();
		}

	Note: The "this" keyword is used to refer to properties of the class itself. So "this.Name" will refer to the Name variable in the class.

INHERITANCE
	You can setup classes so they inherit from one another. By doing this, you don't duplicate code. To set up inheritance you have to make a new class and refer to it by using a ":"
		namespace SchoolLibrary {
			public class Teacher : Person {
				
			}
		}

	Abstract Class:
	---------------
	By using the keyword "abstract" in front of a class name, you are unable to instantiate it. (There is no constructor.) Class can only inherit from one class.

	Abstract Methods:
	-----------------
	When a method is abstract, all the classes that inherit from it must override it. Use the keyword "override" in the method on the subclass. Because this is limiting, using interfaces is preferred. Note that the abstract method does not need to be in an abstract class.

	Virtual Methods:
	----------------
	Using the "virtual" keyword on a method is similar to having a method be "abstract"; it needs to be overridden. The difference is that a virtual method is optional.

		public virtual int FileNumber (parameter1) { Some code; } --> this is on the base class
		public overide int FileNumber (parameter2) {
			return base.FileNumber (parameter2); --> "base" is the class where
		}

	Interfaces:
	-----------
	An interface allows you to require a class to implement certain properties and/or method signatures and have it named a certain way. Interfaces only define the structure so there is no logic in the methods. The key difference is that classes can inherit from multiple interfaces. It's tradition to start the name of the interface with the letter "I".

		namespace Library {
			public interface IDeweyNumber {
				float DeweyNumber { get; set; }
			}
		}

	Interfaces are implemented the same way as a class. Use the ":". If you have a class and interface or multiple interfaces, just separate them by a ",".

	Utility class:
	--------------
	This is just a collection of utility methods that are usually static.

	Extension methods: *Research more*
	------------------
	Extension methods enable you to "add" methods to existing types without creating a new derived type, recompiling, or otherwise modifying the original type. (An example would be if wanted to add a method to the type "string"). Extension methods are a special kind of static method, but they are called as if they were instance methods on the extended type. Using the keyword "this" within a parameter 

	class ExtensionMethods2 {
	    static void Main() {            
	        int[] ints = { 10, 45, 15, 39, 21, 26 };
	        var result = ints.OrderBy(g => g);
	        foreach (var i in result) {
	            System.Console.Write(i + " ");
	        }           
	    }        
	} //Output: 10 15 21 26 39 45

	namespace ExtensionMethods {
	    public static class MyExtensions {
	        public static int WordCount(this String str) {
	            return str.Split(new char[] { ' ', '.', '?' }, 
	                             StringSplitOptions.RemoveEmptyEntries).Length;
	        }
	    }   
	}

	https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods

UNIT TESTING
============
TDD = Test Driven Development

To create a Unit Test Project:
	1) Right click the solution and Add a new Unit Test Project.
	2) We now need to setup a reference:
		a) Expand the Unit Test Project to reveal References
		b) Right-click References and Add the class as a Reference
	3) The Test classes can now see all the code inside the Main classes.

Writing Unit Tests
	1) In the Test class, add a "using" statement for the namespace of the Main class at the top.
	2) Now in the method, you can add your unit test:

	using NUnit.Framework;
	using EsstTraining;

	namespace EsstTrainingTest {
		[TestFixture]
		public class Tests {
			[Test]
			public void Test1() {
				var testInstance = new Class1();
				var testResult = testInstance.AddTwo(9, 5);
				Assert.AreEqual(14, testResult, "I expect 9+5 to equal 14");
			}
		}
	}

	4) Test --> Run Tests
	5) Tip: You can put the windows side-by-side (Main Class | Test Class) to make it easier to work with.


Remember that all unit tests must have an Assert.

ARRAYS
======
	Arrays are denoted by adding [] after the type. 
	Ex:
		var myList = new string[4] 	--> This is an array of 4 values
		var myList[0] = "My";		--> Remember that arrays start with 0
		var myList[1] = "belly";
		var myList[2] = "is";
		var myList[3] = "full.";
		var myList[4] = "Not!"; 	--> This will give an "Index out of bounds" error

		var myList = new string [4] {"My", "belly", "is", "full"};

	To resize use: Array.Resize(ref myList, 6)