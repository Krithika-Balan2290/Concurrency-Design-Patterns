#Guarded Suspension

Guarded suspension is a concurrent design pattern that requires a lock to be acquired and a precondition to be satisfied before the operation can be executed. The guarded suspension is typically applied to method blocks where the method call and the calling is suspended until the precondition or the guard condition is satisfied.
Guarded suspension is used only when the developer is aware of the fact that the method call will be suspended for a finite or known amount of time. If the wait period to satisfy the wait condition is too long then program takes a long time to execute or the program may stop. If the developer knows that this is the problem that he is going to face, then he may choose other concurrent models over this one.

###Implementation:

```

Below is a program in Java to show the implementation shows the implementation of the guarded suspension:
 public class Example {
   synchronized void guardedMethod() {
    while (!preCondition()) {
     try {
       //Continue to wait
       wait();
      //…
      } catch (InterruptedException e) {
     //…
     }
   }
   //Actual task implementation
   }
   synchronized void alterObjectStateMethod() {
     //Change the object state
     //…..
     //Inform waiting threads
     notify();
   }
}

```

The wait() and the notify() method are used to assist the guarded suspension
Wait() is used to detect when there are no items in the queue. Once the other method notifies the other methods the  wait() can exit the guarded state and proceed with a call. Once the queue is empty the  wait() will enter the guarded state again.
![image](http://openhome.cc/Gossip/DesignPattern/images/GuardedSuspension-1.jpg)

<Text Here>

[Prev Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/double_lock.md) | [Next Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/monitor.md)
 
 [Back to contents](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Index.md)
