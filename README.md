**@AfterThrowing Advice - Interaction**


<img src="https://user-images.githubusercontent.com/80107049/189733734-d1499304-a6c4-469c-8384-80fe8b396cff.png" width=500 />

<img src="https://user-images.githubusercontent.com/80107049/189733882-f9ce898e-cac2-4f05-8e9a-5bbeea8b84a2.png" width=500 />



**Sequence Diagram**

<img src="https://user-images.githubusercontent.com/80107049/189734027-ed550f62-b69a-470a-be9b-17d2d851c4e8.png" width=500 />



**Use Cases**

+ Log the exception
+ Perform auditing on the exception
+ Notify DevOps team via email or SMS
+ Encapsulate this functionality in AOP aspect for easy reuse

**Example**

+ Create an advice that will run after an exception is thrown

<img src="https://user-images.githubusercontent.com/80107049/189734086-d61057a6-afa9-4ae1-8157-00af9d70fade.png" width=500 />



+ This advice will run after an exception is thrown

```JAVA
@AfterThrowing("execution(* com.tilmeez.aopdemo.dao.AccountDAO.findAccounts(..))")
public void afterThrowingFindAccountsAdvice() {
  
  System.out.println("Executing @AfterThrowing advice");
  
}
```
**Access the Exception object**

+ Need to access the exception object

```JAVA
@AfterThrowing(
  pointcut="exection(* com.tilmeez.aopdemo.dao.AccountDAO.findAccounts(..))",
  throwing="theExc")
public void afterThrowingFindAccountsAdvice(
  JointPoint theJointPoint, Throwable theExc) {
  
  // log the exception 
  System.out.println("\n=====>>> The exception is: " + theExc);
    
}
```

**Exception Propagation**
+ At this point, we are only intercepting the exception(reading it)
+ However, the exception is still propagated to calling program
+ If we want to stop the exception propagation
  + than use the **@Around** advice

**Development Process - @AfterThrowing**
1. In Main App, Add try/catch for exception handling
2. Modify AccountDAO to simulate throwing an exception
3. Add @AftterThrowing advice

