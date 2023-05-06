Download Link: https://assignmentchef.com/product/solved-eecs2031-lab7-dynamic-memory-allocation
<br>
<strong>   </strong> Part I Dynamic memory allocation 1 Problem A

<strong>Subject:  </strong>

Dynamically allocate array space, using malloc or calloc.




<strong>Specification </strong>

Write a (short) ANSI program that prompts the user for the size of an int array, and then creates the array dynamically.




<strong>Implementation </strong>

Download program lab7A.c. This program tries to create array based on user entered size at run time. Observe how the array element is set using pointer notation.

Compile using<strong>  </strong><strong>gcc -ansi -pedantic-errors lab7A.c. </strong>Observe the error message <strong><em>ISO C90 forbids variable length array ‘my_array’.</em></strong>  No a.out was generated.

As mentioned in class, ANSI (C90) standard does not support variable-length array. That is, the array size should be a constant in the code so that the necessary memory space is allocated at compile time. To generate “dynamic” array at run time, in ANSI C we need to use malloc or calloc to allocate memory dynamically.

<ul>

 <li>Fix the program by allocating the array space dynamically, using malloc or calloc. Allocate needed space only.</li>

 <li>Implement function void printArray(int * arr, int n) which prints the first n elements of the array argument, which is decayed into int *. Using pointer notations in the function.</li>

</ul>




<strong>Sample Inputs/Outputs: </strong>

red 388 % <strong>gcc -ansi -pedantic-errors lab7A.c    </strong>

red 389 % <strong>a.out </strong>

Size of array: <strong>1</strong> [0]: -10 red 390 % <strong>a.out</strong>

Size of array: <strong>3</strong>

[0]: -10

[1]: 100

[2]: 200 red 391 % <strong>a.out</strong>

Size of array: <strong>1000000000000000</strong> Segmentation fault (core dumped) red 392 %




Memory allocation by malloc or calloc may fail, in that case the program crashes. So if your program generates Segmentation fault for some input size, as shown above, that means you did not check the result of memory allocation. Fix the program by checking the result of memory allocation and if the allocation was not successful (how to detect this?), then display an error message “Memory allocation failed. Bye!” and exit the program (kind of like catching an exception in Java).

<strong> </strong>

<strong>Sample Inputs/Outputs: </strong>

red 388 % <strong>gcc -ansi -pedantic-errors lab7A.c    </strong>




red 389 % <strong>a.out </strong>Size of array: <strong>1</strong> [0]: -10 red 390 % <strong>a.out</strong> Size of array: <strong>3</strong>

[0]: -10

[1]: 100 [2]: 200 red 391 % <strong>a.out</strong> No more error message “<strong><em>ISO C90 forbids variable length array …</em></strong>”




Program terminates “peacefully”.

Size of array: <strong>1000000000000000</strong>

Memory allocation failed. Bye!              No “segmentation fault”.

red 392 %




Now uncomment the last block, and run the program again. Observe that the pointer returned from malloc, which is casted into char*, can be passed to strcpy(p, “hello”) and printf(“%s”, p). So for storing strings into the allocated memory space, you can either store character directly, using *(p+i) = ‘X’,  or, pass the address to function strcpy and the like.




<strong>Sample Inputs/Outputs: </strong>

red 388 % <strong>gcc -ansi -pedantic-errors lab7A.c    </strong> red 389 % <strong>a.out </strong>

Size of array: <strong>1</strong>

[0]: -10  hello heXlo red 390 % <strong>a.out</strong>

Size of array: <strong>3</strong>

[0]: -10

[1]: 100

[2]: 200  hello heXlo red 391 % <strong>a.out </strong>

Size of array: <strong>8</strong>

[0]: 1

[1]: 100

[2]: 200

[3]: 300

[4]: 400

[5]: 500

[6]: 600

[7]: 700  hello heXlo red 392 % <strong>a.out</strong>

