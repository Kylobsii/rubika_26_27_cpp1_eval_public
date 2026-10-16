# Theorical questions

[Back to main README](../README.md)

1. What are the steps involved in the compilation process?

Here are all the steps involved in the compilation process :
- Pre-processing : At this step the pre-processor checks for every pre-compilation instruction (lines starting with #, like includes, ifdef, define, etc.). Once every of those instructiosn are resolved, each scripts are turned into a .obj file, able to run on its own (included code for references have been copied)
- Compilation / Assembling : The code is then translated into assembler, and finally into a binary language the computer can run.
- Linking : The linker's role is to group all scripts of the solution into one library (dll, dynamic link library) where scripts are linked with each other. It is also the step that generates the .exe file, used to open the programm

2. What is the difference between a declaration and a definition?

A declaration is what holds the signature of a method. It dictates what's its name, and the ones of its parameters. It also defines its return type, its range (public/protected/private), and what's constant. It is located in the header file.
The definition implements that declaration and tells what to do when it is called. It must abide by the declarations specifities (names of params, constantness, return type ...). It is generally located in the cpp file, but in theory can be implemented directly in the header (although it is a bad practice for most cases).

3. What is the difference between passing a parameter by value, by reference, and by pointer?

A value is passed to a method through parameters so that it can be used within its scope. Passing it by value means that the parameter will hold a one-to-one copy of the said value. This way, the method never takes hold of the original variable. Passing a parameter by pointer means that the parameter will hold an adress pointing at the exact location of the desired value in memory. This pointer can then be dereferenced to access the data stored at the pointed adress. A pointer can be null (not pointing to anything). Passing a parameter by reference, means that the parameter will hold a direct link to the variable holding the value. A reference cannot be null and thus it ensures the actions made to the stored value through the reference won't fail.

4. What is the difference between the stack and the heap?

The stack and heap are two par of the program's allocated memory that served different purposes :
- The stack is used for temporary values, generally with a short life-span (for example local variables). It is more light-weight and thus allows for faster acces to the memory it stores.
- The heap is used for more long-term variables, meant to stay even outside the scope of the method that initilized the value. It generally takes a bit longer to access the memory stored inside the heap, but it guarantees the variable stays alive. To store a value inside the heap, it muse be initialized with the 'new' key word (new MyClass(), instead of just MyClass()). A major difference between heap-stored variable and stack-stored ones is that every value in the heap must be deleted manually before destroying its pointer or reference. If it isn't done, the value stays in the heap with no way to access it, meaning no way to clear it. This case is called a memory leak.

5. What is the difference between struct and class in C++?

Both struct and classes can hold variables, and declare methods. The main differences come with the default range of their elements, and also what they are most used for. The default range of the elements of a class is Private, it generally is used for logic driven elements. The elements of a struct on another hand are public by default, and the struct itself is generally used only to store a specific group of variable.

6. What is the difference between the public, protected, and private access specifiers?

These access specifiers modify the range of the element they precede. A public element is accessed by everyone as long as they can be referenced. A protected element is access by the class implementing it, and by its derived children. Protected elements are generally used for logic that only concerns the children and the class itself, and that no outside element should interfere in. And finally, private elements are only accessed by the class implementing it. 

7. What is a pure virtual function? What effect does it have on a class?

A pure virtual function is a method declared by a parent class but that won't be defined by it, and only by its children. It is written with a '= 0' at the end. The main use for these is to ensure that the parent class is only used as a sort fo interface, as it prevents the class that declares them to be instantiated.

8. Briefly explain the diamond problem in multiple inheritance.

Whenever a class inherits from another class, it calls the constructor of its parent. This means that in the memory storing the derived class, there is actually a succession of the parent class memory space then the one of the class itself. Cpp allows for multiple inheritance, meaning there is nothing preventing a class from inheriting from two or more classes. Now, imagine a case where we have a base class called 'Base'. Then we have two classes 'BaseA' and 'BaseB' that each inherit from it. Finally let's say we have a final class 'MyClass' that inherits from both 'BaseA' and 'BaseB'. In that case, 'MyClass' will have to call the constructors of both its parents, which will themselves both call the constructor of 'Base', effectively creating two different copies of 'Base' for a single element. This causes a major problem which is that if 'MyClass' wants to access a variable declared by 'Base', it will have no way of knowing from which instance of 'Base" to chose from. This can be fixed by adding the 'virtual' keyword in front of the declaration fo the class 'Base' so that inheritance will make sure it is only instantied once in a case fo multiple inheritance.

9. Name the different containers studied in class and describe the strengths and weaknesses of each.

- Vector : Continuous (all elements side by side, easy to iterate through) and dynamic. Adding a new element is heavy because the entire vector is moved to a place in memory with enough space for the new element.
- List : Discontinuous (fragmented memory) but dynamic. Iterating through is slow because there is no way other to go straight to the desired index (i) than by passing through i elements. Allows form insertion, meaning a new element can be added at any place within the list. Is a bit heavier than other containers because elements needs to store pointers to the next element (and previous in a 2-way list)
- Array : Continuous but not dynamic (has a fixed size). Least heavy for the computer because memory is allocated once at the initilisation, easy to iterate through. 
- map : Hash driven, meaning values are stored at a location given by the key once hashed. Very easy to browse, but slow to iterate through. Potential risk of hash collisions.
- Stack : a pile of elements where the first in si the last out (FILO)
- Queue : a group of elements where the first in is the first out (FIFO)

10. For each of the following scenarios, identify the most appropriate container and justify your choice.
- You need to store the top ten scores in a game. The number of elements is known and will never change.
=> Array
- You need to manage a queue of tasks that must be executed in the order they arrive.
=> Queue
- You frequently need to insert and remove elements in the middle of a sequence.
=> List
- You need to store a large number of elements and frequently check whether a particular element exists. The order of the elements does not matter.
=> Map if there is a way to have a key, if not then vector
- You need to keep track of actions so that the most recent action can be undone before earlier actions.
=> Stack
- You need to manage a collection of players whose number can change over time, with frequent read and traversal operations.
=> Vector
- You need to associate each student ID with a grade and retrieve a grade quickly using the student ID.
=> Map