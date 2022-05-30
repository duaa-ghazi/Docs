*  that we should be concerned about models and requirements instead.

* specifying requirements in such detail that a machine can execute them is programming. Such a specification is code.

*  It will still need to be rigorous, accurate, and so formal and detailed that a machine can understand and execute it

* But we will never eliminate necessary precision—so there will always be code.

* We call it wading. We wade through bad code

* keeping your code clean is not just cost effective; it’s a matter of professional survival.

* we should not be shy about telling them what we think.

* It’s your job to defend the code with equal passion. 
* unprofessional for programmers to bend to the will of managers 
* A programmer with “code-sense” will look at a messy module and see options and variations. 
*  Bad code tempts the mess to grow
* Bjarne Stroustrup,inventor of C++ and author of The C++ Programming Language : "**I like my code to be elegant and efficient . clean code does one thing well**"

* Grady Booch, author of Object Oriented Analysis and Design with Applications :

  "**Clean code is simple and direct . readability"**

* “Big” Dave Thomas, founder of OTI, godfather of the Eclipse strategy :

  "**Clean code can be read, and enhanced by a developer other than its original author.  It has minimal dependencies . minimal API .Code, without tests, is not clean** "

* Michael Feathers, author of Working Effectively with Legacy Code:

  "**Clean code always looks like it was written by someone who cares**."

* Ron Jeffries, author of Extreme Programming Installed and Extreme Programming Adventures in C#: start code with **Fortran**

  "**simple code: • Runs all the tests; • Contains no duplication; • Expresses all the design ideas that are in the system; • Minimizes the number of entities such as classes, methods, functions, and the like**."

* Ward Cunningham, inventor of Wiki, inventor of Fit, coinventor of eXtreme Programming. Motive force behind Design Patterns. Smalltalk and OO thought leader. The godfather of all those who care about code.: 

  "**pretty much what you expected.**"

  

* **Uncle Bob** (auther of this book) Robert martin
* The Boy Scouts of America Rule: **"Leave the campground cleaner than you found it."**





**LeBlanc’s law: Later equals never** 

![](/home/duaa/Pictures/cc2.png)

![](/home/duaa/Pictures/cc3.png)



*************

Chapter 2 : Meaningful Names 

![](/home/duaa/Pictures/cc4.png)

![](/home/duaa/Pictures/cc5.png)

 

![](/home/duaa/Pictures/cc6.png)

![](/home/duaa/Pictures/cc7.png)

![](/home/duaa/Pictures/cc8.png)

* use intention-revealing names 

* If a name requires a comment, then the name does not reveal its intent.  

  ```
  int d; // elapsed time in days
  ```

* We should avoid words whose entrenched meanings vary from our intended meaning

* accountList :x: ->  accountGroup or bunchOfAccounts or just plain accounts would be better. it’s probably better not to encode the container type into the name. 

* . Using inconsistent spellings is disinformation.

*  make your names pronounceable.

* Use Searchable Names  : Single-letter names and numeric constants have a particular problem in that they are not easy to locate across a body of text.

* avoid encoding :encoding “language” ,Java programmers don’t need type encoding

* Interface and implementation :   IShapeFactory and ShapeFactory? I prefer to leave interfaces unadorned. ShapeFactory is preffered .  So if I must encode either the interface or the implementation, I choose the implementation -> ShapeFactoryImp 0r IShapeFactory

* Class Names :Classes and objects should have noun or noun phrase names like Customer, WikiPage ... ,class name should not be a verb.

* Methods Names:   should have verb or verb phrase names like postPayment, deletePage, or save. prefixed with get, set, and is 

* Say what you mean. Mean what you say

* dont pun :Avoid using the same word for two purposes “one word per concept”.

  

P28 -> when method mus has more than 3 variables to do the task  , we need to create a class with fields (this variables) and a method to do the task   

Chapter 3: **FUNCTIONS** 

FUNCTIONS : should be small ,do one thing only but do it well

* **One Level of Abstraction per Function** : when  a function  call more than 2 functions(as steps) this called one level of abstraction . and if one of step(function) has set of fun's (next level of abstraction).

* P38 : switch case not achieve the SRP principle because it has more tasks .

  and also not achieve the OCP PRINCIPLE ..  SOL : use abstract factory pattern and inside interface make swithc to create appropriate instance .

​     -> screen code 39

**Function Arguments**

* Function Arguments
  The ideal number of arguments for a function is
  zero (**niladic**). Next comes one (**monadic**), followed
  closely by two (**dyadic**). Three arguments (**triadic**)
  should be avoided where possible. More than three
  (polyadic) requires very special ju