Size of array: <strong>12</strong>

[0]: 1

[1]: 100

[2]: 200

[3]: 300

[4]: 400

[5]: 500

[6]: 600

[7]: 700

[8]: 800

[9]: 900

[10]: 1000

[11]: 1100  hello heXlo red 393 % <strong>a.out </strong>

Size of array: <strong>1000000000000000 </strong>Program terminates “peacefully”.  Memory allocation failed!    No “segmentation fault”.

red 394 %

<strong> </strong>

Name the program lab7A.c and submit using     <strong>submit 2031 lab7 lab7A.c </strong>

<strong> </strong>

<h1>2. Problem B  <sub> </sub></h1>

<strong>Subject  </strong>

Array of pointers. Dynamic memory allocation.  Heap.

In addition to allocating memory dynamically, another important feature of memory allocation functions malloc/calloc/realloc is that they are the ways in C to request a memory space in <strong>Heap</strong>, rather than in <strong>Stack</strong>. Local variables declared in a function are stored in stack, where their memory storage are deallocated when the defining function exits (that’s why a local variable‘s lifetime ends automatically when its defining function returns). Heap memory space, on the other hand, provides persistent storage where the allocated memory remains allocated until the programmer explicitly requests that the space be deallocated (using free()). Nothing happens automatically.




<strong>Implementations </strong>

You have played with program setArr.c in lab6. Now let’s do it again more formally.

<ol>

 <li>Download, read, compile and run c. This simple program declares an array of int pointers and set the pointer in main. Note that variables a,b,c,d and e are local variables in main so they are stored in stack, but they will be deallocated only when main returns. Hence as long as the program is running, these local variables are alive so the program runs well.</li>

</ol>

Observe how the values of the int pointees are accessed in printf at  “pointee level”, using *arr[i], which can also be written as **(arr+i).




Setting all the pointers in main is not that practical. The other provided programs setArr1.c and setArr2.c try to set the array of integer pointers through a void function  setArr(int index, int v). The function tries to set the pointers at index index to point to an integer of value v. Then in main, the programs tries to print out the pointees of the first 5 pointer elements, which should be 0,100,200,300,400.

<ol>

 <li>Download, compile and run c, and observe what happens. <strong>Write at the end of the program your explanation of the outputs. </strong></li>

</ol>




<ol start="2">

 <li>Download, compile and run c, and observe what happens. Run again and you probably see different results.</li>

</ol>

Is this version better than the previous version? A little bit, at least it did not crash.  <strong>Write at the end of the program your explanation of the outputs. </strong>




<ol start="3">

 <li>Both the two programs compile successfully but either does not work or does not work correctly. Fix the program by modifying the function setArr(). The program should produce the expected output as show below. You should not use global or static variables.</li>

</ol>

Name the new program setArr3.c.

red 316 % <strong>a.out</strong> arr[0] -*-&gt; 0 arr[1] -*-&gt; 100 arr[2] -*-&gt; 200 arr[3] -*-&gt; 300 arr[4] -*-&gt; 400

red 317%




Submit your programs using <strong>submit 2031 lab7 setArr1.c setArr2.c setArr3.c         </strong>or<strong> submit 2031 lab7 setArr?.c   </strong>

<strong>       </strong>or   <strong>submit 2031 lab7 setArr[1-3].c   </strong>

(The ? and [1-3] are Unix shell filename wildcards, which we will discuss in class.)

<strong> </strong>

<h1>Part II Structures in C 3. Problem C</h1>

<strong>Subject:  </strong>Structure declaration, initialization and assignment. Structure and functions. Array of structures.

<strong> </strong>

<strong>Implementation</strong>

