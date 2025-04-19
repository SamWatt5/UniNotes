## Concurrency
Concurrency is a fundamental concept in operating systems that refers to the ability of a system to execute multiple processes or threads simultaneously or in overlapping time periods. It's essential for improving the efficiency and responsiveness of modern systems, allowing multiple tasks to be performed seemingly at once, even if they are not actually being executed at the same exact time.  
In a single-core processor, true parallelism (executing multiple tasks at the exact same time) is impossible, instead the OS uses techniques like context switching to rapidly switch tasks, to make it seem like all the processes are running at once. This allows the system to run multiple processes without having to wait for each other to finish.

Concurrency is even more powerful in multi-core processors, because actual parallelism can happen. This means one core can manage background tasks, and another can handle user interactions.

## Challenges raised by Concurrency
A common issue is managing shared resources between multiple threads or processes. If two threads try to modify the same piece of data at the same time, it can lead to a inconsistencies, a problem known as a race condition. To prevent this, synchronization mechanisms like locks, semaphores and monitors are used. E.g. in a bank system, two transactions attempting to update the same account balance at the same time could lead to errors if not properly synchronized.

One common issue is a race condition, where the outcome of a program depends on the unpredictable timing of multiple threads accessing shared data.

## Mutual Exclusion
Mutual Exclusion is a fundamental concept in concurrent programming that ensures only one thread or process can access a shared resource at any given time. It stops multiple threads from performing confliction operations on shared data simultaneously, which can lead to race conditions. When mutual exclusion is enforced, if one thread is accessing a shared resource, other threads are temporarily blocked from