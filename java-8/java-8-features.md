# JAVA 8 

## What are the java 8 features ?
There are a couple of the features are introduced in the java 8 version. Some of the major features which we can tell in the interview. Make sure that if you have not used that feature and not know in depth of it (how to use and when to use) then tell the interviewer that you know about it but not got chance to work on it.

1. Lambda Functions
2. Functional interfaces 
3. Stream APIs 
4. Optional Class 
5. Default and static methods 
6. JVM memory changes - Introduced Metaspace instead of the PermGen Memory 
7. Date changes - Introduced LocalDate, LocalDateTime etc.

### Let's discuss the one by one of every feature

#### Lambda Functions
- Lambda expression is best feature introduced in the java 8.
- Lambada expression is the shortcut or short code for the implementation of the method.
- Earlier we have to implement anonymous class  if we want to provide the implementation of any method without implementing in any class.
  e.g. 
      `Runnable runableImpl = new Runnable(){
        @Override
        public void run(){
          // Add the implementation for this here 
            }
         }`
- Now with the lambda expression we can provide the implementation of the method without defining the name of the class as well as the name of the method.
    e.g. 
 `Runnable runnable = () -> System.out.println("This is the implementation");`
- This will be very cleaver way for providing the implementation to the interface methods.

Syntax 
1. No parameter
   `() -> {\\body}`
2. Single parameter
   `(param1) -> { \\body }`
3. Multiple parameters
   `(param1 , param2) -> { \\body }`

- In the lambda expression we don't need to provide the return type. it implicitly identified by the method available in the interface.
- Also with the lambda expression we can pass the implementation of the method to the another method call as well to run.
  e.g.
    ```
  public void anymethod(Runnable runnable){
     runnable.start();    
  }
  ```
// method call
  `anyMethod(() -> System.out.println("Thread is started"));`

### Functional Interfaces
- In the above we see that how lambda provide the easy way to provide the implementation to the interface methods without defining of the name of the class and the method.
- And lambda internally identify the method.
- This is only possible that if the interface is contains the single abstract method. And this is call the functional interfaces. 
- The interfaces which contains the single abstract method and can have multiple default or static method is called the functional interfaces.

###### Existing functional interfaces 
- Supplier , consumer , predict and function
- Runnable, Callable , Comparable and Comparator are also a functional interfaces

We also can create custom functional interface. By adding only one abstract method in the interface.
Also you can annotate as `@FunctionalInterface` to the interface level. It will add the compile time restriction to the interface if anyone try to add the more than one abstract method in it then it will not compile successfully. 

```
@FunctionalInterface
public interface MyOwnFunction{
    public void someFunction();
    public void default defaultFunction(){
        // provide the body to it.
    }
}
```

#### Default methods and Static Methods
- As we know that the interface can contains only the abstract method (which does not contains the body). and we can implement this method from the interface.
- and suppose if we want to add some more functionality in the interface then we have to provide the implementation for that method to all the classes who has implemented this interface.
- This is not the backward companionable and also were we don't want this functionality there also we need to add the implementation.
- like Person is the interface which have method called identity and it implemented in Employer and Student class. Now I want to add the functionality of Salary which we want only in the Employer in that we case if we added it in interface then we have to provide the implementation for the both of classes.
- This will be resolved by the default methods. were you can add the default method in interface and add the implementation to that methods as well. And you provide the implementation to specific classes only.
- e.g. in above case we can have the default method called salary and can be implemented in the Employee only not in student.
- one benefit of the default method is that it will be reduce of having te utility class all that you can add it in the interface level only which can be consumed.

`interface Person{
    public void identity();

    public default void salray(){
        // default impl
    }
}`

`class Employee implements Person{
    
    @Override
    public void identity(){
    }
    
    @Override
    public default void salray(){
        // default impl
    }
    
}`

In the Student class we don;t need to provide the implementation for the salary method.
```
class Student implements Person{
    @Override
    public void identity(){
    }
}
```

###### Problem occured due to the default methods : 

Daimond Problem - 
- This means that as we know that we can have the default method in the interface which contains the body. and we can implement the multiple interfaces to the class. 
- So in this case the problem is that if suppose that you have two interfaces which contains the same default method with same name and signature and you implemented these interfaces to the class.
- and if you try to create the object and call that default method from the interface then it is not possible as compiler does not know which method should be called from interface 1 or 2. 
- To solve this you have to override the default method in class and call the specific implementation from interface 1 or 2.

Solution - 

```
public class Test implement Interface1 , Interface2{
    
    @overide
    public default void addSome(){
        Interface1.super.addSome(); // call the specific implementation from interface
    }
}
```

Static Methods : 
- On the similar to the default methods. Static methods can have body in the interface.
- But the main difference is that the static methods can not be override into the subclass similar to the default methods.
- static methods basically work as the utility for the any functionality.
- Diamond problem will not be existed with the static methods as becuase this method can be only available with interface name. we can not call this on the sublcass implementation object.
- you can call the static methods in the interface default method as well. Without mentioning the interface name.

```
pulic interface StaticInt{

    public void static isNull(Object obj){
        return obj == null;
    }
    
    public void abstractMethod();
    
    default void printTheMessage(String message){
        isNull(message);
        System.out.println("Hello. Here is your message : " + message);
    }
}

// Implementation for the interface

public class StaticIntImpl implements StaticInt{
    
    @override
    public void abstractMethod(){
        StaticInt.isNull(anyObje);
    }    
}
```
#### Optional Class