* Arguments are even harder from a testing point of view. Imagine the difficulty of
  writing all the test cases to ensure that all the various combinations of arguments work
  properly. If there are no arguments, this is trivial. If there’s one argument, it’s not too hard.
  With two arguments the problem gets a bit more challenging. With more than two argu-
  ments, testing every combination of appropriate values can be daunting.

* arg must be input args .(and the best is to be one arg and not more than 3 ) and we must avoid to be output arg . this also affect on test case (know the input is much easier than expect out the must be include as arg) . 

  ```java
  includeSetupPageInto(StringBuffer pageText) .// the arf is out arg
  //Using an output argument instead of a
  //return value for a transformation is confusing
  ```

  ******

  

**Flag Arguments** 

* if there is a flag bool arg inside fun ,It does one thing if the flag is true and another if the flag is false!
   passing that flag in, and I wanted to limit the scope of refactoring to the function and below. Still, the method call render(true) is just plain confusing to a poor reader. Mousing over the call and seeing **render(boolean isSuite)** helps a little, but not that much. We should have
  split the function into two: **renderForSuite(**) and **renderForSingleTest()**

**Dyadic** **Functions**

A function with two arguments is harder to understand than a monadic function

There are times, of course, where two arguments are appropriate. For example,
Point p = new Point(0,0)

Even obvious dyadic functions like assertEquals(expected, actual) are problematic

**Triads**
Functions that take three arguments are significantly harder to understand than dyads.think very
carefully before creating a triad.

Argument Objects
When a function seems to need more than two or three arguments, it is likely that some of
those arguments ought to be wrapped into a class of their own. Consider, for example, the
difference between the two following declarations:
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
Reducing the number of arguments by creating objects out of them

**Argument Lists**

public String format(String format, Object... args) 

 format they are equivalent to a single argument of type List .

So all the same rules apply. Functions that take variable arguments can be monads,
dyads, or even triads. But it would be a mistake to give them more arguments than
that.
void monad(Integer... args);
void dyad(String name, Integer... args);
void triad(String name, int count, Integer... args);



note:Functions should either do something or answer something, but not both

note: Don’t Repeat Yourself 

**Prefer Exceptions to Returning Error Codes**

and Extract Try/Catch Blocks into fun's

->screen p46 //instead of if else to return error , the exception with try/catch is better

///////////

**Commments** : “Don’t comment bad code—rewrite it.”

*we must cleant the bad code not comment it .

It is sometimes useful to provide basic information with a comment

*warn other pro-grammers about certain consequences

*TODO Comments

*Javadocs in Public APIs
There is nothing quite so helpful and satisfying as a well-described public API.

******

Code formatting is about communication, and
communication is the professional developer’s first order of business.

vertical formatting :

-> vertical density : there is must put a black lines bettween funs , all var and the next . all import and the next . 

->vertical distance :  the var dec on fun or var instant must be on top,and  function that is called should be below a function that does the calling. 2

dependent fun must be on 

-> vertical ordering :We expect the
low-level details to come last.This creates a
nice flow down the source code module from high level to low level,and also function that is called should be below a function that does the calling



**Horizontal Formatting**

limit of char in line at most 100- 120.

We use horizontal white space to associate things that are strongly related

*surrounded the assignment operators with white space to accentuate them,seperate left side and the right side

*didn’t put spaces between the function names and the opening
parenthesis of it is  arg's. This is because the function and its arguments are closely related

*separate arguments within the function call parenthesis to accentuate 

```
public static double root1(double a, double b, double c) {
```

*accentuate the precedence of operators ,factors/div have no white space between them
because they are high precedence. The terms are separated by white space because addi-
tion and subtraction are lower precedence.

```
return (-b + Math.sqrt(determinant)) / (2*a);
```

*******

**horizontal alignment**

screen-p87. not prefer

prefer unaligned declarations and assignments 

screen-p87

**Indentation**

To make this hierarchy of scopes visible, we indent the lines of source code in pro-
portion to their position in the hiearchy. Statements at the level of the file, such as most
class declarations, are not indented at all. Methods within a class are indented one level
to the right of the class. Implementations of those methods are implemented one level to
the right of the method declaration. Block implementations are implemented one level
to the right of their containing block, and so on.

screen p88 before$after



**Dummy Scopes**
Sometimes the body of a while or for statement is a dummy, as shown below

```
while (dis.read(buf, 0, readBufferSize) != -1) // not prefer
```

