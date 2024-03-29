#  DAA Notes for MST
> Author : Aaron Augustine

> Star the gist so that I can get a consensus on how many people are using this resource

# Searching & Sorting Algorithms

> Cheat sheet for algorithm Time Complexity 

| Algorithm | Best | Average | Worst | Auxillary Space |
|--|--|--|--|--|
|Selection Sort|O(n<sup>2</sup>) | O(n<sup>2</sup>) | O(n<sup>2</sup>)| O(1) |
|Insertion Sort & Bubble Sort | O(n) | O(n<sup>2</sup>)|O(n<sup>2</sup>)| O(1) or O(n) for worst case |
|Quick Sort | O(nlogn) | O(nlogn) | O(n<sup>2</sup>) | O(logn) or O(n) for worst case|
|Merge Sort | O(nlogn) | O(nlogn) | O(nlogn) | O(n) |
|Unsorted Case| O(1) | O(n) | O(n) |
|Binary Search | O(1) | O(logn) | O(logn) |

<hr>
<br>

> [Additional Reference : GFG Sorting Techniques](https://www.geeksforgeeks.org/analysis-of-different-sorting-techniques/)

<br><br>

## Unsorted Case  

*Best Case* : Here the best case would be if the element to be found is the first element [ O(1)]
*Average Case* : O(n)
*Worst Case* : Element to be found is the last element [ O(n) ] 

#### *Pseudocode*
```
function search(A, K)
    i = 0;

    while i < n and A[i] != K do
        i = i + 1;

    if i < n
        return i;
    else
        return -1;

```
#### *Python Code*
```python
def search(array, k ):
	i = 0
	n = len(array)
while i < n and A[i] != k : 
	i = i + 1

if i <n : 
	return i;
else : 
	return -1;

#remaining code to input the values into unsorted search
```

> Worst case would be the need to scan the entire sequence A. 
> * Time complexity : O(n)

**Now let us look at the case where A is sorted**
Steps to follow : 
* Compare k with midpoint of A
* If midpoint is K, the value is found
* If K < midpoint, search left half of the array
* If K > midpoint, search right half of the array

<br><br>

## Binary Search 
*Best Case* : Here the best case would be if the element to be found is the middle element [ O(1) ]
*Average Case* : O(log<sub>2</sub>n)

*Worst Case* : Element to be found is on either extremes[ O(log<sub>2</sub>n)
] 

> Since it is **Binary** search, the base of the log will be 2

#### *Pseudocode*
```
bsearch(K, A, l, r) // A sorted, search for K in A[l..r-1]
    if (r - l == 0)
        return false

    mid = (l + r) div 2 // integer division

    if (K == A[mid])
        return true

    if (K < A[mid])
        return bsearch(K, A, l, mid)
    else
        return bsearch(K, A, mid + 1, r)
```


#### *Python Code*
```python
def bsearch(k, array, l, r) :
	if ( r - l == 0):
		return false
	
	mid = ( l + r )/2
	if ( k == arra[mid]) : 
		return true
	if ( k < array[mid]):
		return (bsearch(k, array, l, mid))
	else:
		return (bsearch(k, array, mid+1, r))

#remaining code to input the values into bsearch
```

> T(n) : time to search an array of size n :
> T(0) = 1
> T(n) = 1 + T(n/2)

Therefore if we unwind the recurrence
> T(n) = 1 + 1 + T(n/2^2^) = .....
> T(n) = 1 + 1 + ...... + T(n/2^k^)
> T(n) = 1 + 1 + ... + 1 + T(n/2^logn^) = O(logn)

**Binary search works only for arrays**

<br><br>

## Selection Sort 
*Best Case* : O(n<sup>2</sup>)
*Average Case* : O(n<sup>2</sup>)
*Worst Case* : O(n<sup>2</sup>)

> The idea here is to move the item into it's correct place in the final sorted list ( Not to use another extra array ).
> * It basically iterates through the array.
> * Compares each element to the current element.
>  * Looks to swap if the compared element is smaller.

#### *Pseudocode*
```
SelectionSort(A, n) // Sort A of size n
    for (startpos = 0; startpos < n; startpos++)
        // Scan segments A[0]..A[n-1], A[1]..A[n-1], ...
        
        minpos = startpos;
        for (i = minpos + 1; i < n; i++)
            if (A[i] < A[minpos])
                minpos = i;

        swap(A, startpos, minpos)

```

#### *Java Code*

```java
import java.io.*;
import java.util.Scanner;

public class selection_sort {
    
    void sort(int arr[]) {
        int n = arr.length;

        // Traversing the array
        for(int i = 0; i < n; i++) {
            int min_idx = i;
            for(int j = i + 1; j < n; j++) {
                if(arr[j] < arr[min_idx])
                    min_idx = j;
            }

            // Time to swap them
            int temp = arr[min_idx];
            arr[min_idx] = arr[i];
            arr[i] = temp;
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        selection_sort ob = new selection_sort();

        // int arr[] = {24, 70, 22, 4, 65, 7, 21};
        System.out.print("Input the size of the array to be sorted : ");
        int size = scanner.nextInt();

        int arr[] = new int[size];

        System.out.print("Input the elements of the array : ");
        for(int i = 0; i < size; i++) {
            arr[i] = scanner.nextInt();
        }

        scanner.close();

        ob.sort(arr);
        System.out.println("Sorted Array");
        int n = arr.length;
        for(int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
            System.out.println();
        }
    }
}
```


> Time complexity : O(n<sup>2</sup>)
> Finding minimum in unsorted segment of length k requires one scan, k steps
> T(n) = n + (n-1) + (n-2) + ..... + 1 = n(n+1)/2 = O(n<sup>2</sup>)

<br><br>

## Selection Sort <sub>Recursive</sub>
*Best Case* : O(n<sup>2</sup>)
*Average Case* : O(n<sup>2</sup>)
*Worst Case* : O(n<sup>2</sup>)

#### *Pseudocode*
```
SelectionSort(A, start, n) // Sort A from start to n-1
    if (start >= n - 1)
        return;

    // Locate minimum element and move to start of segment
    minpos = start;
    for (i = start + 1; i < n; i++)
        if (A[i] < A[minpos])
            minpos = i;

    swap(A, start, minpos)

    // Recursively sort the rest
    SelectionSort(A, start + 1, n)

```

#### *Python Code*
```python
def selection_sort_recursive(A, start, n):
    if start >= n - 1:
        return
    
    # Locate minimum element and move to start of segment
    minpos = start
    for i in range(start + 1, n):
        if A[i] < A[minpos]:
            minpos = i
    
    # Swap elements
    A[start], A[minpos] = A[minpos], A[start]
    
    # Recursively sort the rest
    selection_sort_recursive(A, start + 1, n)

# Example usage:
array = [64, 25, 12, 22, 11]
selection_sort_recursive(array, 0, len(array))

print("Sorted array:", array)

```
<br><br>


## Insertion Sort 
*Best Case* : O(n<sup>2</sup>)
*Average Case* : O(n<sup>2</sup>)
*Worst Case* : O(n<sup>2</sup>) 

The *Worst Case* here would be passing an already sorted array to insertion sort. ( Since it checks from right to left to see where the element fits in the array )

> * We take the top most paper in the stack and then create a new stack. 
> * Take a second paper and compare it to the first, and then place it with respect to the first paper.
> * Similarly as the papers in crease compare the paper taken from the 1st stack with n number of papers in the second stack and place it accordingly.

#### *Pseudocode*
```
InsertionSort(Arr,n)
	for(pos = 1; pos < n; pos++)
	// In each iteration Arr[0].... Arr[pos-1] is already sorted
	
	nextpos = pos
	while(nextpos > 0 && Arr[nextpos] < Arr[nextpos - 1])
		swap(Arr,nextpos,nextpos-1)
		nextpos = nextpos - 1
```

<hr>

## Merge Sort 
*Best Case* : O(n logn)
*Average Case* : O(n logn)
*Worst Case* : O(n logn)

The *Worst Case* here would be passing [5,6,7,8,9,1,2,3,4] to the algorithm.


> When combining two sorted arrays we use merge sort in case the elements of the two arrays will stack in a different sorted order if merged.

#### *Pseudocode*
```
function Merge(Arr, m, B, n, C )
	
	i, j, k = 0;
	
	while(k < m+n)
		if(j == n or A[i] <= B[j] )
			C[k] = A[i]; i++;k++;
		
		if(i == m or A[i] > B[j])
			C[k] = B[j]; j++;k++;
```

<hr>

## Quick Sort
*Best Case* : O(n logn)
*Average Case* : O(n logn)
*Worst Case* : O(n<sup>2</sup>)

The *Worst Case* here would be passing an already sorted array (either in ascending or descending order) to Quick sort. 

>We choose a pivot element ( say the very first value.
>Parition it into lower part ( lesser than pivot ) and upper part ( greater than pivot ) 
>Then we recursively sort those two halves and finally combine the sorted subarrays

#### *Pseudocode*
```
QuickSort(Arr,l,r)
	if( r - l <= 1)
		return;
	
	yellow = l + 1;
	for( green = l + 1; green < r; green++ ) 
		if ( Arr[green] <= Arr[l] ) // l is pivot element
			swap(Arr, yellow, green);
			yellow++;
		
	swap(Arr,l,yellow-1); // moving pivot element ahead of lower part

	//Recursively calling QuickSort
	Quicksort(Arr,l,yellow-1);
	Quicksort(Arr,yellow,r);

```

### *Python Code*
```python
def QuickSort(Arr, l, r):
    if l >= r:
        return
    
    yellow = l + 1
    for green in range(l + 1, r):
        if Arr[green] <= Arr[l]:
            Arr[yellow], Arr[green] = Arr[green], Arr[yellow]
            yellow += 1
            
    Arr[l], Arr[yellow - 1] = Arr[yellow - 1], Arr[l]
    
    # Recursively calling QuickSort
    QuickSort(Arr, l, yellow - 1)
    QuickSort(Arr, yellow, r)

# Example input and usage
Arr = [3, 6, 8, 10, 1, 2, 1]
QuickSort(Arr, 0, len(Arr))
print("Sorted array:", Arr)

```
<hr>



# Questions for MST

## PYQ's


> [Reference : Math markdown](https://en.wikibooks.org/wiki/LaTeX/Mathematics)

<br>

#### Q1 a. A machlne needs a minimum of 300 sec to sort 1100 elements by Quick sort. The minimum time needed to sort 200 elements will be?

**Ans**.Minimum time needed to sort 200 elements with *Quick Sort* means 
T(n) = O(nlogn) 

t<sub>1</sub> = 300 sec
n<sub>1</sub> = 1100 elements
t<sub>2</sub> = ??
n<sub>2</sub> = 200elements

So, 



 $\frac{300} {x}= \frac{1100 log 1100} {200 log 200}$ 
 
 $\frac{300} {x}= \frac{1100}{200} \times \frac{log 1100} { log200 }$ 
 
 $x = 300 \times \frac{2}{11} \times 0.75657116126 =41.267seconds$

<hr>

#### Q1 b. Explain the characteristics of an algorithm 

**Ans**.  *An algorithm is  aset of well defined instructions to solve a particular problem*

It's characteristics are as follows :  <mark>IOFUEL</mark>
* Input : Requires input ( other than 0 )
* Output : Outcomes at the end of algo
* Finiteness : No, of instructions should be finite 
* Unambiguity : Instructions should be clear
* Effectiveness : Should be adequate to solve the problem
* Language Independent : Instructions can be implemented in any language

**![](https://lh7-us.googleusercontent.com/XUTtGr-QhOm7WYW8dDSjlNicxs5UMCiE9kzUkMjPhvO4ArvjTUmtsHtvMAmgRL_jf9FslJtoLcss7-qRX3uQSu0Oa0IEKiZ837G3F_TWb2nXJmvLcHPqQ_kmszPD7UCD_Q15-suyXMYxZOXWWxdFbU0)**

<hr>

#### Q2 a. What is stable sorting and give example of stable and unstable sorting algorithms

**Ans**. 
### Stable Sorting 
Stable sorting referes the a sorting algorithm's ability to preserve the relative order of two equal elements in the input array. 
Ex. If students are listed in alphabetical order along with their Math marks.
> If after sorting, students with the same marks are still in alphabetical order then it is stable sorting.

### Examples of stable and unstable sorting :
Stable Sorting Algorithm : **Merge Sort**
* Merge sort is stable if we merge carefully, i.e., if we don't allow the elements from the right to overtake the elements from the left.
* Favour the left list while breaking ties.

Unstable Sorting Algorithm : **Quick Sort**
* The swap operation that takes place during partitioning disturbs the original order.


<hr>

#### Q2 b. Write the algorithm for selection sort using recursion 


#### *Pseudocode*
```
SelectionSort(Arr,start,n)
	if ( start >= n-1 )
		return;
	
	minpos = start;
	//Locate the minimum element and move it to the start of the segment
	for( int i = start + 1; i < n; i++)
		if( Arr[i] < Arr[minpos] )
			minpos = i;
		
	swap(Arr, start, minpos);

	//Recursively call SelectionSort function
	SelectionSort(Arr,start+1,n);
		
```

#### *Algorithm*
1. Start with the second element in the array ( Iterate through to the last element )
2. Set the current element as key for each iteration.
3. Compare the key with the previous element, if it is smaller then swap it.
4. The above process continues till the previous element is not greater than the key.
5. With recursion we will just have to pass the index of the next key to the function

<hr>

####  Q3 a. What is the time complexity of this code, 
```
for (i = 0; i < n; i++) {
    for (j = 0; j < i * i; j++) {
        if (j % i == 0) {
            for (k = 0; k < j; k++){
                printf("xyz");
            }
        }
    }
}

``` 
?

**Ans**. T(n) of for loop<sub>1</sub> : O(n)
> Loop executes from i = 0 to i = n

T(n) of for loop<sub>2</sub> : O(n<sup>2</sup> - n)  $\approx$ O(n<sup>2</sup>)
> Loop executes from i = n to i= n<sup>2</sup>

T(n) of for loop<sub>3</sub> : O(n<sup>2</sup>)
> Since the maximum value of j here does till n<sup>2</sup> it executes from k=0 to k = n<sup>2</sup>

Hence overall complexity = O(n<sup>5</sup>)

<hr>

#### Q3 b. Sort the following array using quicksort method 
> 24  56  47  35  10  90  82  31

**Ans**. 
**![](https://lh7-us.googleusercontent.com/XU_dhretlAbnvwEcALd7Z0-VD7FLCkQ41g-vWnP59o8AuEOaFGSq-CbOna_xlLdcZBZsm3x94zflrwDP1vdh_9FsdGrvtBXBhOzWvQF4VOlDi0U72_-EjfYMHnAO3sgmq1EiyUZ74uzmCLVztWFnKB4)**
**![](https://lh7-us.googleusercontent.com/6N2nAxLGtJmV6hCIY_fY9sFBAswVcC6vY36kVqKIcvR5glvZP5vesit8BkkBGiz3ZR4WiInQo9acRLQXKWSUdDFWiDEfXPdmGaKiuTQx5PazlEKY0w03Xq4_UickocyVmHlRRKoJ1xjR8_OxZePZ70A)**

<hr>

#### Q4 a. Which sorting algorithm is best if the list is already sorted ? Why?

**Ans**. If the list is already sorted, the best sorting algorithm to use would be **Insertion Sort**.

The reason is that Insertion Sort has a time complexity of O(n) in the best-case scenario when the input list is already sorted. In this case, Insertion Sort simply performs a linear scan through the list to confirm that it's sorted, resulting in minimal comparisons and swaps.

Other sorting algorithms like Merge Sort, Quick Sort, or Heap Sort have a worst-case time complexity of O(n log n), even if the list is already sorted. This means they would still perform additional comparisons and swaps, even though they are unnecessary in this scenario.
<hr>

## Questions for the Exam!

#### Q1. What is an Algorithm ? Why do we analyse algorithms?

**Ans**. *An Algorithm is the step-by-step instruction given to sove a certain problem*
Just how there are many ways to travel from a given 'City A' to 'City B', there can be multiple algorithms for a given question. 
Analysing them helps us figure out which algorithm is the most suitable and the most effective.

<hr>

#### Q2. What is running time anaylsis ?

**Ans**. It is the process of determining how processing time increases as the size of the problem ( input size ) increases. 
The following are the different types of inputs we encounter : 
* Size of an array
* Polynomial Degree
* Number of elements in a  matrix
* Number of bits in binary representation of the input
* Vertices and edges of a  graph

<hr>

#### Q3. What is meant by Time Complexity 
of an algorithm ?

**Ans**. Time complexity of an algorithm is the time taken by it to solve the problem in question.

There can be three cases for time complexity ( Asymptotic Notation )
1. Worst Case
2. Average Case
3. Best Case

#### Q4. What is Upper Bound analysis ?

**Ans**. It is the case where the maximum number of operations have to be executed to solve the problem / sort the array.
Ex. For Linear Search the worst case would be when the element is not present in the array. O(n)

<hr>
<br><br><br>

# Introduction PPT - Shortnotes


## Basics ( Variables, Datatypes, etc )
> Ref : [Chap_1_pdf](https://classroom.google.com/c/NjU3MzUwMzg0NDgy/m/NjU4Mjc0MDkzNDYx/details)

## Variables
X, y, z or any other alphabets that are used as "*placeholders*" to store values ( data ) are known as variables.

## Data types
The variables defined form equations when used. To solve the equations we need them to hold specific types of values and 'data type' is the name being use to define those specific values.
*In Programming language it is a set of data with values having predefined characteristics* 
> Ex. : char, integer, boolean, long int, short int, etc

There are two types of Data Types : 
- System defined data types / Primitive Data types ( *int, float, char, double, bool, etc ....* )
- User Defined Data types : 
![](https://lh7-us.googleusercontent.com/rylKh1jPp5tTkKNDRyDw4jy8VJTXGnKO9BAdBF_AhoevlPpGEkTV8AYI693xJW3NIaByvFifQNjldUqIYLJWQmN6AXWRIQGK0S_UqY3n9AW3zUthqG20MaaMf1m636t69-LZNgKVz1k4tg9Q758DkZ4)

<hr>

## Data Structure 

> [Reference : Data structure based mcqs](https://www.sanfoundry.com/sorting-multiple-choice-questions-mcq/)


*Data Structure is a particular way of storinga nd organizing data on a computer so that it can be used efficiently*
There are two types of Data Structures : 
* Linear Data Structures ( *elements are accessed in a sequential order*)
* Non-Linear Data Structures (*elements are stored/accessed in a non-linear order*)

## Abstract Data Types <sub>ADT's</sub>
When we combine the user defined data structures with their operations they are known as 'Abstract Data Types', and they consist of two parts : 
* Declaration of Data
* Declaration of Operations

Ex : Linked Lists, Stacks, Queues, Priority Queues, Binary Trees, Dictionaries, Disjoint Sets, Hash Tables, Graphs, etc
<hr>

## Commonly Used Rate of growths

**![](https://lh7-us.googleusercontent.com/2xn1LSkl1ln_fqdyGy_zTpqf4RTOVa0sWsjRShl66SWilHgt-vIoXbMa7UWKujaJloy0GvPnxFczfhL_LzM2rTnV5uwGmueezRQlzw6egAeUFlsz7K2MmsSkXXMkPC1OOPp3U79SFFbfby5Xk-5EACE)**
The table above shows the relation between different rates of growth and examples

**![](https://lh7-us.googleusercontent.com/7lwSiL-rvYP66ye8VnLkpxkWpex5wZjH1UExrhnFXop-0t5aBDcRVLWNGWT67t9ni1An9V5__tkyLXh9RAvEKdYRlhukY0dGOtvuFlcPv2fKdPjQgDFsFCPE7DXg1l_OH6tlPA9Q5LzrCEJZHEpM4Hg)**
The flowchart above describes the decrease in time complexity, of the rate of growth.

> There are 3 types of analyis : 
> * Worst Case
> * Best Case 
> * Averge Case

<hr>

## Asymptotic Notation
[Reference : Aysmptotic notations - Big-O,Ω and theta](https://www.youtube.com/watch?v=A03oI0znAoc)


##  Big-O Notation 
*This shows upper bound of a function
*Represented as f(n) = O(g(n)), i.e. for larger values of n, f(n) = g(n)


## Big-Ω Notation
* This shows lower bound of a function



## Theta Notation
* This shows the average bound of afunction

<hr>
<br><br><br>

# Arrays and Linked Lists 
> [Reference : Array and Array ops mcqs](https://www.sanfoundry.com/data-structure-questions-answers-array-array-operations/)

## Linked List 
It is a DS used to store collections of data, and it has the following properties
* Successive elements are connected by pointers.
* Last elements points to NULL
* Can grow or shrink in size during execution of a program
* Can be made just as long as required
* Does not waste memory space 

### Main linked list operations : 
* **Insert** : Inserts an element into the list
* **Delete** : Deletes an element from the list : 

### Auxillary linked list operations
* **Delete List** : Removes all the elements of the list / disposes of the list 
* **Count** : Returns the number of elements in the list 
* Find n^th^ node from the end of the list

<hr>

## Arrays 
**![](https://lh7-us.googleusercontent.com/u1tT-MC3ilPz4B14Z2NyewoKneBuAs41xufwguVhYx6IxN7KlHDKjs_dQOzdfMnpiQOQxgySPUvwLUH8dH_z7XApN1KkeJRDNGB37wRtLl1jQvv9FY3TBTzKOYWC3wO4wQSt5FNPDuPy1asdyXZj5_4)**

### Advantages of Arrays : 
1. Simple and easy to use 
2. Faster access to the elements

### Disadvantages of Arrays : 
1. **Fixed Size** : The size of the array is static ( specify the array size before using it ) 
2.**One block allocation** : To allocate the array at the beginning itself, sometimes it may not be possible to get the memory for the complete array.
3. **Complex position-based insertion** : TO insert an element at a given position we may need to shift the elements. This will create a position for us to insert the new element at the desired position.

**The main disadvantage of linked lists is the long access time for any element in a linked list**

## Difference between Linked Lists and Arrays
**![](https://lh7-us.googleusercontent.com/NAA1UFQ0FDQeuqWy0qmLmAL3aa8nVEAc7xyeI33P_7z_wl6LB-HX0YPwEFI0Ul3mlQscFeqcspIVXxbLGESJcB6eb4I3dLwD8-16mUQPMTdd8XUI9H8NBzPXFhLimice1EWISd3OotRYumeAUyyi28g)**


# Stacks and Queues

## Stacks
A stack is a simple data structure used for storing data. In this the order that they arrive in is important, just like a stack of plates, the first one stacked is the last to be used.

> Two operations that can be done on a stack are "Push" (insert data ) and "Pop" ( remove data )

**![](https://lh7-us.googleusercontent.com/eB8AtQSRUY1d89s7QtMfoSSsiVcKzPgAbnwL6hhH5-EJyjPV77aE7FMjnH1QGBbiJluc-malu0khGY975dkPQyWkYZgZTEJwpv1m9Yk_DB32auUOUPxUCTVRtz38hemQMRklcb4frrTUsXEKywRM89Q)**

> It is an ordered list, where insertion and deletion are done at one end.
> The Last element inserted is the first one to be deleted and hence it is called Last In First Out or First In Last Out ( LIFO / FILO )


## Queues
A queue is a data strucutre used to store data, in which the order that the data arrives is important.

It is an ordered list in which insertions are done at one end ( *rear* ) and deletions are done at the other end (*front*)

Also known as First in First Out or Last in Last Out

### Applications of Queues : 
* Operating System schedule jobs in the order of arrival
* Simulation of real world queues
* Multiprogramming
* Asynchronous data transfer, etc

