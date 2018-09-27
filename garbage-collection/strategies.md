# Reference Counting
* When an object X references an object Y, the system increments a counter on Y.
* When X drops its reference to Y, the system decrements the counter.
* When counter reaches zero, Y is no longer live and hence eligible for garbage collection.
	* This will also decrement the counter of objects to which Y refers.
* This strategy fails in face of cycles.
	* X holds a reference to Y.
	* Y holds a reference to X.
	* Neither X nor Y will be garbage collected.
	* Nor any object which refer to X and Y.
# Mark And Sweep
* Name refers to the way two phases of garbage collection are implemented.
* First determine a set of roots that contains the directly reachable objects.
	* Local variables on the stack.
* Once a set of roots is determined, mark the objects referenced by those roots as reachable.
	* Examine references in those objects and mark them as reachable.
	* This process continues until no more reachable objects remain unmarked.
* Reclaim the unmarked i.e. dead objects.
* Requires freezing of program execution as interconnection of objects may change during the marking phase.
# References
* The Java Programming Language