screen p91 : the best , notes : 1- return in fun no need to put space before .

**Data Abstraction**

screen p94 one exposes its implementation and the other com-
pletely hides it.

Hiding implementation is not just a matter of putting a layer of functions between
the variables. Hiding implementation is about abstractions! A class does not simply
push its variables out through getters and setters. Rather it exposes abstract interfaces
that allow its users to manipulate the essence of the data, without having to know its
implementation.



*difference between objects and data structures. Objects hide
their data behind abstractions and expose functions that operate on that data.Data struc-
ture expose their data and have no meaningful functions. screen p96

data structures simply had public variables and no functions, whereas objects had private variables and public functions(not getter/setter )(). there are frameworks and standards (e.g., “beans”) that demand that even simple data structures have accessors and mutators.

Procedural code (code using data structures) makes it easy to add new functions without
changing the existing data structures. OO code, on the other hand, makes it easy to add
new classes without changing existing functions.

***The Law of Demeter**
says that a method f of a class C should only call
the methods of these:
• C
• An object created by f

• An object passed as an argument to f
• An object held in an instance variable of C

The method should not invoke methods on objects that are returned by any of the
allowed functions. In other words, talk to friends, not to strangers

```java
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath(); 
//this violate the Law of Demeter (among other things)
//because it calls the getScratchDir() function on the return value of //getOptions() and then
//calls getAbsolutePath() on the return value of getScratchDir()

//Train Wrecks : Chains of calls(called Train Wrecks) like this are generally considered to be sloppy style and should be avoided
//It is usually best to split them up as follows:
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

**Hybrids**
*This confusion sometimes leads to unfortunate hybrid structures that are half object and
half data structure. They have functions that do significant things, and they also have either
public variables or public accessors and mutators that, for all intents and purposes, make
the private variables public, tempting other external func.

**Data Transfer Objects**

- a data structure is a class with public variables and no functions. This is sometimes called a data transfer object, or DTO
- Somewhat more common is the “bean” form shown in Listing 6-7. Beans have private
  variables manipulated by getters and setters
- **Active Record**: special forms of DTOs They are data structures with public (or bean-
  accessed) variables; but they typically have navigational methods like save and find . Typically these Active Records are direct translations from database tables,

**Exceptions**

instead of if else and flag to return message or not  we use try/catch or throw  it is more clear 

write Try-Catch-Finally statement first statement when you are writing code that could throw
exceptions.

**Use Unchecked Exceptions**

checked exceptions is an Open/Closed Principle 1 violation.

Consider the calling hierarchy of a large system. Functions at the top call functions
below them, which call more functions below them, ad infinitum. Now let’s say one of the
lowest level functions is modified in such a way that it must throw an exception. If that
exception is checked, then the function signature must add a throws clause. But this
means that every function that calls our modified function must also be modified either to
catch the new exception or to append the appropriate throws clause to its signature. Ad
infinitum.

Checked exceptions can sometimes be useful if you are writing a critical library: You
must catch them. But in general application development the dependency costs outweigh
the benefits. used unchecked ingeneral yes 

 

Provide Context with Exceptions:If you are logging in your application,
pass along enough information to be able to log the error in your catch

**Don’t Return Null**

* check for null,it is bad ,Returning null from methods is bad

* in case  of list (return empty list instead of null if there is no items) screen p111 s Collections.emptyList()

**Don’t Pass Null**

Returning null from methods is bad, but passing null into methods is worse. Unless you
are working with an API which expects you to pass null , you should avoid passing null in
your code whenever possible. the rational approach is to forbid
passing null by default.

The question is not so much whether you should check for `null` or let the runtime throw an exception; it is how you should respond to such an unexpected situation.

Your options, then, are:

- Throw a generic exception (`NullReferenceException`) and let it bubble up; if you don't do the `null` check yourself, this is what happens automatically.
- Throw a custom exception that describes the problem on a higher level; this can be achieved either by throwing in the `null` check, or by catching a `NullReferenceException` and throwing the more specific exception.
- Recover by substituting a suitable default value.

***Should we always check each parameter of method in java for null in the first line?***

opinion 1 : There is no general rule which one is the best solution. Personally, I would say:

- The generic exception is best if the error condition would be a sign of a serious bug in your code, that is, the value that is null should never be allowed to get there in the first place. Such an exception may then bubble all the way up into whatever error logging you have set up, so that someone gets notified and fixes the bug.
- The default value solution is good if providing semi-useful output is more important than correctness, such as a web browser that accepts technically incorrect HTML and makes a best effort to render it sensibly.
- Otherwise, I'd go with the specific exception and handle it somewhere suitable

opinion2 :The best way is to **only check when necessary**.

If your method is `private`, for example, so you know nobody else is using it, and you know you aren't passing in any nulls, then no point to check again.

If your method is `public` though, who knows what users of your API will try and do, so better check.

based on this article https://www.baeldung.com/java-avoid-null-check : so we can **Handling *null* Through the API Contract**  , and for  client code accessing the above APIs, there is no need for a *null* check.  

for get somthing   and we dont know if it null or not  we can  use Optional 

```
public Optional<Object> process(boolean processed) {
    String response = doSomething(processed);
    return Optional.ofNullable(response);
}
```

and use optional with collection 

```
public String findFirst() {
    return getList().stream()
      .findFirst()   // this return optional andwill return an empty 							Optional when there is no data
      .orElse(DEFAULT_VALUE);  // Here, we have used orElse to provide 									a default value instead ofreturn an 								empty Optional.
}
```



**Boundaries**

**Third-party code** :Third-party code helps us get more functionality delivered in less time

**Learning log4j** : use the apache log4j package 

**Learning Tests Are Better Than Free**

**Using Code That Does Not Yet Exist**



***

Unit test

The Agile and TDD(Test Driven Development) move-
ments have encouraged many programmers to write automated unit tests,

Three Laws of TDD:

First Law You may not write production code until you have written a failing unit test.
Second Law You may not write more of a unit test than is sufficient to fail, and not com-
piling is failing.
Third Law You may not  write more production code than is sufficient to pass the cur-
rently failing test.

Clean Tests

```
@Test
public void turnOnCoolerAndBlowerIfTooHot() throws Exception {
tooHot(); // put detail in fun 
assertEquals("hBChl", hw.getState()); // one final assert
}
```

* StringBuffer  are a bit ugly than string concatination.

**One Assert per Test**
There is a school of thought 4 that says that every test function in a JUnit test should have one  one assert statement.

**Single Concept per Test**

Clean tests follow five other rules that form the above acronym:

**Fast** Tests should be fast. They should run quickly. When tests run slow, you won’t want
to run them frequently. If you don’t run them frequently, you won’t find problems early
enough to fix them easily. You won’t feel as free to clean up the code. Eventually the code
will begin to rot.
**Independent** Tests should not depend on each other. One test should not set up the condi-tions for the next test. You should be able to run each test independently and run the tests in
any order you like. When tests depend on each other, then the first one to fail causes a cas-
cade of downstream failures, making diagnosis difficult and hiding downstream defects.

**Repeatable** Tests should be repeatable in any environment. You should be able to run the
tests in the production environment, in the QA environment, and on your laptop while
riding home on the train without a network. If your tests aren’t repeatable in any environ-
ment, then you’ll always have an excuse for why they fail. You’ll also find yourself unable
to run the tests when the environment isn’t available.

**Self-Validating** The tests should have a boolean output. Either they pass or fail. You
should not have to read through a log file to tell whether the tests pass. You should not have
to manually compare two different text files to see whether the tests pass. If the tests aren’t
self-validating, then failure can become subjective and running the tests can require a long
manual evaluation.

**Timely** The tests need to be written in a timely fashion. Unit tests should be written just
before the production code that makes them pass. If you write tests after the production
code, then you may find the production code to be hard to test. You may decide that some
production code is too hard to test. You may not design the production code to be testable.

********

**Classes**

Following the standard Java convention, a class should begin with a list of variables. Pub-
lic static constants, if any, should come first. Then private static variables, followed by pri-
vate instance variables.Public functions should follow the list of variables

**Encapsulation**
We like to keep our variables and utility functions private, but we’re not fanatic about it.
Sometimes we need to make a variable or utility function protected so that it can be
accessed by a test. For us, tests rule. If a test in the same package needs to call a function
or access a variable, we’ll make it protected or package scope. However, we’ll first look for
a way to maintain privacy. Loosening encapsulation is always a last resort.

**Classes Should Be Small!**

**The Single Responsibility Principle** :a class or module should have one,
and only one, reason to change

**Cohesion**
Classes should have a small number of instance variables(loosly coupling) and Each of the methods of a class should manipulate one or more of those variables(high Cohesion)

we would like cohesion to be high. When cohesion is high, it
means that the methods and variables of the class are co-dependent and hang together as a
logical whole . implementation of a Stack  is a very cohesive class.

**concrete** classes, which contain implementation details (code), and **abstract** classes, which
represent concepts only, A client class depending upon concrete details is at risk when
those details change. We can introduce interfaces and abstract classes to help isolate the
impact of those details.

****

Systems :

Software systems should separate the startup process, when the application objects are
constructed and the dependencies are “wired” together, from the runtime logic that takes
over after startup.

1- seperate counstruction oblect from using i

* 

```
public Service getService() {
if (service == null)
service = new MyServiceImpl(...); // Good enough default for most 										cases?
return service;
}
```



2-seperation of main : on main .One way to separate construction from use is simply to move all aspects of construction to
main ,



3- factories . use Factory method pattern/abstract factory  (main create instance from the imp class of such interfaceso ) the application is decoupled from the details of how to
build

4- dependency injection : powerful mechanism for separating construction from use and it is  application of Inversion of Control (IoC). supporting the Single Responsibility Principle. In the context of dependency management, an object should not take responsibility for instantiating dependencies itself.Instead, it should pass this responsibility to another “authoritative” mecha-
nism, thereby **inverting the control**

* True Dependency Injection goes one step further. The class takes no direct steps to
  resolve its dependencies; it is completely passive. Instead, it provides **setter methods** or
  **constructor arguments (or both)** that are used to inject the dependencies .During the construction process, the DI container instantiates the required objects (usually on demand) and uses the constructor arguments or setter methods provided to wire together the dependencies. 

Finally, even object-oriented programming is undermined. One bean cannot inherit
from another bean. Notice the logic for adding a new account. It is common in EJB2 beans
to define “data transfer objects” (DTOs) that are essentially “structs” with no behavior.

**EJB**( (Enterprise Java Bean) is **a server-side software element that summarizes business logic of an application**.

In AOP(aspect-oriented programming), modular constructs called aspects specify which points in the system should
have their behavior modified in some consistent way to support a particular concern. This
specification is done using a succinct declarative or programmatic mechanism.

Pure Java AOP Frameworks:  Spring AOP and JBoss AOP,

In Spring, you write your business logic as Plain-Old
Java Objects. POJOs. POJOs are purely focused on their domain. They have no dependencies on
enterprise frameworks (or any other domains).

**Emergence**

According to Kent, a design is “simple” if it follows these rules:
•1-  Runs all the tests:

2–4: Refactoring: 

• 2- Contains no duplication
• 3- Expresses the intent of the programmer(Expressive)
• 4- Minimizes the number of classes and method

******



**Concurrency** 

Concurrency is a decoupling strategy. It helps us decouple what gets done from when it
gets done.  (related to thread )

FOR EXAMPLE  : consider a system that handles one user at a time and requires only one second
of time per user. This system is fairly responsive for a few users, but as the number of
users increases, the system’s response time increases. No user wants to get in line
behind 150 others! We could improve the response time of this system by handling
many users concurrently.

• Concurrency always improves performance.
Concurrency can sometimes improve performance, but only when there is a lot of wait
time that can be shared between multiple threads or multiple processors. Neither situ-
ation is trivial.
• **Design does not change when writing concurrent programs.**
In fact, the design of a concurrent algorithm can be remarkably different from the
design of a single-threaded system. The decoupling of what from when usually has a
huge effect on the structure of the system.
• **Understanding concurrency issues is not important when working with a container**
**such as a Web or EJB container.**
In fact, you’d better know just what your container is doing and how to guard against
the issues of concurrent update and deadlock described later in this chapter.
Here are a few more balanced sound bites regarding writing concurrent software:
• **Concurrency incurs some overhea**d, both in performance as well as writing additional
code.
• **Correct concurrency is complex**, even for simple problems.

• **Concurrency bugs aren’t usually repeatable**, so they are often ignored as one-offs 2
instead of the true defects they are.
• **Concurrency often requires a fundamental change in design strategy.**

Concurrency Defense Principles:

1- Single Responsibility Principle

###### 	• Concurrency-related code has its own life cycle of development, change, and tuning.
• Concurrency-related code has its own challenges, which are different from and often
more difficult than nonconcurrency-related code.
• The number of ways in which miswritten concurrency-based code can fail makes it
challenging enough without the added burden of surrounding application code.
Recommendation: Keep your concurrency-related code separate from other code. 6

2- corollary:Limit the Scope of Data

..... on pdf 

**Producer-Consumer** 

One or more producer threads create some work and place it in a buffer or queue. One or
more consumer threads acquire that work from the queue and complete it. The queue
between the producers and consumers is a bound resource

**Readers-Writers** 

When you have a shared resource that primarily serves as a source of information for read-
ers,

**Beware Dependencies Between Synchronized Methods**
Dependencies between synchronized methods cause subtle bugs in concurrent code.

Recommendation: Avoid using more than one method on a shared object.

Recommendation: Keep your synchronized sections as small as possible.

**Writing Correct Shut-Down Code Is Hard**

Recommendation: Think about shut-down early and get it working early. It’s going to
take longer than you expect. Review existing algorithms because this is probably harder
than you think.

************

**Successive Refinement**

Args is very simple to use. You simply construct the Args class with the input argu-
ments and a format string..If there is a problem, either in the format string or in the command-line arguments
themselves, an ArgsException will be thrown

it is too long 

**********

junit 

factoring SerialDate

**Smells and Heuristics :**

**Comment**

Inappropriate Information

Obsolete Comment

Redundant Comment

Poorly Written Comment

Commented-Out Code



**Functions**

F1: **Too Many Arguments**
Functions should have a small number of arguments. No argument is best, followed by
one, two, and three. More than three is very questionable and should be avoided with prej-
udice. (See “Function Arguments” on page 40.)
F2: **Output Arguments**
Output arguments are counterintuitive. Readers expect arguments to be inputs, not out-
puts. If your function must change the state of something, have it change the state of the
object it is called on. (See “Output Arguments” on page 45.)
F3: **Flag Arguments**
Boolean arguments loudly declare that the function does more than one thing. They are
confusing and should be eliminated. (See “Flag Arguments” on page 41.)
F4: **Dead Function**
Methods that are never called should be discarded. Keeping dead code around is wasteful.
Don’t be afraid





**General**

....

**java**

1-  **Avoid Long Import Lists by Using Wildcards**
If you use two or more classes from a package, then import the whole package with
**import package.*;**
Long lists of imports are daunting to the reader.

2- Don’t Inherit Constants 

This is a hideous practice! The constants are hidden at the top of the inheritance hierarchy.
Ick! Don’t use inheritance as a way to cheat the scoping rules of the language. **Use a static**
**import instead.**

```
public interface PayrollConstants {
public static final int TENTHS_PER_WEEK = 400;
public static final double OVERTIME_RATE = 1.5;
}
```

```
import static PayrollConstants.*;//here

