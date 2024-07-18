[### Basic questionary --

## SOLID principles

1. S - Single responsibility principle -
   This principle means that class should have the single responsbility. Which means that it should have single reason
   to change the implementation.
   example - Suppose that we have an class called as the Student which will be have actions such as the name age
   division and also calculating the marks. Now here it is viovlating the SRP as mark is the different responsbility
   than the student calass. so that the calculation of the marks should be in the different class.
2. O - Open for extension and closed for the modification
   This means that the class should be open for the extensions of the additional functionalities but it should be closed
   for the modification in the existing code. This is will be not applied for the bug fixes.

   In the below example if you see that we have the different payment methods and this will be violating the principal
   of the open and clsed as if suppose in the future if i want to support the new method of the payment then we have to
   chnage in existing code.
   `` public class MakePayment{

           public void pay(String typeOfPayment){
               switch (typeOfPayment){
                   case "UPI" :
                       // perform the opertion
                       break;
                   case "Netbanking" :
                       // perform the opertion
                       break;
                   default:
                       // some default try
               }
           }
   }``

   Here is the solution which needs to be applied :
    ```
     interface Payment{
   public void pay();
   }

   class UPIPayment implements Payment{

        @Override
        public void pay() {
        }
   }

   class NetBanking implements Payment{

        @Override
        public void pay() {
        }
   }
   ```
3. Liskov substitution -
   This principle is that subclass should be the substitution of the parent class without changing an any behvior. like
   if suppose we have class A which is the subtype of the class B, so we should be able to replace the class B with A
   without disturbing the behavior of class A.

```
   class Rectangle {
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int calculateArea() {
        return width * height;
    }
```

above example will violoate the principle of the liskov substituation. As if you see that in the square we are changing
the implementation of the overriden methods which will be change the behvior of the rectangular. So if we replace the
rectangular with the square then it will behave differently
Here is the solution which we can apply for this.

```
class Square extends Rectangle {
@Override
public void setWidth(int width) {
this.width = width;
this.height = width;
}

    @Override
    public void setHeight(int height) {
        this.width = height;
        this.height = height;
    }

}

```

4. I - Interface segregation -  
   In this principle we should be split the larger interface into the multiple small interfaces. Which help to implement
   the interfaces which they are actually intrested in it instead of implementing un required things.
   for e.g.

```
interface Document {
    void create();
    void edit();
    void save();
    void print();
}

class TextDocument implements Document {
    // ...implement all methods
}

class PDFDocument implements Document {
    // ...implement all methods except edit()
}
```

Now the above example is not follow the interface segregation as pdf documents are not editted but due to this is
present in the interface we have to impement it in the pdf dcoument class as well.
How we can solve is

```
interface EditableDocument {
    void edit();
}

interface PrintableDocument {
    void print();
}

interface Document {
    void create();
    void save();
}

class TextDocument implements EditableDocument, PrintableDocument, Document {
    // ...implement relevant methods
}

class PDFDocument implements PrintableDocument, Document {
    // ...implement relevant methods
}
```

5. Dependecy inversion
   Entities must be depend on the abstraction and not on the low level module. which menas that high level module must
   not be depend on the low level module
   example

```
class FileLogger {
    public void log(String message) {
        // log message to a file
    }
}

class LogManager {
    private FileLogger fileLogger;

    public LogManager() {
        this.fileLogger = new FileLogger();
    }

    public void logMessage(String message) {
        fileLogger.log(message);
    }
}
```

In this example if you see that the LoManager is directly dependent on the FileLogger which is violating the principle
of the D.
So we can solve this by

```
interface Logger {
    void log(String message);
}

class FileLogger implements Logger {
    // ...implement log()
}

class LogManager {
    private Logger logger;

    public LogManager(Logger logger) {
        this.logger = logger;
    }

    public void logMessage(String message) {
        logger.log(message);
    }
}
```

-------------

## OOPS Concepts

1. Abstractions -

Abstractions means that hiding of the internal architectual/implementation from the user and exposing the simple things.
Which will be makes the client life easy.
Great example of the abstraction is that microwave in this user just needs to be put the food in the microwave and
start by clicking on the button. Whatever the internal implementation of the microwave to heat the food which is not
required to understand the user and which is not exposed to the user.

There are data abstraction and process abstraction
In the data abstraction we can hide the access of the data by making them as the private and exposing of the getter
setter methods.
and in the process abstraction as in the example we can expose simpler processes to user like start the microwave and
stop and internal implementation such as take oil then start the heater then wai for the 10 mins which will be hidden
from the user.

2. Encapsulation

Encapsulation is protective barrier which will safe the data and code together. Which means that practically making an
the fields are private and providing an access of the fields by exposing the public methods.
In the java encapsulation is implemented by using an access modifiers. and exposing the getter method to provide the
access of class members.

#### Access modifiers

1. private - resticted to the class level only
2. protected - resticted to the class level, accessisble in same package and subclasses (same and diff package)
3. public - no resticion
4. default - if you have not mentioned the access modifier then it will be default. and resticted to the class level and
   in same package.

3.Inhiritance

Inhiritance is inherating the properties from the one class to the another class. class which is inheriting the
properties is called as the subclass or the child class and another is parent class.
This is used to resuse the same code and also help to apply the polymorphysam. which means that we can have the multiple
child classes which can assigned to the parent classes.
Child class can override the behavior of the praent class and also can have their seperate fields as well.
We can use extend keyword to override the parent class. All the public and protected members are accessible in the child
class.

4. Polymorphisam

Polmorphisam means that the functionality of the object is same but it changes based on the situations. So there are two
type of the polymorphisam. compile time polymorphisam (method overloading) and runtime polymorphisam (method overriding)
Method overloading is that were we can he method in the same class which provide the same functionality but different in
different sutuations.

```
public void draw(){
		System.out.println("Drwaing circle with default color Black and diameter 1 cm.");
	}
	
	public void draw(int diameter){
		System.out.println("Drwaing circle with default color Black and diameter"+diameter+" cm.");
	}
	
	public void draw(int diameter, String color){
		System.out.println("Drwaing circle with color"+color+" and diameter"+diameter+" cm.");
	}
```

Method overriding is that inhiritance the properties and behavior of the parent class to the subclass. in the above case
compiler will know that which methods needs to be called as the name is same but it has the different argumnets. but in
runtime poly the class or object will be decided whether is parent or any child to be called.

_Important Notes :_ 

1. return type is not considered for the method overloading. 
2. if child class method is throws the compiletime exception then it needs to be handled or thrown by the parent class methods as well. for the runtime exception it not needs to be handled on the parent class level.
3. But if parent class throws any exception then it not needs to be mention on the child class method.
4. In case of the method overriding return type should be same as ther parent method.