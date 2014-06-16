

## ISemaphore

Hazelcast ISemaphore is the distributed implementation of  `java.util.concurrent.Semaphore`. As you may know, semaphores offer *permit*s to control the thread counts in the case of performing concurrent activities. To execute a concurrent activity, a thread grants a permit or waits until a permit becomes available. When the execution is completed, permit is released.

<font color="red">***Note:***</font> *Semaphore with a single permit may be considered as a lock. But, unlike the locks, when semaphores are used any thread can release the permit and also semaphores can have multiple permits.*

When a permit is acquired on ISemaphore:

-	if there are permits, number of permits in the semaphore is decreased by one and calling thread performs its activity. If there is contention, the longest waiting thread will acquire the permit before all other threads.
-	if no permits are available, calling thread blocks until a permit comes available. And when a timeout happens during this block, thread is interrupted. In the case where the semaphore


```java
```

	<initial-permits>3</initial-permits>
```

<font color="red">***Note:***</font> *If there is a shortage of permits while the semaphore is being created, value of this property can be set to a negative number.*

`At iteration: 1, Active Threads: 2 `

`At iteration: 2, Active Threads: 3 `

`At iteration: 3, Active Threads: 3 `

`At iteration: 4, Active Threads: 3 `


Hazelcast also provides backup support for ISemaphore. When a member goes down, another member can take over the semaphore with the permit information (permits are automatically released when a member goes down). To enable this, synchronous or asynchronous backup should be configured with the properties `backup-count` and `async-backup-count`(by default, synchronous backup is already enabled).

A sample configuration is shown below.

```xml
<semaphore name="semaphore">
	<initial-permits>3</initial-permits>
	<backup-count>1</backup-count>
</semaphore>
```
