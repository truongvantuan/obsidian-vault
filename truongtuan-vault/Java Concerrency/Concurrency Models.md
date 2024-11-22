1. **Shared State**
![[Pasted image 20241109103740.png]]
Threads are designed to share the state with other thread. By state is meant some data, typically object or more objects.
When threads share state, problem like race condition, dead lock, etc. may occur.
2. **Separate state**
![[Pasted image 20241109103754.png]]
Separate state mean different threads in application do not share any state among them.
When no two threads write to same object, we can avoid most of the common concurrency problems.
3. **Parallel work**
![[Pasted image 20241109103812.png]]

Parallel worker concurrency distributes the incoming jobs to different workers. Each worker completes the full job. The workers work in parallel, run in different threads.

	- Advantages: To increase the parallelization level of the application
	- Disadvantages: Shared State Can Get Complex.

4. Assembly line
