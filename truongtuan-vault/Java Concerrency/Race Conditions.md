# Two types of Race Conditions
Race conditions can occur when two or more threads read and write the same variable.
## Read-Modify-Write
`both read then both update then both wtire variable at the same time`
The read-modify-write pattern means that two or more threads first read a given variable, then modify its value and write it back to the variable.
## Check-Then-Act
`both check then both do somethings at the same time`
The check-then-act pattern means that two or more threads check a given variable, for instance if a Map contains a given value, and then go on to act based on that information, e.g. taking the value from the map.
The problem map occur if two threads check the Map for a given value at the same time - see that value present, and then both threads try to take (remove) that the same time. However only one thread can actually take the value.

## Preventing Race Conditions
1. **Critical Sections** the code blocks lead to the race conditions.
2. The to **prevent race conditions from occurring** must make sure that the **critical section is executed as an atomic instruction**. That mean that only once thread is executing this critical section.
3. Implement: 
	1. Using **synchronized block java code**
	2. Using **Lock** or **Atomic variables**, e.g. AtomicInteger
	3. Using **Synchronized block** for small critical section. For larger Critical Section can break into smaller critical section
```
	synchronized(this) {
	// critical section here
	}
```
4. Separate thread for Single Responsibility
	1. One Runnable for read, one for modify.
	2. Two threads access same objects but not write to the same objects.