useful Links : 1- https://www.baeldung.com/solid-principles#l  

  

**design principles encourage us to create more maintainable, understandable, and flexible software**

1. **S**ingle Responsibility
2. **O**pen/Closed
3. **L**iskov Substitution
4. **I**nterface Segregation
5. **D**ependency Inversion

---> **Single Responsibilit**y : 

benifits :

 	1- Testing : will have fewer test cases . 

​	2- Lower coupling : fewer dependencies . 

​	3- organization : it is small so it is easier to search  . 

* the mwethods that direct relate to class properties(data filed ) we put it inside the class . but if we have a method that will deal with a task (like printing ,formmating ,etc) we need another class that responsiple for implement this task ( single responsipility) , then we can use this class in another classes if we need it without the basic class 

---> **Open for Extension, Closed for Modification**  . 

if we want to add features to class but we may have bugs and errors . so the best solution is to create a class with new feature and make it extend the original class without modifies it  

---> **Liskov Substitution** . i(f class A is a subtype of class B, we should be able to replace B with A without disrupting the behavior of our program.)  ( “[subclass](https://web.archive.org/web/20150906155800/http://www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf)[es](https://web.archive.org/web/20150906155800/http://www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf)[ should be substitutable for their base classes](https://web.archive.org/web/20150906155800/http://www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf)“,) 

  for example : if we have interface that has a specific behavior and there is an form implementation that belong to this behavior . but if we have another form it is belong to this interface b but not belong ti its behavior ( methods ) here we have a problem ( we will change the behavior of the program because we will implement any thing for the methods ) . the solution is   rework our model into interfaces  that has all behaviors 

----> **Interface Segregation** :   **larger interfaces should be split into smaller ones** . 

let say we have interface that have more than one methods . and if we normal class cannot implement all these methods . so we will split it into interfaces (each method for each interface ) . then this normal class will implements the interfaces that can implement and other classes will implement the other that needed

--->**Dependency Inversion** : **This way, instead of high-level modules depending on low-level modules, both will depend on abstractions.** 

if we have high-level-class and low level classes . and hig-level depends on low-lwvwl . if we hava low-level classes as classes and with it functionalit . if we want to add or modifiy or make another version or type   of it we must change it and chang  the dependencies inside high level . the sol is to mak an intefac from low level and declar it inside higlevelas (with name of interface) so we can we can easily switch out the type of low-level 

