#Double Checked Locking

The Double-Checked Locking Optimization design pattern reduces contention and synchronization overhead whenever critical sections of code must acquire locks in a thread-safe manner just once during program execution<sup>[9]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.

The most common problem associated with concurrent programming is race condition. In order to avoid race condition, we need to ensure that only one thread can access a certain block of code at a time. If a thread wants to enter the critical section of code, it must first acquire a lock. The thread executes the critical section only when it get the lock and it blocks until it acquires the lock. This approach is called serialization.

Serialization is a problem if the critical section needs to be performed only once during the instantiation of the object. In this case, even though locking is not needed, threads wait to acquire the lock, do no processing and release the lock. This results in a large performance overhead even though the locking was not needed in the first place. Double-Checked Locking Optimization was designed to overcome this problem.

To implement Double-Checked Locking, we introduce a flag that serves as a *hint* as to whether the critical section needs to be executed. This flag is checked before acquiring the locks, so if the critical section need not be executed, then the lock is not acquired, thus reducing the unnecessary overhead. The pseudocode for Double-Checked Locking can be given as below<sup>[9]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>:

```
// Perform first-check to evaluate 'hint'. 
if
(
first_time_in_flag is FALSE)
{
acquire the mutex
// Perform double-check to avoid race condition. 
if
(
first_time_in_flag is FALSE)
{
execute the critical section
set first_time_in_flag to TRUE
}
release the mutex
}
```

There are three steps to implement Double-Checked Locking<sup>[9]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>:

+ Identify the critical section. This critical section needs to be executed only once.
+ Implement the Locking logic. This ensures that only one thread executes the critical section at a time.
+ Implement the first-time-in flag. This is to  ascertain whether the critical section has already been executed or whether this is the *first time in*.

The benefits of Double-Checked Locking include reducing the locking overhead for critical sections that need not be executed repeatedly and preventing race conditions as we are using locks when the critical section does need to be executed<sup>[9]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>:.

On the other hand, the liabilities of Double-Checked Locking are<sup>[9]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>:

+ ######Non-atomic pointer or integral assignment semantics:
The read and write to the flag must be an atomic operation. Also, if a pointer is used as the flag, then a non-atomic read and write may result in an illegal memory access.

+ ######Multi-Processor cache coherency:
Some multi-processor systems optimize cache operations by performing reads and writes out of order. Because of this, implementing Double-Checked Locking is difficult on these systems.

+ ######Additional mutex usage
Even though the locks are not acquired every time a critical section is executed by a thread, a lock is still created by the program which just stays unused in memory throughout the execution of the program.


[Prev Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/disrupt.md) | [Next Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/suspension.md)
 
 [Back to contents](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Index.md)
