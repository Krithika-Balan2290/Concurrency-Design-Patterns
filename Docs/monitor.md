#Monitor Object
Monitor object is a behavioral pattern design by which the methods are synchronized such that only one method runs with an object at a time. It also allows the objects, method to cooperatively schedule their methods for sequential execution. This pattern is also known by the name of Thread- safe Passive Objects. 

##Solution:
For each object accessed concurrently by client threads define it as a monitor object. Clients can access the services of a method only if the method is snychronised.  To prevent race conditions involving monitor object state, only one synchronized method at a time can run within a monitor object. Each monitored object contains a monitor lock that synchronized methods use to serialize their access to an object’s behavior and state. In addition, synchronized methods can determine the circumstances under which they suspend and resume their execution based on one or more monitor conditions associated with a monitor object.

##Structure
 There are four participants in the Monitor Object pattern:
### Monitor object 
A monitor object exports one or more methods to clients. To protect the internal state of the monitor object from uncontrolled changes or race conditions, all clients must access the monitor object only through these methods. Each method executes in the thread of the client that invokes it because a monitor object does not have its own thread of control. For instance, the consumer handler’s message queue in the Gateway application can be implemented as a monitor object. 
###Synchronized methods 
 Synchronized methods implement the thread-safe services exported by a monitor object. To prevent race conditions, only one synchronized method can execute within a monitor at any point in time, regardless of the number of threads that invoke the object’s synchronized methods concurrently or the number of synchronized methods in the object’s class.
### Monitor lock 
 Each monitor object contains its own monitor lock. Synchronized methods use this monitor lock to serialize method invocations on a per-object basis. Each synchronized method must acquire/release the monitor lock when the method enters/exits the object, respectively. This protocol ensures the monitor lock is held whenever a method performs operations that access or modify its object’s state. Synchronized methods use monitor conditions to determine the circumstances under which they should suspend or resume their processing. 


<Text Here>

[Prev Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/suspension.md) | [Next Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/reactor.md)
 
 [Back to contents](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Index.md)
