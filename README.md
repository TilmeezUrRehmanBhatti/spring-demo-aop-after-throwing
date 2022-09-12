**@AfterThrowing Advice - Interaction**

<img src="inkdrop://file:Q4mDQwaJY" width=5/>


<img src="inkdrop://file:KlNwnGuTV" width=500 />



**Sequence Diagram**

<img src="inkdrop://file:deM53xuUD" width=500 />


**Use Cases**

+ Log the exception
+ Perform auditing on the exception
+ Notify DevOps team via email or SMS
+ Encapsulate this functionality in AOP aspect for easy reuse

**Example**

+ Create an advice that will run after an exception is thrown

<img src="inkdrop://file:UZkcC9Lo9" width=500 />



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