<ol>

 <li>Download file c. Look at the existing code, and then complete the program by following the comments. Observe

  <ul>

   <li>how a structure type is defined</li>

   <li>how a struct variable is declared and initialized at declaration o if a struct variable is declared but not initialized, its members get random/garbage values.</li>

   <li>how a struct variable’s member values are set after declaration, and how the values are retrieved.</li>

   <li>that, when a struct variable is assigned/copied to another struct variable o the values of the members are copied</li>

  </ul></li>

</ol>

o the two structures are independent. Changing members of one struct does not affects the other.

&#x25aa;   However, if the structure has pointer member, then after copy, both pointers point to the same pointee (kind of like ‘’shallow copy” in Java. ) If the pointee is modified, the change can be seen via both structures.

<ul>

 <li>how a struct variable with array as element is declared and initialized at declaration</li>

 <li>how an array of structures is declared, initialized at declaration, and set after declaration</li>

 <li>how a struct can be passed to a function as argument. o function getSum(struct s) work correctly, but o function processStruct(struct s) does not work as expected.</li>

</ul>




<ol start="2">

 <li>Fix the definition of function processStruct() as well as its function call, so that argument structure can be modified correctly.</li>

</ol>

<strong> </strong>

<strong>Sample Inputs/Outputs: </strong>(The hexadecimal memory address would be different from here)

red 326 % <strong>a.out</strong>

———– simple struct ————– a: 32 4 b: 4196576 0 Random/garbage values

a: 100 4 b: 100 4




Enter value for b.int2: <strong>5937</strong> a: 100 4

b: 700 5937

——- struct with pointer member —————– xx: 5 0x7fffa2b65b1c 100 yy: 5 0x7fffa2b65b1c 100

<h2><sup>     </sup>You might get different values c: 10000</h2>

xx: 5 0x7fffa2b65b1c 10000 yy: 5 0x7fffa2b65b1c 10000

——- struct with array member ——————

2 [100 400]

——– struct and function —————– elements sum of a: 104




struct a before processing: 100 4 struct a after  processing: 101 104 ——— array of structs —————- arr[0]: 1 2 arr[1]: 3 4 arr[2]: 5 6

red 327 %

<strong> </strong>

<strong>Submission   </strong>Submit your program using   <strong>submit 2031 lab7 lab7C.c </strong>

<strong>Part III Self-referential structures (Structures + Dynamic memory allocation) </strong>

<strong> </strong>

<h1>4 problem D Array of structures, Linked list</h1>

<strong>Background:  Singly Linked list </strong>

Skip this section if you are familiar with linked list and its basic data structure in C




A linked list consists of a chain of structures (called nodes), with each node containing a pointer (in Java this is called a ‘reference’) to the next node in the chain.







Note that the last node in the list contains a NULL pointer/reference.




To build up a linked list, the first thing we need is a structure that represents a single node in the list. For simplicity, let’s assume that a node contains only one integer data field. So a node struct contains nothing but an integer (the node’s data) plus a reference/pointer to the next node in the list.

Here is how a node class is defined in Java:

Class Node {   int data;   Node next;

};




Here is how a node structure is defined in C:

struct node {   int data;   struct node * next;

};




Note that the next field has type struct node *, which means it can store the address of  another node structure (which is, of course, of the same type of this node).




Now that we have the node structure declared, we need a way to keep track of where the list begins. In other words, we need a pointer variable that always points to the first node in the list, which serves as our only access point to the whole list. Let’s name the variable head:

struct node * head;




Note that when the list is empty, head is NULL.




<strong>Crete and insert a new node into the list </strong>

In general, creating and inserting a new node to the list requires three main steps:

<ol>

 <li>Allocate memory for the node (how?)</li>

 <li>Store data in the node</li>

 <li>Insert the node into the list, which involves finding the proper place for the new node, and setting the next pointer of the new node and its ‘neighbors’ properly.</li>

</ol>

<strong> </strong>

<strong>Remove a node from the list </strong>

Deleting a node also involves three main steps

