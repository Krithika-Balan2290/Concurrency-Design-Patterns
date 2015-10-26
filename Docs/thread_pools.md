#Thread Pools
The thread pool pattern is where a number of threads are created to perform a number of tasks, which are usually organized in a queue. The results from the tasks being executed might also be placed in a queue, or the tasks might return no result. Typically, there are many more tasks than threads. As soon as a thread completes its task, it will request the next task from the queue until all tasks have been completed. The thread can then terminate, or sleep until there are new tasks available.

If the number of tasks is very large, then creating a thread for each one may be impractical.

Another advantage of using a thread pool over creating a new thread for each task is thread creation and destruction overhead is negated, which may result in better performance and better system stability. Creating and destroying a thread and its associated resources is an expensive process in terms of time. An excessive number of threads will also waste memory, and context-switching between the runnable threads also damages performance. For example, a socket connection to another machine—which might take thousands (or even millions) of cycles to drop and re-establish—can be avoided by associating it with a thread which lives over the course of more than one transaction.

When implementing this pattern, the programmer should ensure thread-safety of the queue. In Java, you can synchronize the relevant method using the synchronized keyword. This will bind the block modified with synchronized into one atomic structure, therefore forcing any threads using the associated resource to wait until there are no threads using the resource. As a drawback to this method, synchronization is rather expensive. You can also create an object that holds a list of all the jobs in a queue, which could be a singleton.

Typically, a thread pool executes on a single computer. However, thread pools are conceptually related to server farms in which a master process, which might be a thread pool itself, distributes tasks to worker processes on different computers, in order to increase the overall throughput. Embarrassingly parallel problems are highly amenable to this approach.
![image](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0c/Thread_pool.svg/400px-Thread_pool.svg.png)
<Text Here>

[Prev Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/rw_lock.md) | [Next Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)
 
 [Back to contents](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Index.md)
