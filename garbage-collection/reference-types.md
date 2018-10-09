# Reference Objects
* An object whose sole purpose is to maintain a reference to another object called the `referent`.
* Instead of maintaining a direct reference, you maintain a direct reference to a reference object which wraps the actual object.
* If reference object is the only reference to an object, GC can decide whether to reclaim the object or not.
* If the object is reclaimed, the reference object is cleared.
* The strength of a reference object dictates the GC behavior.
# `Reference` class
* Contained in `java.lang.ref` package.
* Abstract
* Generic
* Superclass of all the specific reference classes.
## Methods
* `public T get()`
* `public void clear()`
* `public boolean enqueue()` - Add this reference object to the reference queue with which it is registered.
* `public boolean isEnqueued()` 
# Reference Types
* `Strong References`
* `SoftReference`
* `WeakReference`
* `PhantomReference`
## Strong References
* An object is strongly reachable if it can be reached through at least one chain of strong references i.e. the normal references.
```java
Employee emp = new Employee();		// Creating a strong reference.
emp = null;				// Signalling the garbage collector that the Employee object has no strong references and hence elgible for garbage collection.
```
## SoftReference
* An object is softly reachable if it is not strongly reachable, but it is reachable through at least one chain containing a soft reference.
* Used to create a soft reference to an existing object that is already referred to by a strong reference.
* Reclaimed at the discretion of garbage collector.
	* Garbage collector will always reclaim memory occupied by soft references before throwing an `OutOfMemoryError`.
```java
Employee emp = new Employee();
SoftReference<Employee> softRef = new SoftReference<Employee>(emp);	// Creating a soft reference to an object referred by a strong reference.
emp = null;								// Signal the garbage collector to reclaim the memory occupied by the Employee object if it wishes to.
Employee resurrectedEmp = softRef.get();				// In case the garbase collector has not ran, we now have a strong reference to the Employee object.
```
## WeakReference
* An object is weakly reachable if it is not softly reachable, but it is reachable through at least one chain containing a weak reference.
* Once an object becomes weakly reachable, it becomes eligible for finalization.
* A weakly reachable object will be reclamied by the garbage collector.
	* If an object has only a weak reference pointing to it, garbage collector will consider it eligible for garbage collection even if there is sufficent memory.
	* If garbage collector determines that an object is weakly reachable, all `WeakReference` objects that refer to that object will be cleared.
	* Object then becomes eligible for finalization and unless the object is phantom reachable, the object will be reclaimed after finalization.
* Used in conjunction with `WeakHashMap`.
	* A special kind of `HashMap` where keys are all weak references.
## PhantomReference
* An object is phantom reachable when it is not weakly reachable, has been finalized (if necessary), but is reachable through at least one chain containing a phantom reference.
* Once an object becomes phantom reachable, it becomes eligible for finalization.
* Can't be accessed directly.
	* When using a `get()` method, it always returns null.
* If an object is phantom reachable, it cannot be reclaimed till the phantom reference is explicitly cleared.
* `PhantomReference` objects allow us to deal with objects whose `finalize()` methods have been invoked.
* Used in conjunction with `ReferenceQueue`.
# Reference Queues
* When an object changes reachability state, references to that object may be placed on a reference queue.
* Reference objects can be associated with a queue when they are constructed.
* Used by garbage collector to communicate with application code about reachability changes.
* Both weak and soft references are enqueued at some point after the garbage collector determines that their referent has entered a particular reachabliity state.
	* In both cases, they are cleared before being enqueued.
* Phantom references are also enqueued at some point after the garbage collector determines that their referent has become phantom reachable.
	* However they are not cleared.
* Once a reference object has been queued, it is guaranteed that `get()` will return `null` and hence objet cannot be resurrected.
* Registering a reference object with the queue doesn't create a reference between the queue and the reference object.
## Methods
* `public Reference<? extends T> poll()` - Remove and return the next reference object from this queue or `null` if queue is empty.
* `public Reference<? extends T> remove()` - Blocking method to remove and return the next reference object from this queue.
* `public Reference<? extends T> remove(long timeout)` - Blocking method to remove and return the next reference object from this queue till either an object is available or timeout period elapses. If timeout expires, null is returned.
## Reference Queues And Phantom References
* A phantom reference never lets you reach the object, even if it is otherwise reachable.
* Reference queues are used with phantom references to determine when an object is to be reclaimed.
* Phantom references are enqueued only after it is finalized and hence the last chance to do something.
# References
* The Java Programming Language - Ken Arnold, James Gosling, David Holmes
