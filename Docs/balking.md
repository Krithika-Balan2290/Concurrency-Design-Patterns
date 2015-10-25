#Balking Pattern

The Balking patter is a software design pattern that helps to deal with incomplete or inconsistent states of shared objects. The balking patterns allows certain blocks of code to execute only if the object is in a certain state. This means that in other states the code would not be executed or a different block of code would be executed. When they are in unacceptable states, the objects tend to “balk” at execution of the code.
A balking pattern is typically used in a single threaded execution pattern in order to synchronize object accesses to its state. A Single threaded execution pattern is a concurrency patterns which does not allow portions of code to be executed concurrently. These portions of code would be then be synchronized on the shared object. The balking pattern checks if the shared object is in a particular state and only then allows execution of the code.
The following example demonstrates the balking pattern<sup>[3]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>:
```
public class Example {
    private boolean jobInProgress = false;

    public void job() {
        synchronized(this) {
           if (jobInProgress) {
               return;
           }
           jobInProgress = true;
        }
        // Code to execute job goes here
        // ...
    }

    void jobCompleted() {
        synchronized(this) {
            jobInProgress = false;
        }
    }
}
```

Here, the class Example is the shared object which is synchronized using the Balking Pattern. Since the code blocks inside the functions *job()* and *jobCompleted()* are synchronized, only one thread can execute it at a time. This means that only one thread can update the value of the variable *jobInProgress* at any time. So, the job gets executed only if the job is not already being executed. Effectively the block of code which accesses the shared object is implemented by only one thread at a time, resulting in the implementation of the Single Threaded Execution Pattern.

The Balking pattern is considered to an anti-Pattern rather than a true design pattern. If the object is not in the correct state, then the object must not even allow an improper call to a function on that object or else it should be able to handle the call in a concurrent manner instead of making the execution single threaded. The Balking pattern is also not recommended when object would be in an inappropriate state for a known amount of time<sup>[4]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.


[Prev Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/active.md) | [Next Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/barriers.md)
 
 [Back to contents](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Index.md)
