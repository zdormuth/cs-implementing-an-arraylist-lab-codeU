# cs-implementing-an-arraylist-lab


## Objectives

1.  Write an implementation of an ArrayList.


## Implementing an Array-backed List

For this lesson we provide a partial implementation of an ArrayList that uses a Java array to store the elements.  We left four of the methods incomplete; your job is to fill them in.  We provide JUnit tests you can use to check your work.


## Instructions

When you check out the repository for this lab, you should find a file structure similar to what you saw in the previous lab.  The top level directory contains `CONTRIBUTING.md`, `LICENSE.md`, `README.md`, and the directory that contains the code for this lab, `javacs-lab02`.

In the subdirectory `javacs-lab02/src/com/flatironschool/javacs` you'll find the source files you need for this lab:

    *  `MyArrayList.java` contains a partial implementation of the `List` interface using a Java array to store the elements.

    *  `MyArrayListTest.java` contains JUnit tests for `MyArrayList`.

In `javacs-lab02`, you'll find the Ant build file `build.xml`.  If you are in this directory, you should be able to run `ant MyArrayList` to run `MyArrayList.java`, which contains a few simple tests.  Or you can run `ant MyArrayListTest` to run the JUnit test.
    
When you run the tests, several of them should fail.  If you examine the source code, you'll find four `TODO` comments indicating which methods you will fill in.

## `MyArrayList` code

Before you start filling in the missing methods, let's walk through some of the code.  Here are the instance variables and the constructor. 

```java
public class MyArrayList<E> implements List<E> {
	int size;                    // keeps track of the number of elements
	private E[] array;           // stores the elements
	
	public MyArrayList() {
		array = (E[]) new Object[10];
		size = 0;
	}
}
```

As the comments indicate, `size` keeps track of how many elements are in `MyArrayList`, and `array` is the array that actually contains the elements.  

The constructor creates an array of 10 elements, which are initially `null`, and sets `size` to 0.  Most of the time, the length of the array is bigger than `size`, so there are unused slots in the array.
    
One detail about Java:  You can't instantiate an array of T[], so you have to instantiate an array of Object and then typecast it.  You can [read more about this issue here](http://www.ibm.com/developerworks/java/library/j-jtp01255/index.html).

Next we'll look at the method that adds elements to the list.  Here's our implementation of `add`:

```java
	public boolean add(E element) {
		if (size >= array.length) {
			// make a bigger array and copy over the elements
			E[] bigger = (E[]) new Object[array.length * 2];
			System.arraycopy(array, 0, bigger, 0, array.length);
			array = bigger;
		} 
		array[size] = element;
		size++;
		return true;
	}
```

If there are no unused spaces in the array, we have to create a bigger array and copy over the elements.  Then we can store the element in the array and increment `size`.
    
It might not be obvious why this method returns a boolean, since it seems like it always returns `true`.  As always, [you can find the answer in the documentation](https://docs.oracle.com/javase/7/docs/api/java/util/Collection.html#add(E)).

It's also not obvious how to analyze the performance of this method.  In the normal case, it's constant time, but if we have to resize the array, it's linear.  In the next README we'll explain how we can handle this.

We'll look at `get` next, and then you can fill in `set`.  Actually, `get` is pretty simple:

```java
	public T get(int index) {
		if (index < 0 || index >= size) {
			throw new IndexOutOfBoundsException();
		}
		return array[index];
	}
```

If the index is out of bounds, it throws an exception; otherwise it reads and returns an element of the array.  Notice that it checks whether the index is less than `size`, not `array.length`, so it's not possible to access the unused elements of the array.

## Instructions

*   In `MyArrayList.java`, you'll find a stub for `set` that looks like this:

```java
	public T set(int index, T element) {
		// TODO: fill in this method.
		return null;
	}
```

Read [the documentation of set](https://docs.oracle.com/javase/7/docs/api/java/util/List.html#set(int,%20E)), then fill in the body of this method.  If you run `MyArrayListTest` again, `testSet` should pass.

HINT: Try to avoid repeating the index-checking code.


*   Your next mission is to fill in `indexOf`.  As usual, you should [read the documentation](https://docs.oracle.com/javase/7/docs/api/java/util/List.html#indexOf(java.lang.Object)) so you know what it's supposed to do.  In particular, notice how it is supposed to handle `null`.

    To make things a little easier, we've provided a helper method called `equals` that compares an element from the array to a target value and returns `true` if they are equal (and it handles `null` correctly).
Notice that this method is private because it is used inside this class but it is not part of the `List` interface.

When you are done, run `MyArrayListTest` again; `testIndexOf` should pass now, as well as the other tests that depend on it.

*   Only two more methods to go, and you'll be done with this lab.  The next one is an overloaded version of `add` that takes an index and stores the new value at the given index, shifting the other elements to make room, if necessary.

Again, [read the documentation](https://docs.oracle.com/javase/7/docs/api/java/util/List.html#add(int,%20E)), write an implementation, and run the tests for confirmation.

HINT: Avoid repeating the code that makes the array bigger.


*  Last one: fill in the body of `remove`.  [The documentation is here](https://docs.oracle.com/javase/7/docs/api/java/util/List.html#remove(int)).  When you finish this one, all tests should pass.


Once you have your implementation working, compare it to mine, which you can find by checking out the solutions branch of the repo, or [you can read it on GitHub](https://github.com/learn-co-students/cs-implementing-an-arraylist-lab-codeU/tree/solution).




<p data-visibility='hidden'>View <a href='https://learn.co/lessons/cs-implementing-an-arraylist-lab'>Implementing an Array List</a> on Learn.co and start learning to code for free.</p>
