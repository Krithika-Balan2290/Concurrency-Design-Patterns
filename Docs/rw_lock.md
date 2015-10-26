#Read Write Locks

A readers–writer (RW) or shared-exclusive lock (also known as a multiple readers/single-writer lock[1] or multi-reader lock) is asynchronization primitive that solves one of the readers–writers problems. An RW lock allows concurrent access for read-only operations, while write operations require exclusive access. This means that multiple threads can read the data in parallel but an exclusive lock is needed for writing or modifying data. When a writer is writing the data, all other writers or readers will be blocked until the writer is finished writing. A common use might be to control access to a data structure in memory that cannot be updated atomically and is invalid (and should not be read by another thread) until the update is complete.
Readers–writer locks are usually constructed on top of mutexes and condition variables, or on top of semaphores.


##Read Write Priority Policies:
RW locks can be designed with different priority policies for reader vs. writer access. The lock can either be designed to always give priority to readers (read-preferring), to always give priority to writers (write-preferring) or be unspecified with regards to priority. These policies lead to different tradeoffs with regards to concurrency and starvation.
######Read-preferring
RW locks allow for maximum concurrency, but can lead to write-starvation if contention is high. This is because writer threads will not be able to acquire the lock as long as at least one reading thread holds it. Since multiple reader threads may hold the lock at once, this means that a writer thread may continue waiting for the lock while new reader threads are able to acquire the lock, even to the point where the writer may still be waiting after all of the readers which were holding the lock when it first attempted to acquire it have released the lock.
######	Write-preferring 
RW locks avoid the problem of writer starvation by preventing any new readers from acquiring the lock if there is a writer queued and waiting for the lock. The writer will then acquire the lock as soon as all readers which were already holding the lock have completed.[3] The downside is that write-preferring locks allows for less concurrency in the presence of writer threads, compared to read-preferring RW locks. Also the lock is less performant because each operation, taking or releasing the lock for either read or write, is more complex, internally requiring taking and releasing two mutexes instead of one. This variation is sometimes also known as "write-biased" readers–writer lock. 
######	Unspecified priority 
RW locks does not provide any guarantees with regards read vs. write access. Unspecified priority can in some situations be preferable if it allows for a more efficient implementation. [10]



<Text Here>

[Prev Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/reactor.md) | [Next Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/thread_pools.md)
 
 [Back to contents](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Index.md)
