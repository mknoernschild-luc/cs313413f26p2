COMP 313/413 Project 2 Report

TestList.java and TestIterator.java

	TODO also try with a LinkedList - does it make any difference?

    There is no observable difference between using List or LinkedList. The differences between
    the two classes are performance and internal structure, which the available tests can't observe.

TestList.java
	testRemoveObject()
		list.remove(5); // what does this method do?
			list.remove(5) removed the value at index 5, which is the second instance of 77.
			So, the list becomes: [3, 77, 4, 77, 5, 6].

		list.remove(Integer.valueOf(5)); // what does this one do?
			list.remove(Integer.valueOf(5)) removes the first element that equals 5 by calling remove(Object o).
			So, the list then becomes: [3, 77, 4, 77, 6].

TestIterator.java
	testRemove()
		i.remove(); // what happens if you use list.remove(77)?
			If you use list.remove(Integer.valueOf(77)) instead of i.remove(), the first 77 is removed from the
			list directly, ignoring the location of the iterator. The iterator then detects that the list was
			modified, and the next time i.next() is called, an exception (ConcurrentModificationException) is thrown.

TestPerformance.java

	State how many times the tests were executed for each SIZE (10, 100, 1000 and 10000)
	to get the running time in milliseconds and how the test running times were recorded.

	SIZE 10, REPS 1000000
								  #1   #2   #3   #4   #5   #6
        testArrayListAddRemove:  13ms 13ms 13ms 14ms 13ms 14ms
        testLinkedListAddRemove: 11ms 11ms 12ms 12ms 11ms 12ms
		testArrayListAccess:     11ms 11ms 12ms 17ms 13ms 14ms
        testLinkedListAccess:    5ms  6ms  6ms  6ms  5ms  6ms

	SIZE 100, REPS 1000000
								  #1   #2   #3   #4   #5   #6
        testArrayListAddRemove:  22ms 22ms 22ms 22ms 23ms 22ms
        testLinkedListAddRemove: 11ms 13ms 13ms 12ms 13ms 12ms
		testArrayListAccess:     12ms 16ms 14ms 15ms 18ms 15ms
        testLinkedListAccess:    14ms 15ms 14ms 12ms 15ms 15ms

	SIZE 1000, REPS 100000
								  #1   #2   #3   #4   #5   #6
        testArrayListAddRemove:  13ms 13ms 13ms 12ms 13ms 14ms
        testLinkedListAddRemove: 4ms  4ms  5ms  4ms  5ms  5ms
		testArrayListAccess:     11ms 11ms 10ms 11ms 11ms 10ms
        testLinkedListAccess:    33ms 34ms 34ms 35ms 35ms 34ms

	SIZE 10000, REPS 10000
								  #1   #2   #3   #4   #5   #6
        testArrayListAddRemove:  12ms 12ms 12ms 12ms 12ms 12ms
        testLinkedListAddRemove: 2ms  2ms  2ms  2ms  2ms  2ms
		testArrayListAccess:     7ms  9ms  9ms  10ms 9ms  8ms
        testLinkedListAccess:    45ms 47ms 45ms 45ms 46ms 45ms

	listAccess - which type of List is better to use, and why?

		 ArrayList is better to use when it comes to access because, other than at size=10, it is faster at every size. Additionally,
		 as the size increases the advantage of ArrayList compared to LinkedList only improves. For example, at size 10000,
		 ArrayList access takes ~8.66 ms on average compared to LinkedList access, which takes 45.5 ms on average.

	listAddRemove - which type of List is better to use, and why?

		 LinkedList is better to use when it comes to Add/remove because it is faster at larger sizes. While at size=10, LinkedList add/remove
		 does not have much of an advantage over ArrayList add/remove; by the time size=10000, LinkedList add/remove has an advantage over ArrayList
		 add/remove with LinkedList add/remove takes only 2 ms on average, compared to ArrayList add/remove taking 12 ms on average.
