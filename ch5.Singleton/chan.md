
### assigning variable as a static variable

downsides 

- it is assigned when a server runs for the first time
- we don't need right now but it is assigned and take resource

###  Singleton

we can prevent calling the construct outside and control the way instantiating the singleton object as writing codes like this 

```java
class Singleton {

	public static Singleton instance;

	private Singleton() {}
	public Singleton getInstance() {
		... //create the instance - lazy loading
	}
	
}

```


### Synchronization Problem

Two threads called the function at the same time
- there is a possibility creating 2 instances 

**solution 1: just use synchronized keyword**
- if this isn't causing substantial overhead for your application, **just use it**
- it decrease performance by a factor of 100

```java
public static synchronized Singleton getInstance() {}
```


**solution 2: just eagerly create the instance** 

```java
public static Singleton instance; = new Singleton()
```

- if creation and runtime aspect of the Singleton isn't onerous, create singleton eagerly

solution 3: Double-checked locking
- volatile
	- write data in main memory directly passing the CPU cache
- synchronized block in if block

```java
private volatile static Singleton instance;

...


if (instance == null) {
	synchronized (Singleton.class) {
		if (instance == null) {
			instance = new Singleton()
		}
	}
}


```