<ol>

 <li>Locate the node to be deleted</li>

 <li>Alter the next pointer of the previous node so that it ‘bypasses’ the deleted node 3. (Optional) Free the space occupied by the deleted node.</li>

</ol>

<strong> </strong>

<strong>4.0 Linked list implementation in Java. </strong>

Download file MyLinkedList.java, this is a simplified Java implementation of Linked-list data structure. While you might never need to implement a linked list like this in Java (since Java provides a Linked List data structure in its Collections package), reading this simplified code may help you understand how to define Node and LinkedList class, how to traverse and modify the list. You can see that implementing Linked List in Java is relatively straightforward.   Run the program to see the interesting outputs.

<strong> </strong>

<h2>4.1 Problem D0</h2>

<strong>Subject:  </strong>Linked list implementation on stack (in main)

<strong> </strong>

<strong>Implementation:  </strong>

Download file lab7D0.c, look at the code and play with it. Observe that this implementation, which is not very practical, creates nodes and link them directly. It works.

<strong> </strong>

<h2>4.2 Problem D1</h2>

<strong>Subject</strong><strong>  </strong>

Linked list implementation on stack (in function)




<strong>Implementation:  </strong>

Download file lab7D1.c, which moves the repeated implementation of insertion into a function addBegining(). The code of addBegining() imitates the code of method addBegining() in MyLinkedList.java.

Compile and run the program, what did you get?

This is the implementation that had perplexed me for many years, as I could not figure out why the imitated Java code addBegining() in MylinkedList.java works, and the C code lab7D0.c also works,  but not the code in lab7D1.c.

Can you see the problem? Write your answer in the program that you will develop next in problem D2.  Hint: remember setArr2.c which you just did in part I?




<h2>4.3 Problem D2</h2>

<strong>Subject</strong><strong>  </strong>

Linked list implementation on heap.

<strong>Implementation: </strong>

Fix the implementation of addBegining()in lab7D1.c, name the new program lab7D2.c

Also write your answer for problem D1 in your program (as comment).




<strong>Sample output: </strong>

red 330 % <strong>a.out</strong>

5

500 400 300 200 100

red 331 %




<strong>Submission: </strong>Submit using <strong>submit 2031 lab7 lab7D2.c</strong><strong>.</strong>

<strong> </strong>

<h2>4.4 Problem DX</h2>

<strong>Subject:</strong><strong>   </strong>

Stream IO + Structures + Array of structures + Linked list

<strong> </strong>

<strong>Specification </strong>

Based on the prior practice, lets implement a full-fledge Linked list data structure in C.

You are provided with a partially implemented program lab7D3.c, and a data file data.txt.




<strong>Implementation </strong>

Download lab7DX.c, study the existing code there, which does the following:

<ul>

 <li>Opens a data file txt using FILE IO in C. The file contains lines of integers, each line contains exactly two integers. (Stream and FILE IO is a topic that is usually in the syllabus but is skipped this semester.)</li>

 <li>Reads the data file line by line, and store the two integers in each line into Arr is an array of struct integers. The structure integers contains two data members.</li>

</ul>

&#x25aa;   the structure stored in arr[i] gets the two values for its data members from the two integers in the i’th line of the file. For example, the structure in arr[0] gets the two values for its members from the two integers in the first line of the file,  arr[1] gets the two values for its members from the two integers in the second line, and so on.




Based on the existing implementation, implement the following:

<ul>

 <li>Build the linked list (pointed by head) by reading in each structure in the array, adding up the two int fields and then inserting the sum value into the linked list. (line 73-76. This is the only coding you need to do in main())</li>

 <li>Implement or complete the following functions.

  <ul>

   <li>int len (), which returns the length of the list. o int search(int key) which searches the list for node with data key.</li>

   <li>void insert(int d), which inserts at the end of the list a new node with data the list may or may not be empty.</li>

   <li>void insertAfter(int d, int index), which inserts into the list a new node with data d,after the n’th node. (The first node is considered the 0’th node.) Assume that the list is not empty and index is valid in the range [0,len()-1].</li>

   <li>void delete (int d) which removes the node in the list that has data value Assume the node is not empty, and all the nodes in list have distinct data, and <strong>the node with data </strong><strong>d exists in the list</strong>.</li>

  </ul></li>

