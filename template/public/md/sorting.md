layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Sorting and Complexity

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---
# Sorting Algorithms

* an algorithm that puts elements of a list in a certain order
   * numerical order, lexicographical order, user-defined order

.row[
.col-4[

```python3
selection sort
insrtion sort
bubble sort
```

]
.col-8[

naive sorting  
O(*n*<sup>2</sup>)
]
]

.row[
.col-4[

```python3
merge sort
quick sort
```

]
.col-8[

efficient sorting  
O(*n* log *n*)
]
]

---
# Selection Sort

* The algorithm divides the input list into two parts: 
   * a sorted sublist and a sublist of the remaining unsorted items 
   

1. Initially, the sorted sublist is empty and the unsorted sublist is the entire input list. 
2. finding the smallest (or largest, depending on sorting order) element in the unsorted sublist,
3. exchanging (swapping) it with the leftmost unsorted element, 
4. and moving the sublist boundaries one element to the right.

.row[
.col-10[

<img src="https://user-images.githubusercontent.com/39995503/99181806-5757e600-2774-11eb-8ca2-c8b353b36287.png" width=450/>


]
.col-2[

<img src="https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif" width=55/>

]
]

https://en.wikipedia.org/wiki/Selection_sort

---
# Selection Sort

.row[
.col-10[
.font-15[
```python
def selSort(numList): 
    '''sort numList into ascending order'''

    # Iterate through all list elements 
    n = len(numList)

    for i in range(n): 

        # Find the minimum element in remaining unsorted sublist
        min_inx = i

        for j in range(i+1, n): 
            if numList[min_inx] > numList[j]: 
                min_inx = j

        # Swap the minimum element and the first element 
        numList[i], numList[min_inx] = numList[min_inx], numList[i]


sourceList = [8,5,2,6,9,3,1,4,0,7]
selSort(sourceList)
print(sourceList)
```
]
]
.col-2[
<img src="https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif" width=55/>
]
]

---
# Insertion Sort

* Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.


1. At each iteration, insertion sort removes one element from the unsorted sublist, 
2. finds the location it belongs within the sorted sublist, and inserts it there. 
3. It repeats until no unsorted elements remain.

.center[<img src="https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif"/>]


https://en.wikipedia.org/wiki/Insertion_sort

---
# Insertion Sort


.row[
.col-8[

.font-15[
```python
def insertionSort(numList):
    '''Implementation of insertion sort'''
    
    # iterate over numList
    for i in range(1, len(numList)): 
        j = i
        
        # find the place to insert numList[i]
        while j > 0 and numList[j] < numList[j-1] : 
            # swap numList[j] and numList[j-1]
            numList[j], numList[j-1] = numList[j-1], numList[j] 
            j = j -1

sourceList = [6,5,3,1,8,7,2,4]
insertionSort(sourceList)
print(sourceList)
```
]
]
.col-4[
<img src="https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif"/>
]
]

---
# Bubble Sort

* sometimes referred to as sinking sort


1. repeatedly steps through the list, 
2. compares adjacent elements and swaps them if they are in the wrong order. 
3. The pass through the list is repeated until the list is sorted.

<img src="https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif"/>

https://en.wikipedia.org/wiki/Bubble_sort

---
# Bubble Sort

.row[
.col-8.font-15[
```python
def bubbleSort(items):
    '''Implementation of bubble sort'''
    n = len(items)
    for i in range( n ) :
        for j in range(n-1-i) : 
            if items[j] > items[j+1] :                                     
                items[j], items[j+1] = items[j+1], items[j] 

sourceList = [6,5,3,1,8,7,2,4]
bubbleSort(sourceList)
print(sourceList)
```
]
.col-4[

<img src="https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif"/>
]
]

---
# Merge Sort

* a divide and conquer algorithm that was invented by .green[John von Neumann] in 1945

1. Divide the unsorted list into `n` sublists, each containing one element (a list of one element is considered sorted).
2. Repeatedly merge sublists to produce new .red[sorted] sublists until there is only one sublist remaining. 

