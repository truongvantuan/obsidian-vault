# The internal Java Memory Model

1. Thread diagram
![[Pasted image 20241118113520.png]]
- **Each thread** running in the Java virtual machines has its **own thread stack**.
- Thread stack contains "call stack".
- Thread stack contains all **local variable** for **each method** being executed. 
- Local variables created by a thread are invisible to all other thread. Each thread has its own version of each local variable.
- Heap memory contains all objects created in application.

2. Local variable diagram
![[Pasted image 20241118114402.png]]
- Local variables: primary data (int, short, double, long, char, etc...), and **reference to objects**.
- 