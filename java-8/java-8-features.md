# JAVA 8 

## What are the java 8 features ?
There are couple of the features are introuduced in the java 8 version. Some of the major features which we can tell in the interview. Make sure that if you have not used that feautre and not know in depth of it (how to use and when to use) then tell the interviewer that you know about it but not got chance to work on it.

1. Lambda Functions
2. Stream APIs
3. Optional Class
4. Default and static methods
5. Functional interfaces
6. JVM memory changes - Introduced Metaspace instead of the PermGen Memory
7. Date changes - Introduced LocalDate, LocalDateTime etc.

### Let's discuss the one by one of every feature

#### Lambda Functions
- Lambda expression is best feature introduced in the java 8.
- Lambada expression is the shortcut or short code for the implementation of the method.
- Earlier we have to implement annonoumous class  if we want to provide the implementation of any method without implementing in any class.
  e.g. 
      `Runnable runableImpl = new Runnable(){
        @Override
        public void run(){
          // Add the implementation for this here 
            }
         }`
- Now with the lambda expression we can provide the implementation of the method without defininf the name of the class as well as the name of the method.
    e.g. 
 `Runnable runnable = () -> System.out.println("This is the implementation");`
- This will be very cleaver way for prividing the implementation to the inetrface methods.

Syntax 
1. No parameter
   `() -> {\\body}`
2. Single parameter
   `(param1) -> { \\body }`
3. Multiple parameters
   `(param1 , param2) -> { \\body }`

- In the lamdaba expression we don't need to provide the return type. it implicitly identified by the method available in the interface.
- Also with the lambda expression we can pass the implementation of the method to the another method call as well to run.