.center[<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif"/>]

---
# Merge Sort

.row[
.col-5.font-14[
```python3
def mergeSort(list):
    '''Implementation of merge sort'''
    # base case
    if len(list) == 1: 
        return list[:] 

    # recursive case
    halfway = len(list) // 2
    list1 = list[0:halfway]
    list2 = list[halfway:len(list)]

   # recursively sort left half
    newlist1 = mergeSort(list1)
    # recursively sort right half
    newlist2 = mergeSort(list2)

    # merge the two halves
    newlist= merge(newlist1, newlist2)
    
    return newlist
```
]
.col-7.font-14[
```python3
def merge(a, b):
    index_a= 0 # the current index in list a
    index_b= 0 # the current index in list b
    c = [ ]

    while index_a< len(a) and index_b< len(b):
        if a[index_a] <= b[index_b]:
            c.append( a[index_a] )
            index_a= index_a+ 1
        else:
            c.append( b[index_b] )
            index_b= index_b+ 1
    # when we exit the loop
    # we are at the end of at least one of the lists
    c.extend( a[index_a:] )
    c.extend( b[index_b:] )
    return c
```
]
]

---
# Merge Sort

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e6/Merge_sort_algorithm_diagram.svg/2560px-Merge_sort_algorithm_diagram.svg.png" width=500/>

---
# Quick Sort

* a divide and conquer algorithm that was invented by .green[Tony Hoare] in 1959

1. Pick an element, called a pivot, from the list.
2. Partitioning: reorder the list so that 
   * all elements with values less than the pivot come before the pivot, 
   * while all elements with values greater than the pivot come after it (equal values can go either way). 
   * After this partitioning, the pivot is in its final position. 
3. Recursively apply the above steps to the sub-list of elements with smaller values and separately to the sub-list of elements with greater values.

https://en.wikipedia.org/wiki/Quicksort

---
# Quick Sort


```python3
def quickSort(numList, low, high):
    if low<high:
        p = partition(numList, low, high)
        print(p)
        quickSort(numList, low, p-1)
        quickSort(numList, p+1, high)


sourceList = [69, 10, 30, 2, 16, 8, 31, 22]
#sourceList = [8, 10, 7]

quickSort(sourceList, 0, len(sourceList)-1)
print(sourceList)
```


---
# Quick Sort - Partition

.row[
.col-8.font-14[

```python3
def partition(numList, low, high):
    pivot = (low + high)//2
    L = low
    R = high

    while L<R:

        while (numList[L] < numList[pivot]) and (L<R):
            L=L+1
        while (numList[pivot] <= numList[R]) and (L<R):
            R=R-1
            
        if L<R:
            numList[L], numList[R] = numList[R], numList[L]
            
            # cannot sort [8, 10, 7] without this
            if L == pivot:  
                pivot = R

    numList[pivot], numList[R] = numList[R], numList[pivot]

    return R
```
]
.col-4[
<img src="https://user-images.githubusercontent.com/39995503/99187387-b11ed700-2799-11eb-8066-128d85605b1d.png" width=250/>
]
]

---
# Complexity of Algorithms

* Given an algorithm, how .red[efficient] is this algorithm for solving a problem given input of a particular size?


* The .red[algorithmic complexity] of a computation is some measure of how difficult it is to perform the computation.


* Measures some aspect of cost of computation (in a general sense of cost).


* Common complexity measures:
   * .red[Time] complexity: # of ops or steps required
   * .red[Space] complexity: # of memory bits required

---
# Complexity Depends on Input

* Most algorithms have different complexities for inputs of different sizes.  
   * (e.g., searching a long list takes more time than searching a short one.)


* Therefore, complexity is usually expressed as a .red[function of input size].


* This function usually gives the complexity for the worst-case input of any given length.

---
# The Growth of Functions

* In both computer science and in mathematics, there are many times when we care about how fast a function grows.


* In computer science, we want to understand how quickly an algorithm can solve a problem as the size of the input grows. 


* We can compare the efficiency of two different algorithms for solving the same problem. 


* We can also determine whether it is practical to use a particular algorithm as the input grows. 
   * .red[Scalability]!

---
# Comparing Two Algorithms

* Suppose you are designing a web site to process user data (e.g., financial records).


* Suppose database program A takes f<sub>A</sub>(`n`)=30`n`+8 microseconds to process any `n` records, while program B takes f<sub>B</sub>(`n`)=`n`<sup>2</sup>+1 microseconds to process the `n` records.


* Which program do you choose, knowing you’ll want to support millions of users? 

.center[**A!**]

.center[<img src="https://user-images.githubusercontent.com/39995503/99189767-2d1f1c00-27a6-11eb-8e39-44d2c599341b.png" width=300/>]

---
# Order of Growth

<img src="https://user-images.githubusercontent.com/39995503/99189254-a6693f80-27a3-11eb-82ad-072f6a984ce5.png" width=500/>

---
# Order of Growth

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7e/Comparison_computational_complexity.svg/2560px-Comparison_computational_complexity.svg.png" width=500/>

---
# Computer Time Examples

* Assume time = 1 ns (10<sup>-9</sup> second) per op, problem size = `n` bits, #ops: a function of `n` as shown.

.center[<img src="https://user-images.githubusercontent.com/39995503/99189382-4626cd80-27a4-11eb-8b3a-261c5fe90ce5.png" width=500/>]

---
# Concept of Order of Growth

<img src="https://user-images.githubusercontent.com/39995503/99189486-bc2b3480-27a4-11eb-9286-cd04ba8ff8f9.png" width=700/>

---
# Big-O Notation: *O(g)* 

* at most order g

<img src="https://user-images.githubusercontent.com/39995503/99189577-23e17f80-27a5-11eb-896d-67541adf882d.png" width=700/>

---
# Examples of "Big-O" Proof

<img src="https://user-images.githubusercontent.com/39995503/99189620-6dca6580-27a5-11eb-9ca6-69a051d0f8af.png" width=700/>

---
# Order of Growth

<img src="https://user-images.githubusercontent.com/39995503/99189254-a6693f80-27a3-11eb-82ad-072f6a984ce5.png" width=450/>

<img src="https://user-images.githubusercontent.com/39995503/99190063-cc90de80-27a7-11eb-8a72-507f32c4d2af.png" width=800/>

* You will learn a lot about complexity of algorithms in .red[Data Structure] class, .red[Algorithms] class, and so on….!!!

---
# Comaring Sorting Algorithms

* Selection Sort -> O(`n`<sup>2</sup>)


* For a data list of size `n`
   * 1st round: inspects all `n` items for finding the smallest one
   * 2nd round: it inspects the remaining `n-1` items
   * … and do on


* The total number of .red[comparisons] in iterations is:

.center[<img src="https://user-images.githubusercontent.com/39995503/99190175-7a03f200-27a8-11eb-882b-d98938621879.png" width=500/>]

* contains an `n`<sup>2</sup> term which is the biggest term

---
# Comaring Sorting Algorithms

* Merge Sort -> O(`n`log<sub>2</sub>`n`)


* For a data list of size `n`
   * The number of levels: log<sub>2</sub>`n`
   * The number of comparisons in the merge step of each level: a little bit less than `n`
      * when merging two lists (each of which has M/2 elements)
      * best case: (M/2) comparisons
      * worst case: (M-1) comparisons


* The total number of .red[comparisons] in iterations is: `n`log<sub>2</sub>`n`     

---
# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.
* Introduction to Computation and Programming Using Python, John V. Guttag