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
# References
* The Java Programming Language - Ken Arnold, James Gosling, David Holmes