</ul>




Hint: the slides and the Java program will probably help you.




<strong>Sample Inputs/Outputs: </strong>

If implemented correctly, your program should give the following interesting outputs:

red 314 % <strong>cat data.txt </strong>

3 4

1 2

3 2

6 0

<ul>

 <li>5</li>

 <li>5</li>

</ul>

2 0

<ul>

 <li>0</li>

 <li>0 red 315 % <strong>out</strong> arr[0]: 3 4 arr[1]: 1 2 arr[2]: 3 2 arr[3]: 6 0 Number in () indicates the length of the arr[4]: 3 5 list after current insertion/deletion arr[5]: 4 5</li>

</ul>

<h3>arr[6]: 2 0             (before insertion/deletion)</h3>

arr[7]: 0 0 arr[8]: 1 0




insert 7: (1)   7

insert 3: (2)   7   3 insert 5: (3)   7   3   5 insert 6: (4)   7   3   5   6 insert 8: (5)   7   3   5   6   8 insert 9: (6)   7   3   5   6   8   9

insert 2: (7)   7   3   5   6   8   9   2 insert 0: (8)   7   3   5   6   8   9   2   0 insert 1: (9)   7   3   5   6   8   9   2   0   1 remove 0: (8)   7   3   5   6   8   9   2   1 remove 1: (7)   7   3   5   6   8   9   2 remove 2: (6)   7   3   5   6   8   9 remove 3: (5)   7   5   6   8   9 remove 5: (4)   7   6   8   9 remove 6: (3)   7   8   9 remove 7: (2)   8   9 remove 8: (1)   9 remove 9: (0) insert 7: (1)   7 insert 3: (2)   7   3 insert 5: (3)   7   3   5 insert 6: (4)   7   3   5   6 insert 8: (5)   7   3   5   6   8 insert 9: (6)   7   3   5   6   8   9

insert 2: (7)   7   3   5   6   8   9   2 insert 0: (8)   7   3   5   6   8   9   2   0 insert 1: (9)   7   3   5   6   8   9   2   0   1

insert -4 after index 2: (9)      7   3   5  -4   6   8   9   2   0   1 insert -6 after index 0: (10)     7  -6   3   5  -4   6   8   9   2   0   1 insert -8 after index 6: (11)     7  -6   3   5  -4   6   8  -8   9   2   0   1 search   5 ….  found search  50 ….  not found search   9 ….  found search  19 ….  not found search   0 ….  found search  -4 ….  found

red 316 % <strong> </strong>




Note:  main function does not cover all the cases. You may want to test other cases.




<strong>Submission:</strong>

Submit your program using     <strong>submit 2031 lab7 lab7DX.c</strong><strong>.c </strong>

<strong> </strong>

<strong>In summary, for this lab, you should submit the following files: </strong>

<strong>Part I:  lab7A.c setArr1.c setArr2.c setArr3.c </strong>

<strong>Part II: lab7C.c </strong>

<strong>Part III:lab7D2.c lab7DX.c</strong>

<strong> </strong>

You can issue <strong>submit –l 2031 lab7</strong> to view the list of file you have submitted.




<strong> </strong>

<h1>Common Notes</h1>

All submitted files should contain the following header:

/***************************************

<ul>

 <li>EECS2031 – Lab 7 *</li>

 <li>Author: Last name, first name *</li>

 <li>Email: Your email address *</li>

 <li>eecs_num: Your eecs login username *</li>

 <li>York #: Your student number</li>

</ul>

****************************************/




<strong> </strong>

<strong> </strong>

<strong> </strong>