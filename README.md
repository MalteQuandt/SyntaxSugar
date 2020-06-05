## Syntactic sugar in Java

### 1. Table of Content: 

- [Syntactic sugar in Java](#syntactic-sugar-in-java)
  * [1. Table of Content:](#1-table-of-content-)
  * [2. Introduction:](#2-introduction-)
  * [3.  At the beginning of time: 1970:](#3-at-the-beginning-of-time-1970)
  * [4. Examples in other programming languages:](#4-examples-in-other-programming-languages)
  * [5. Wrapper assignment:](#5-wrapper-assignment)
  * [6. Static-Block](#6-static-block)
  * [7. For-Each-Loop:](#7-for-each-loop-)
  * [8. Arbitrary Number of Arguments:](#8-arbitrary-number-of-arguments-)
  * [9. Try with resources:](#9-try-with-resources-)
  * [10. Lambdas as substitute for functional interfaces:](#10-lambdas-as-substitute-for-functional-interfaces-)
  * [11. Double brace initialization:](#11-double-brace-initialization-)
  * [12. Double colon operator:](#12-double-colon-operator-)
  * [13. Conclusion](#13-conclusion)
  * [14.  References and Resources:](#14--references-and-resources-)

### 2. Introduction:

Syntactic sugar in a programming language is special syntax, that is designed so that it can be better understood by humans (Or be "sweeter" to the eye). There are a lot of examples, in nearly every programming language, like the array notation in the `C` programming language, which actually stands for a kind of  pointer arithmetic. But why does it even exist? Well, to an extend, every programming language that is higher level than byte code uses some kind of syntactic sugar. 

### 3.  At the beginning of time: 1970:

At the very beginning, programming was done on punch cards, after that it was bite code, and after that some basic high level languages were starting to pop up. Assembly, FORTRAN, COBOL, BASIC just to name a few, and every language, no matter the size or the paradigm had some kind of syntactic sugar thrown in to make the life of the programmer which were supposed to use them that much more easier. Some of those things never made it into the modern times, as they were bad to work with or because they were encouraging bad coding style (I'm looking at you, GOTO).

### 4. Examples in other programming languages:

As alluded to before, syntactic sugar is not something that only exists in java, rather it is a concept that exists in nearly every other programming language.

1. **Array notation is just pointer arithmetic**: The most obvious kind of syntax sugar. Assume an expression *( a + x) , where a is the pointer to the 0th element of an array, and x is an arbitrary number smaller or equal to the length of the array itself. This would be equal to the array notation of a[x].

2. **Augmented Assignment:** This is a feature quite a lot of programming languages have, be it object oriented, procedural or imperative. It means that the assignment expression a =a + b, with two variables where the operator **+** and **=** are defined can be written as a +=b, which is used more often than some people think.

3. **Method calling on an Object** Assume an object **object** with a method called **method** which has three formal parameters **a1**, **a2** and **a3 **of an  irrelevant type. Calling this method from the object in the language java would look something like this: `object.method(value1, value2, value3);`
   But this is just syntactic sugar for the global method call in the lower level language this object-oriented language is written in. That call would look something like this:

   `method(object, value1, value2, value3);`

4. **The ternary operator:** The ternary operator is the only operator of any language with c-like syntax which takes in three expressions as its operands. It is a simple way to write a branching statement as an expression. Let a, b and c be integers. Then the statement `if(b >= a) { c = b } else { c = a } `  is functionally equivalent to the statement`c = (b >= a ? b : a)` The only difference is that the first example is a statement and the second one is an expression, which means that you can bind the ternary operator in other expressions or terms which is very powerful.

5. **Accessing members from a pointer**: Assume a struct `struct`with the member `member`, and a pointer `ptr`that references that struct. Now, you could use pointer arithmetic to reference that pointer by writing *(ptr).member, but it is way more easy to just write ptr->member. The compiler does not care anyways, as it will most likely be compiled the same way anyways.

6. **Type inference**: The C# programming language (And also Java since Java 10) gives the user the ability of type inference, which has this syntax: `var identifier = value;`, which allows the compiler to automatically detect the data type of the value and set the type of that variable during compilation time. C++ also has this since C++11 using the `auto` modifier.

7. **Honorable Mentions:**  Most of those can be summarized under the mantle of "Syntax of C-like programming languages" which is true, a lot of these sugars have been around since the c programming language was first released by Kernighan and Ritchie in 1972.
   A few honorable mentions for me would be the goes-to loop in c-like languages: Let **x** be a positive integer and **b** be a positive integer smaller than x, then the loop `for(;x-->b;) {//do something}` which makes x iterate down until x is equal to b.

Those were a few examples from other programming languages. But now that we are warmed up and are hopefully aware what syntactic sugars are and are able to spot them, let us go into the actual topic of this article: Syntactic sugars in the *Java* Programming language.

In java, ["Syntactic sugar is a mean which allows Java to provide new syntax without implementing that on JVM level. The syntactic syntax is converted into another more general or low level construct by the compiler wich can be understood be JVM."]([https://www.logicbig.com/how-to/software-engineering/syntactic-sugar.html#:~:text=Syntactic%20sugar%20is%20a%20mean,can%20be%20understood%20by%20JVM.](https://www.logicbig.com/how-to/software-engineering/syntactic-sugar.html#:~:text=Syntactic sugar is a mean,can be understood by JVM.))

Now, what does that mean exactly?  Well, first we need to look at how the JVM (Java virtual machine) compiles and interprets the code we feed it. It is a bit unique in that java code is **both** compiled and interpreted. First, it is run through the compiler and is converted into so called bytecode. This is the step that the java language is implementing syntax sugar in. Afterwards, this bytecode in being fed into the JVM, a virtual machine which java is famous for, as you can use it to run your code independent from your platform! This is the step the java devs don't want to implement sugar in. As a simple example:

```` java
a += b;

// and

a = a + b;
````

Would both be compiled to the same byte code, and that is the point of syntax sugar. To break things that would be difficult to write down easier by implementing new syntax for the compiler to understand and convert, not by adding new things the virtual machine (And therefore your computer) can do.

### 5. Wrapper assignment:

Let's just start with something that every java programmer probably already knows and just work us through this list with an descending order of familiarity ( At the very least, i hope so!).

Some people argue that java is not a "true" object oriented programming language, as in one of those, no such things as primitive data types would exist. Java's way of stepping into the right direction is the inclusion of wrappers. Wrapper in the Java Programming language are a way to "wrap" primitive data types in objects.  Everyone could write a wrapper by themselves, as they are really not that difficult of objects. Here is a (Extremely simple) Wrapper implementation for the Integer data type:

````java
public Integer {
    // Encapsulated hidden value of the immutable integer data type. I set it as final simply to make it more clear
	// That the value will never be changed.
    private final int value;
    
    // Simple constructor to create the 
    public Integer(int value) {
        this.value = value;
    }
    
    // Simple getter for the value of this wrapper.
    public int getInt() {
        return value;
    }
}
````

You might wonder why there is a getter, but not a single setter to be seen, and this is because the Wrappers in java are, like Strings, immutable data types. This means that the internal state of the data can never be changed after the object has been created once. 
**Coders beware:** This does not mean that the object variable containing the reference to the wrapper can never change its value. It just means that if you want to assign a new value the old one will be dereferenced and with the next cycle of the garbage collector removed from memory.
Now that we are all on the same page, we can continue with this sugar, because all this buildup has it's conclusion, i promise. In order to create a new Integer-object, without the sugar you would have to write in code `Integer value = new Integer(1);`
This creates a new wrapper and assigns it to the object variable *value*. But in java, if you want to use the Wrapper classes from java itself, there is another way to write this assignment, and it is way more intuitive: Integer value = 1; This statement expresses what the coder really wants to express: Create an Integer variable and assign it the value one without the *new* keyword and the constructor. It is faster and way easier to read and understand with a glance. Sure, there is not really a difference for the experienced programmer, but for the beginner and the intermediate, as well as a person who just wants to understand the code with a glance it will make a difference.

### 6. Static-Block

This is a very simple feature: It is a block that is declared like so: `static{}` in which every field or method that is declared is handled as if it has the modifier *static* in front of it. This is useful if you have know that you want to access all the methods or fields in a specific class in a static context, which is sometimes the case ( Even if it is not really a best practice per-se) .
A small but simple example could look like this:

```` jave
static {
int a;
int b;
int add() {
return a + b;		
}
}
````

Everything within the scope of the static block is seen as a global variable or a class method.

### 7. For-Each-Loop:

The for-each loop in java, or otherwise referred to as the enhanced-for-loop is a simplified way to iterate over an array, a list that inherits from the Collection class or a list that inherits the iterable interface.
The syntax for it is written as follows:

````java
for(Object object : list) {
    // Do something
}
````

This functionally nearly equivalent to:

````java
for(int iterator = 0; iterator <= list.size();iterator++) {
    //Do something
}
````

Now, there is not really a difference when you work with objects. But when you try to use this loop to change the values of an array filled with primitive types, or tried to assign a new value to the object variable in the for-each example, you will find, that no change has been done. This is for the simple reason that the for each loop does not give you the actual object you are working on, but rather a reference (**Remember:** Java is pass by value, not pass by reference). This has the effect that you can work with the values a those positions, but if you were to try to assign a new value you would only assign a new value to the reference to the point in the list, not the actual point itself.

So you should only use this if you want to work on objects or if you just use the values for some kind of computation, not if you want to change the value of some variables in the list.

### 8. Arbitrary Number of Arguments:

Assume a method with the signature `int sum(Integer ... integers);`On first glance, it is pretty obvious what this is supposed to do: It should allow the client which uses the method to put in an arbitrary number of arguments. A short example, using the method from the above, but this time i will implement it at the beginning.

````java
abstract int sum(Integer ... integers) {
    int sum = 0;
    // Usage of the for-each loop!
    for(Integer summand : integer) {
        // Again, syntactic sugar to make this method a bit shorter than it would otherwise have been, and a lot more readable!
        sum += summan;
    }
    return int;
}

// This method can now be called in a few different ways:
public static void main(String[] args) {
    int buffer = 0;
    // First way:
    /* 
    * Here, we put in an empty array of numbers.
    * In this method it is useless, but it could be useful for some other methods where an empty array is
    * sometimes the case.
    */
    buffer = sum();
    System.out.println(buffer);
    
    /*
    * This is the notation if you want to write an array of size 3
    * with the elements 1, 2 and 3. It will be transformed into an array by the language.
    */
    buffer = sum(1, 2, 3);
    System.out.println(buffer);
    
    // Creating an array and just plugging that in as the argument is also possible.
    buffer = sum(new Integer[] = {1, 2, 3});
    System.out.println(buffer);
}
````

Things to note: The argument that gets passed to the function will ** always** be an array, so treat it that way. It is not a collection or a list, but an array of the type you specify, be it object or primitive. 
The syntax for this notation is: `Type ... arrayIdentifer` where the type is the type of the elements in the array.

Something else to note is that you can use this with other formal parameters too. A short example:

````java
abstract void method(float fPar1, double dPar2, char ... characters);
````

If you use it in combination with other parameters remember that the arbitrary number of argument sugar must stand at the end of the method as the very last formal parameter.

One las thing though, you should probably avoid using this in combination with generic types like in this example `void exampleMethod(T ... genreics);`If you do this, you will never be able to safely overload this method anymore. Lets look at an example:

````java
void method(T... examples);
void method(String ... examples);

// Suppose we call this method and pass it those arguments:
method("Hello", "World", 123);
````

If the generic method was not there, the solution would be easy! 123 would be cast to be a string and it would be put into the string array of length 3 that we have created with the method call. But now, there is no telling which of the two methods the compiler will choose. So always try to avoid those so called "accept-all" signatures.

### 9. Try with resources:

The try with resources syntax sugar has saved me quite a lot in my projects, as i quite often forget to close a stream after it's natural lifespan is over. But with the try-with-resources statement you don't even have to write that pesky `if(stream != null) stream.close();`anymore, as the language takes care of that for you. Let's look at an example:

````java
try {
    FileReader reader = new FileReader(file);
    // Do something with the reader.
} catch(IOException e) {
    System.out.println("The stream has encountered an error!");
    e.printStackTrace();
} finally {
    // We need to close the stream, cause it is no longer needed!
    if(reader != null) {
        reader.flush();
        reader.close();
    }
}
````

Why do we even need to care about closing this? Well, simple. File handlers are a scarce resource even on modern Computers, and if we don' t close our streams they will not be handed out again by the application (At the very least not until the program closes completely and the OS relocates all it's resources anyways.) This is why it is a best practice and should always be done.

Here is a way better way to do this:

```java
try(FileReader reader = new FileReader(file)) {
    // Do something with the reader!
    // The reader object variables scope will carry through to the end of this block!
} catch(IOException io) {
    System.out.println("The Stream has encountered an error!");
    e.printStacktrace();
}
```

In this example, closing the stream that is created within the parenthesis after the try will be handled by the JVM, and the programmer does not have to do a lot. Of course that can not be used as well, when you want to initialize multiple readers or writers or other kinds of streams, as that would mean that you also had to write multiple try-with-resources statements, which would clutter your code quite fast, so in that case the old way is still preferred.

### 10. Lambdas as substitute for functional interfaces:

For everyone who does not know what lambda calculus or lambda expressions are, i highly encourage you to watch [this](https://www.youtube.com/watch?v=eis11j_iGMs) video from the YouTube channel Computerphile which i believe brilliantly sums up the topic. But as a quick entry to the topic: Lambda calculus is a system of formal mathematics developed by the mathematician Alonzo Church in the 1930's. It is a system which can be used to simulate any Turing Machine, and is therefore Turing complete. 

First, we need to be clear about what the term "Functional interface" in java means. I am just going to assume that everyone still here is familiar with what a normal interface is, so i jump straight into the technicalities: A functional interface in java was introduced in Java 8 to give java programmers the ability to program with the functional paradigm. It is an interface with just a **single** unimplemented method. A quick example:

```` java
public interface MyInterface {
    // Single, not implemented method, only the signature is defined.
    public void myMethod();
}

// This is also a functional interface, since it only includes a single non implemented method. It does not matter if there are //other implemented methods or not, the only important thing is that there is only one unimplemented one.
interface MyInterface2 {
    public void myMethod();
    
    public void mySecondMethod() {
        System.out.println("Hello");
    }
}
````

Now, you could  implement this with the normal java syntax:

````java
MyInterface interfaceImplementaion = new MyInterface() {
    public void myMethod() {
        System.out.println("This is the implementation");
    }
}
````

We just created a new class that implements the MyInterface and defined that method in the with the curly brackets defined block. But there is a way faster way to write this down, and that is when we utilize java lambda expressions:

```` java
MyInterface interfaceImplementaion = () -> System.out.println("This is the implementation!");
````

Using the lambda feature we could break a fairly difficult to understand block of code easy to read and write.

As a last example, only to show how efficient lambda expressions can be, lets look at the code from an actionlistener:

````java
button.addActionListener(new ActionListener() {
	@Override
	public void actionPerformed(ActionEvent e) {
		//Do something!
	}
});

//With lambda syntax you can compress this into:
button.addActionListener(event -> {
//Do something!
});
````

Pretty cool that you can break this thing down to such a small line of code, right?

### 11. Double brace initialization:

Double brace initialization is a feature introduced by the java language in order to make passing a list as an argument easier.
Let's just start with an example this time:

```` java
ArrayList<String> list = new ArrayList<String>() {{
    add("Hello");
    add("World");
    add("!");
}};
````

So, what happens here?  The answer is that the compiler creates an anonymous class inheriting from ArrayList and provides us with an initialization block ( Which is represented with the inner braces.). When we write the method `add(argument);`  we actually write `this.add(argument);`with *this* referencing the newly created inner class that inherits from array list.

Lastly, be well aware that this pattern is considered by many to be a so called "Anti-Pattern", because it can cause memory-leaks, it creates a new class every time it is used (Which is fine when used once, but using it multiple times just puts a lot of stress on the class loader and the performance of your application.) If you want to know more about that, look at reference 

### 12. Double colon operator:

The double colon operator in java is a very small syntactic sugar than some may remember from the C++ Language. 
In short, `A::B` refers to the method `B` from the Class `A`, and is a method reference. It was introduced in Java 8 with the lambda expressions and is also called a **convenience** operator.

Another few short examples:

````java
ArrayList::add // Refers to the method add from the class ArrayList.
HashMap::new // Referes to the standart constructor of the class HashMap.
````

Lets look at just one more example with the knowledge of lambda expressions and method references that we have now.

The Math class in java has the max method defined as so:`max(int a, int b) { return ( a > b) ? a : b};`Which is very simply a class which takes two operands and returns the max value, or the second one if they are equal. This method can also be classified as a binary operator, as it takes two operands.

Lets assume we have a method method1 which takes as a parameter the functional interface `IntBinaryOperator`. Now you can use the call `Math::max`as the actual parameter, which means that we give the method method1 the function `Math.max` as an argument.

Now, where is that different to just using `Math.max(a, b)` as the actual parameter? Well, first of all, in Java 7 ( Which is the version where this was not possible) you could not put a function as a parameter, you could only pass function **results**. But this is totally different. Here, we actually pass the function itself, which will be checked by the compiler to be compliant with the functional interface and then fitting bytecode will be generated.

A final example will be showcased with the Method `reduce` defined in the java class `IntPipeline`.  This example has been taken directly from [Stack Overflow.](https://stackoverflow.com/questions/20001427/double-colon-operator-in-java-8?noredirect=1&lq=1)

```` java
@Override
public final OptionalInt reduce(IntBinaryOperator op) {
    return evaluate(ReduceOps.makeInt(op));
}

@Override
public final OptionalInt max() {
    // I have alreaddy defined the Math.max class above, so i will not do that here.
    return reduce(Math::max);
}


//Now, you could just write this with the functional interface and java 7 syntax, which would look like this:
reduce(new IntBinaryOperator() {
    int applyAsInt(int left, int right) {
        return Math.max(left, right);
    }
});
// But this is not much fun, as it takes quite a lot of syntax just to write this down.
// We can optimise this with the newly added lambda in java 8, which will be called like this:

reduce((int left, int right) -> Math.max(left, right));

// Finally, we can reduce this just one more time, as we can just put in the reference to the max.max method.
reduce(Math::max);
````

### 13. Conclusion

Those were the more interesting kinds of syntactic sugars in the language. But this does not mean that the other ones are not important at all, quite the opposite! The more popular and well known kinds of syntax sugars are so well known **because** they are so useful. There are reasons why the C language is still used today, and why the syntax of C-like languages is used so often, it is just so easy to use, and useful! I have already counted a few of the best syntax sugars that came to my head in the beginning, but there are many more, maybe even equally useful ones, but i just had to pick some to use and i picked my favorite and the ones i considered to be the most useful.
There are more kinds of syntactic sugars in the java programming language than i care to look up, but i think i have talked about the main ones, and brought this topic to your attention. This is the end of the article, and what you will do with that knowledge is up to you. You can just go about your normal day and forget about all the not's and crannies and all the uniqueness of the java language, or you could switch the tab and open up a browser and start your own research into this (in my opinion) very interesting topic. But however you may decide, i would really like it if you were to give me feedback in any way you can, i am open to critique. This is my first toe dip into the world of scientific journalism, so i hope to hear some good constructive critic. 

### 14.  References and Resources:

1. [Wikipedia Article about Syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar)
2. https://stackoverflow.com/questions/3158730/java-3-dots-in-parameters
3. [https://softwareengineering.stackexchange.com/questions/195081/is-a-lambda-expression-something-more-than-an-anonymous-inner-class-with-a-singl#:~:text=Yes%2C%20it%20is%20just%20a,would%20be%20exactly%20equivalent%20semantically.](https://softwareengineering.stackexchange.com/questions/195081/is-a-lambda-expression-something-more-than-an-anonymous-inner-class-with-a-singl#:~:text=Yes%2C it is just a,would be exactly equivalent semantically.)
4. https://docs.oracle.com/javase/tutorial/java/javaOO/arguments.html#varargs
5. https://stackoverflow.com/questions/515975/closing-streams-in-java
6. https://www.quora.com/What-syntactic-sugars-are-there-in-Java
7. [One of the oldest editions of "The C Programming language"](http://www.lysator.liu.se/c/bwk-tutor.html#goto)
8. [Wikipedia Article of the C Programming language](https://en.wikipedia.org/wiki/C_(programming_language))
9. [Why Dobule-Brace initialization are considered an anti pattern](https://blog.jooq.org/2014/12/08/dont-be-clever-the-double-curly-braces-anti-pattern/)
10. [10 Best Practices when coding in Java](https://blog.jooq.org/2013/08/20/10-subtle-best-practices-when-coding-java/)
11. [What are functional interfaces?]([http://tutorials.jenkov.com/java-functional-programming/functional-interfaces.html#:~:text=A%20functional%20interface%20in%20Java,to%20the%20single%20unimplemented%20method.](http://tutorials.jenkov.com/java-functional-programming/functional-interfaces.html#:~:text=A functional interface in Java,to the single unimplemented method.))
12. [Research about Lambda calculus](https://en.wikipedia.org/wiki/Lambda_calculus)
13. [Double colon and what it means](https://stackoverflow.com/questions/27015495/meaning-of-in-java-syntax?noredirect=1&lq=1)
14. [Double colon and the math class.](https://stackoverflow.com/questions/20001427/double-colon-operator-in-java-8?noredirect=1&lq=1)
