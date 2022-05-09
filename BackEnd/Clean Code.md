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

* Interface and implementation :   IShapeFactory and ShapeFactory? I prefer to leave interfaces unadorned. ShapeFactory is preffered .  So if I must encode either the interface or the implementation, I choose the implementation -> ShapeFactoryImp 0r CShapeFactory

* Class Names :Classes and objects should have noun or noun phrase names like Customer, WikiPage ... ,class name should not be a verb.

* Methods Names:   should have verb or verb phrase names like postPayment, deletePage, or save. prefixed with get, set, and is 

* Say what you mean. Mean what you say

* dont pun :Avoid using the same word for two purposes “one word per concept”.

  
