## This is sample Java class with Gitbug markdown file

##### Writing the Controller Code to queue up a job on IronWorker to be done asynchronously

```java
package collections.queue;

import java.util.LinkedList;
import java.util.List;

public class BlockingQueue {
	
	private List<Object> queue = new LinkedList<Object>();
	private int limit = 10;
	
	public BlockingQueue(int limit) {
		this.limit = limit;
	}
	
	public synchronized void enqueue(Object item) throws InterruptedException {
		if (queue.size() == limit) {
			wait();
		}
		if (queue.size() == 0){
			notifyAll();
		}
		queue.add(item);
	}
	
	public synchronized Object dequeue() throws InterruptedException {
		if (queue.size() == 0) {
			wait();
		}
		if (queue.size() == limit) {
			notifyAll();
		}
		return queue.remove(0);
	}
}
```

##### Writing the worker script to make the API request and save back to the database


```ruby
setup_database

uri = URI.parse("http://pygments.appspot.com/")
request = Net::HTTP.post_form(uri, lang: params["request"]["lang"], code: params["request"]["code"])

snippet = Snippet.where(:id => params["snippet_id"]).first
snippet.update_attribute(:highlighted_code, request.body)
```