public class HourlyEmployee extends Employee {
private int tenthsWorked;
private double hourlyRate;
public Money calculatePay() {
int straightTime = Math.min(tenthsWorked, TENTHS_PER_WEEK);
int overTime = tenthsWorked - straightTime;
return new Money(
hourlyRate * (tenthsWorked + OVERTIME_RATE * overTime)
);
}
.
```

3-Constants versus Enums

use them! Don’t keep using the old trick of public static final int s.

 enum s carefully. They can have methods and fields.

```java
public class HourlyEmployee extends Employee {
private int tenthsWorked;
HourlyPayGrade grade;
public Money calculatePay() {
int straightTime = Math.min(tenthsWorked, TENTHS_PER_WEEK);
int overTime = tenthsWorked - straightTime;
return new Money(
grade.rate() * (tenthsWorked + OVERTIME_RATE * overTime)
);
}
...
}
public enum HourlyPayGrade {
APPRENTICE {
public double rate() {
return 1.0;
}
},
LEUTENANT_JOURNEYMAN {
public double rate() {
return 1.2;
}
},
JOURNEYMAN {
public double rate() {
return 1.5;
}
},
MASTER {
public double rate() {
return 2.0;
}
};
public abstract double rate();
```

**Names**

1-**Choose Descriptive Names**

The power of carefully chosen names is that they overload the structure of the code
with description. That overloading sets the readers’ expectations about what the other
functions in the module do.

2-**Choose Names at the Appropriate Level of Abstraction**

**3-Use Standard Nomenclature Where Possible**

4-**Unambiguous Names**

5-**Use Long Names for Long Scopes**
The length of a name should be related to the length of the scope. You can use very short
variable names for tiny scopes, but for big scopes you should use longer names.

6-**Avoid Encodings**

7-**Names Should Describe Side-Effects**

**Tests :** 

Insufficient Tests

2: Use a Coverage Tool!

Don’t Skip Trivial Tests

Test Boundary Conditions

An Ignored Test Is a Question about an Ambiguity

Exhaustively Test Near Bugs

Patterns of Failure Are Revealing

Test Coverage Patterns Can Be Revealing

Tests Should Be Fast