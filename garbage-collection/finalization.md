# `finalize()`
* You can implement a `finalize()` method that is executed before an object's space is reclaimed.
* Invoked by GC after it determines that this object is no longer reachable.
* Inovked at most once per object.
* Execution of this method may make the object reachable. This is called as `resurrection`.
	* Since `finalize()` is invoked only once per object, resurrection also happens only once.
* There are no guarantees on when and if at all it will be called.
* Exception thrown if any is ignored by GC.
* If your object has become garbage, it is possible that objects referring to your objects may also be garbage. 
	* As garbage, they may have been finalized before your object and hence be in an unexpected state.
* When an application exits, no further garbage collection is performed.
	* So `finalize()` will not be called for objects that have not yet been collected.
* Garbage collector may reclaim objects in any order or it may never reclaim them.
# Best Practices
* Provide an explicit cleanup method like `close()`, `destroy()` etc.
```java
import java.io.*;

public class FileProcessor {
	private FileReader reader;
	
	public FileProcessor(String path) throws FileNotFoundException {
		reader = new FileReader(path);
	}

	public synchronized void close() throws IOException {
		if(reader != null) {
			reader.close();
		}
		reader = null;
	}

	protected void finalize() throws Throwable {
		close();
	}
}
```
* Always invoke `super.finalize()` preferrably in a `finally` block.
```java
import java.io.*;

public class FileProcessor {
	private FileReader reader;
	
	public FileProcessor(String path) throws FileNotFoundException {
		reader = new FileReader(path);
	}

	public synchronized void close() throws IOException {
		if(reader != null) {
			reader.close();
		}
		reader = null;
	}

	protected void finalize() throws Throwable {
		try {
			close();
		} finally {
			super.finalize();
		}
	}
}
```
# References
* The Java Programming Language - Ken Arnold, James Gosling, David Holmes
