# Reference Types
* `Strong References`
* `Soft References`
* `Weak References`
* `Phantom References`
## Strong References
* Any object with a strong reference to it, will never be garbage collected.
```java
Employee emp = new Employee();		// Creating a strong reference.
emp = null;				// Singalling the garbage collector that the Employee object has no strong references and hence elgible for garbage collection.
```
## Soft References
* Used to create a soft reference to an existing object that is already referred to by a strong reference.
* Garbage collector will always reclaim memory occupied by soft references before throwing an `OutOfMemoryError`.
* Useful to create object pools where the size of the pool is dynamic.
```java
Employee emp = new Employee();
SoftReference<Employee> softRef = new SoftReference<Employee>(emp);	// Creating a soft reference to an object referred by a strong reference.
emp = null;								// Signal the garbage collector to reclaim the memory occupied by the Employee object if it wishes to.
Employee resurrectedEmp = softRef.get();				// In case the garbase collector has not ran, we now have a strong reference to the Employee object.
```
## Weak References
* If an object has only a weak reference pointing to it, garbage collector will consider it eligible for garbage collection even if there is sufficent memory.
* Used in conjunction with `WeakHashMap`.
	* A special kind of `HashMap` where keys are all weak references.
## Phantom References
* Can't be accessed directly.
* When using a `get()` method, it always returns null.
# References
* https://dzone.com/articles/reference-types-java-part-1
* https://dzone.com/articles/weak-soft-and-phantom-references-in-java-and-why-they-matter
* https://plumbr.io/handbook/gc-tuning-in-practice/weak-soft-and-phantom-references
