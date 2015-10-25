#Concurrency Design Patterns

Concurrency design patterns are the patterns of solutions of problems faced during concurrent programming. Some of these patterns are described in the following sections.

#Active Object

The Active Object design pattern, also known as the concurrent object design pattern, decouples method execution from method invocation to enhance concurrency and simplify synchronized access to objects that reside in their own threads of control<sup>[2]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.

As concurrency continues to gain popularity, the problem of synchronizing accesses by concurrent threads to shared data and methods becomes much more significant. The solution to the synchronization problem must be able to handle the following:
+ Process-intensive threads must not hog access to a particular object and block access to other threads for a long time.
+ Programing the synchronized access to shared memory items must be straightforward. 
+ The applications must be designed to take advantage of the parallelism already available on the platform being used for development.

The solution to this problem is to separate the method invocation on a shared object from its execution. The method invocation must occur in the client thread whereas the method itself must be executed in a separate thread. This separation must be implemented in such a way that it looks like the client thread is just invoking a normal method.
An active object consists of six components:
######Proxy:
A proxy is an interface which represents the shared object. It is present in the client threads and it allows the client threads to call methods on the shared object.
######Method Request:
When a client thread invokes a method, provided by the proxy, on the active object, it creates an object of the *Method Request* class. This class contains information regarding the execution of methods, such as the parameters passed to it and the return values. The Method Request class also checks for some guard conditions which determine whether the method can be executed. The *Method Request* class is implemented by a subclass called “Concrete Method Request” class for the specific method invoked by the client thread.
######Activation List:
The *Activation List* is a list of all concrete method requests that are currently pending execution. When the proxy creates a concrete method request, it adds it to the *Activation List* so that it can be scheduled for execution. This allows the client thread to continue execution without having to depend on the execution of the method invoked on the shared object.
######Scheduler:
The scheduler runs in the active object’s thread where it picks up the method from the activation list to be executed next on the active object. The scheduling decision is based on criteria such as the order in which the methods were invoked or the state of the active object. It uses a method’s guard conditions to check these criteria and decide which method to execute next. 
######Servant:
A servant method is the interface between the proxy and the actual implementation of the method being called. It is invoked when the scheduler picks up a method request for execution and so, it runs on the scheduler’s thread. The scheduler also has some methods which help the Method Request objects verify if the particular method can be executed.
######Future:
A Future is an object in which the servant stores its result once it finishes executing. When a client thread wants to access the result of a method execution, it checks the future for the result. The client thread can either poll the future until a result is available or it can block until the servant completes execution and stores the result in the future object.


[Prev Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/structural.md) | [Next Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/balking.md)
 
 [Back to contents](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Index.md)
