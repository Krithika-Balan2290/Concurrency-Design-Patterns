#Reactors

The Reactor design pattern handles service requests that are delivered concurrently to an application by one or more clients. Each service in an application may consist of several methods and is represented by a separate event handler that is responsible for dispatching service-specific requests. Dispatching of event handlers is performed by an initiation dispatcher, which manages the registered event handlers. Demultiplexing of service requests is performed by a synchronous event demultiplexer.
##Participants:
The key participants in the Reactor pattern include the following: 
###Handles
 Identify resources that are managed by an OS. These resources commonly include network connections, open files, timers, synchronization objects, etc. Handles are used in the logging server to identify socket endpoints so that a Synchronous Event Demultiplexer can wait for events to occur on them. The two types of events the logging server is interested in are connection events and read events, which represent incoming client connections and logging data, respectively. The logging server maintains a separate connection for each client. Every connection is represented in the server by a socket handle. 
###Synchronous Event Demultiplexer 
 Blocks awaiting events to occur on a set of Handles. It returns when it is possible to initiate an operation on a Handle without blocking. A common demultiplexer for I/O events is select [1], which is an event demultiplexing system call provided by the UNIX and Win32 OS platforms. The select call indicates which 2 Handles can have operations invoked on them synchronously without blocking the application process. 
###Initiation Dispatcher
 Defines an interface for registering, removing, and dispatching Event Handlers. Ultimately, the Synchronous Event Demultiplexer is responsible for waiting until new events occur. When it detects new events, it informs the Initiation Dispatcher to call back application-specific event handlers. Common events include connection acceptance events, data input and output events, and timeout events. 
###Event Handler 
Specifies an interface consisting of a hook method [3] that abstractly represents the dispatching operation for service-specific events. This method must be implemented by application-specific services. 
###Concrete Event Handler 
  Implements the hook method, as well as the methods to process these events in an application-specific manner. Applications register Concrete Event Handlers with the Initiation Dispatcher to process certain types of events. When these events arrive, the Initiation Dispatcher calls back the hook method of the appropriate Concrete Event Handler. There are two Concrete Event Handlers in the logging server: Logging Handler and Logging Acceptor. The Logging Handler is responsible for receiving and processing logging records. The Logging Acceptor creates and connects Logging Handlers that process subsequent logging records from clients. The structure of the participants of the Reactor pattern is illustrated in the following OMT class diagram:
![image](http://dos.iitm.ac.in/OOSD_Material/OOSWLifeCycle/Reuse%20Mechanisms/Architec%20patterns/img/img1.jpg)
[10]

<Text Here>

[Prev Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/monitor.md) | [Next Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/rw_lock.md)
 
 [Back to contents](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Index.md)
