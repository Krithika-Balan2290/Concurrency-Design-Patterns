#Barriers

In parallel computing, multiple threads execute at the same time in order to speed up processing. But sometimes, the threads might have to wait for some processing to complete before continuing the execution. Also, threads might execute in stages. All threads execute the first stage, then start the second stage together and so on until all threads finish processing. This kind of execution can be implemented using barriers.

Barriers are a means to achieve synchronization in which a group of threads stop execution at the barrier and wait for the other threads to catch up. Once all threads reach the barrier, the execution proceeds until the next barrier. This kind of pattern where all threads wait for the other threads to reach the barrier before continuing execution is called a *global barrier*. A *local barrier* is a pattern in which the parent thread waits for the child threads to complete execution before proceeding with its execution. Problems like divide and conquer algorithms are better implemented using local barriers whereas other algorithms are better implemented using global barriers<sup>[5]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.

![Barriers]( http://www.albahari.com/threading/Barrier.png)

One problem with barrier synchronization is that all threads must wait for the slowest threads to complete its execution. This causes a lot of decrease in the performance of the program. When our goal to optimize performance, using too many barriers would greatly hinder that goal. If barriers are really needed, then programmers can opt for split barriers. These barriers allow the faster threads to continue with other tasks while they are waiting for the slow threads to arrive. This would help increase the performance of a program while using barriers. Many parallel programing environments include implicit barriers at the end of code blocks. Programmers must be aware of these features of the environment when using barriers.

Barrier abstraction is provided as a feature in most parallel programming environments. POSIX threads provides a *Barrier* object along with the barrier functions which can be used for barrier synchronization. The functions provided with the barrier object can create the barrier, associate a certain number of threads with it and wait till the threads reach the barrier in order to continue execution<sup>[6]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.

The `pthread_barrier_init()` function is used to create barriers<sup>[6]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.

```
int pthread_barrier_init(pthread_barrier_t  *barrier, 
          const pthread_barrierattr_t *restrict attr, 
          unsigned count);
#include <pthread.h> 
pthread_barrier_t barrier; 
pthread_barrierattr_t attr;
unsigned count;
int ret; 
ret = pthread_barrier_init(&barrier, &attr, count);
```

This function allocated the required resources to the input barrier. The attributes of the barrier can be specified in the optional *attr* argument and *count* specifies the number of threads associated with the barrier<sup>[6]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.


The function `pthread_barrier_wait()` is used to synchronize the threads at a barrier<sup>[6]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.

```
int pthread_barrier_wait(pthread_barrier_t  *barrier);
#include <pthread.h> 
pthread_barrier_t barrier; 
int ret; 
ret = pthread_barrier_wait(&barrier);

```

When the barrier is created, it is associated with the number of threads specified in the *count* variable. When the `pthread_barrier_wait()` is called, the calling thread blocks until the number of threads associated with the barrier have all called the `pthread_barrier_wait()` function. When all the associated threads have called the `pthread_barrier_wait()` function, a constant `PTHREAD_BARRIER_SERIAL_THREAD` is returned to one unspecified thread and 0 is returned to all the other threads. The barrier is then reset to its initial state and the execution continues<sup>[6]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.


[Prev Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/balking.md) | [Next Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/disrupt.md)
 
 [Back to contents](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Index.md)
