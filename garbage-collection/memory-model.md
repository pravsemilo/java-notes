# Parts of JVM Heap
* `Young Generation`
	* `Eden Memory`
	* `Survivior Memory`
* `Old Generation`
* `Permanent Generation`
	* `Method Area`
	* `Memory Pool`
	* `Runtime Constant Pool`
	* `Java Stack Memory`
# Young Generation
* Divided into three parts - `Eden Memory` and two `Survivor Memory`.
## Eden Memory
* Newly created objects are located here.
## Survior Memory
* At any point of time one of the survivor spaces are empty.
## Minor GC
* Garbage collection which happens when young generation gets filled.
* When `Eden Space` gets filled, Minor GC is performed and suriving objects are moved to one of the `Survivor Spaces`.
* Minor GC also checks survivor objects if any and moves them to another survivor space.
* At any point of time one of the survivor spaces are empty.
* Objects that survive many cycles of minor GC are moved to `Old Generation` space.
	* This is done by setting a threshold for the age of young generation.
* Takes less time compared to `Major GC`.
# Old Generation
* Contains long lived objects that have survived many rounds of `Minor GC`.
* Also called `Tenured Space`.
## Major GC
* Performed when `Old Generation` is full.
* Takes longer time.
# Permanent Generation
* Also called `Perm Gen`.
* Not part of heap.
* Contains application metadata required by JVM.
* `Perm Gen` objects are garbage collected in a `full garbage collection`.
## Method Area
* Stores class structure, constants, static variables and code for methods and constructors.
### Runtime Constant Pool
* Per-class runtime representation of constant pool in a class.
* Runtime constants
* Static Methods 
## Memory Pool
* Pool of immutable objects.
## Java Stack Memory
* Used for execution of a thread.
* Contains method specific values that are short-lived and references to objects in the heap that are getting referred from the method.
# References
* https://www.journaldev.com/2856/java-jvm-memory-model-memory-management-in-java
