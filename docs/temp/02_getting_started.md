## Exercises

##### 2.1-1 Using Figure 2.2 as a model, illustrate the operation of INSERTION-SORT on the array A = <31, 41, 59, 26, 41, 58>

<31, 41, 59, 26, 41, 58>
<26, 31, 41, 59, 41, 58>
<26, 31, 41, 41, 59, 58>
<26, 31, 41, 41, 58, 59>

##### 2.1-2 Rewrite the INSERTION-SORT procedure to sort into nonincreasing instead of non- decreasing order.

	for (int i=1; i < A.length; ++i)
		int val = A[i-1]
		for (int j=i-1; j > -1; --j)
			if (A[j] < val)
				A[j+1] = A[j]
			else
				break
		A[j+1] = val

##### 2.1-3 Consider the searching problem: Input: A sequence of n numbers A = <a_1, a_2, ..., a_n> and a value v. Output: An index i such that v = A[i] or the special value NIL if v does not appear in A. Write pseudocode for linear search, which scans through the sequence, looking for v. Using a loop invariant, prove that your algorithm is correct. Make sure that your loop invariant fulfills the three necessary properties.

	for (int i=0; i < A.length; ++i)
		if (v == A[i])
			return i
	return nil

##### 2.1-4 Consider the problem of adding two n-bit binary integers, stored in two n-element arrays A and B. The sum of the two integers should be stored in binary form in an (n + 1) -element array C . State the problem formally and write pseudocode for adding the two integers.

	int carry = 0 
	for (int i=n; i > -1; --i)
		C[i+1] = A[i] ^ B[i] ^ carry
		carry = (A[i] & B[i]) | (A[i] & carry) | (B[i] & carry)
	C[0] = carry

##### 2.2-1 Express the function n^3/1000 - 100n^2 - 100n + 3 in terms of \Theta notation.
	\Theta(n^3)

##### 2.2-2 Consider sorting n numbers stored in array A by first finding the smallest element of A and exchanging it with the element in A[1]. Then find the second smallest element of A, and exchange it with A[2]. Continue in this manner for the first n - 1 elements of A. Write pseudocode for this algorithm, which is known as selection sort. What loop invariant does this algorithm maintain? Why does it need to run for only the first n - 1 elements, rather than for all n elements? Give the best-case and worst-case running times of selection sort in ‚-notation.

	for (int i=1; i < A.length; ++i)
		int min = i
		for (int j=i+1; j < A.length; ++j)
			if A[j] < A[min]
				min = j
		swap(A[i-1], A[min])

Loop invariant: A[0] ... A[i-1] are sorted.

we don't need to run the algorithm if A.length == 1.
if A.length > 1, we only need to put (A.length-1) elements in the right position and thus we need loop n-1 elements

Best case: n^2
Worst case: n^2

##### 2.2-3 Consider linear search again (see Exercise 2.1-3). How many elements of the in- put sequence need to be checked on the average, assuming that the element being searched for is equally likely to be any element in the array? How about in the worst case? What are the average-case and worst-case running times of linear search in ‚-notation? Justify your answers.

Checked elements on average: n/2 = \Theta(n)
Worst case: n = \Theta(n)

##### 2.2-4 How can we modify almost any algorithm to have a good best-case running time?

Find the input of base case -> Pre-calculate the solution -> check if input is the bast case at the beginning of the algorithm -> return pre-calculated answer if it is; continue to run regular algorithm if not.

##### 2.3-1 Using Figure 2.4 as a model, illustrate the operation of merge sort on the array A <3, 41, 52, 26, 38, 57, 9, 49>.

3, 9, 26, 38, 41, 49, 52, 57
3, 26, 41, 52   |   9, 38, 49, 57
3, 41 | 26, 52 | 38, 57 | 9, 49
3 | 41 | 52 | 26 | 38 | 57 | 9 | 49

##### 2.3-2 Rewrite the MERGE procedure so that it does not use sentinels, instead stopping once either array L or R has had all its elements copied back to A and then copying the remainder of the other array back into A.

	Merge (A, p, q, r)
		n_1 = q - p + 1
		n_2 = r - q
		// let L[1..n_1 + 1] and R[1..n_2+1] be new arrays
		for (int i=0; i < n_1; ++i)
			L[i] = A[p+i-1]
		for (int i=0; i < n_2; ++i)
			R[i] = A[q+i]
		int i, j;
		i = j = 0 
		while (i < n_1 && j < n_2)
			if (L[i] < R[j]) 
				A[i+j] = L[i]
				i++
			else
				A[i+j] = R[j]
				j++
		while (i < n_1)
			A[i+j] = L[i]
			i++
		while (j < n_2)
			A[i+j] = R[j]
			j++

##### 2.3-3 Use mathematical induction to show that when n is an exact power of 2, the solution of the recurrence
	T(n) = 2             if n =2
	       2T(n/2) + n   if n=2^k, for k > 1
is
	T[n] = nlgn

_Proof_

if n = 2 => T(n) = 2 = 2 lg 2 = nlgn
assume statement holds for T(k) where k > 2
then T(2k) = 2T(k) + 2k = 2klgk + 2k = 2k(lgk + 1) = 2k(lgk + lg2) = 2klg2k

Q.E.D.

##### 2.3-4 We can express insertion sort as a recursive procedure as follows. In order to sort A[1..n], we recursively sort A[1..n-1] and then insert A[n] into the sorted array A[1..n-1]. Write a recurrence for the running time of this recursive version of insertion sort.

	insertion_sort(A, n)
		if (n > 1)
			insertion_sort(A, n-1)
			key = A[n]
			int i=n-1
			for (; i > -1; --i)
				if (A[i] > key)
					A[i+1] = A[i]
			A[i+1] = key

##### 2.3-5 Referring back to the searching problem (see Exercise 2.1-3), observe that if the sequence A is sorted, we can check the midpoint of the sequence against v and eliminate half of the sequence from further consideration. The binary search al- gorithm repeats this procedure, halving the size of the remaining portion of the sequence each time. Write pseudocode, either iterative or recursive, for binary search. Argue that the worst-case running time of binary search is \Theta(lgn).

Iterative

	binary_search(A, start, end, target)
		while (start < end)
			mid = start + (end - start)/2
			if (A[mid] == target)
				return mid
			else if (A[mid] < target)
				start = mid + 1
			else
				end = mid
		return -1

Recursive

	binary_search(A, start, end, target)
		if (start < end)
			mid = start + (end - start) / 2
			if (A[mid] == target)
				return mid
			else if (A[mid] < target)
				return binary_search(A, mid+1, end, target)
			else
				return binary_search(A, start, mid, target)
		return -1

Base on above code, for each iteration, algorithm will throw away about half elements based on mid point compare result. Therefore T(n) = T(n/2) => T(n) = lgn

#####2.3-6 Observe that the while loop of lines 5–7 of the INSERTION-SORT procedure in Section 2.1 uses a linear search to scan (backward) through the sorted subarray A[1..j-1]. Can we use a binary search (see Exercise 2.3-5) instead to improve the overall worst-case running time of insertion sort to \Theta(nlg n)?

No, because array insert operation is O(n) so overall complexity is still O(n) * O(n) = O(n^2)

##### 2.3-7 Describe a \Theta(nlg n)-time algorithm that, given a set S of n integers and another integer x, determines whether or not there exist two elements in S whose sum is exactly x. 

sort S -> for each element of sorted S, test wheter (x - element) is in it by binary search.

Overall complexity = O(sorting) + O(n) * O(binary_search)
if we use merge sort, then = O(nlogn) + O(n)*O(lgn) = O(nlgn)

## Problems

##### 2-1 Insertion sort on small arrays in merge sort
Although merge sort runs in \Theta(nlgn) worst-case time and insertion sort runs in \Theta(n^2) worst-case time, the constant factors in insertion sort can make it faster in practice for small problem sizes on many machines. Thus, it makes sense to *coarsen* the leaves of the recursion by using insertion sort within merge sort when subproblems become sufficiently small. Consider a modification to merge sort in which n=k sublists of length k are sorted using insertion sort and then merged using the standard merging mechanism, where k is a value to be determined.

_a. Show that insertion sort can sort the n=k sublists, each of length k, in ‚.nk/ worst-case time._

_b. Show how to merge the sublists in \Theta(nlg(n/k)) worst-case time._

_c. Given that the modified algorithm runs in \Theta(nk + nlg(n/k)) worst-case time, what is the largest value of k as a function of n for which the modified algorithm has the same running time as standard merge sort, in terms of \Theta-notation?_

_d. How should we choose k in practice?_

a. sort cost for each sublist in worst case = \Theta(k^2)
Overall cost = n/k * \Theta(sorting) = n/k * \Theta(k^2) = \Theta(nk)

b.
	
	       n                n
	     /   \
	  n/2    n/2            n
	  / \    / \
	  ...    ...            ...
	 /    \  /   \
	k     k k     k         n/k * k = n

Above tree has height lg(n/k) and merge cost for each level is n, therefore the total worst cost is \Theta(nlg(n/k)) 

c. 

	nk <= nlgn and nlg(n/k) <= nlgn
	which implies: k <= lgn  and n/k <= n
	thus, 1 <= k <= lgn

Roughly, the largest k we can choose is k = lgn

d. It should depends on size of n, if lgn is not very large then k should be close to lgn; otherwise, we should choose a k less than lgn such that insertion sort is faster than merge sort for sorting k elements.

##### 2-2 Correctness of bubblesort
_Bubblesort is a popular, but inefficient, sorting algorithm. It works by repeatedly swapping adjacent elements that are out of order._

	BUBBLESORT(A)
	1 for i = 1 to A.length-1
	2 	for j = A.length downto i+1
	3		if A[j] < A[j-1]
	4			exchange A[j] with A[j-1]

_a. Let A' denote the output of BUBBLESORT(A). To prove that BUBBLESORT is correct, we need to prove that it terminates and that_

	A'[1] <= A'[2] <= ... <= A'[n],

_where n = A.length. In order to show that BUBBLESORT actually sorts, what else do we need to prove ? The next two parts will prove inequality (2.3)._

_b. State precisely a loop invariant for the for loop in lines 2-4, and prove that this loop invariant holds. Your proof should use the structure of the loop invariant proof presented in this chapter._

_c. Using the termination condition of the loop invariant proved in part (b), state a loop invariant for the for loop in lines 1–4 that will allow you to prove in- equality (2.3). Your proof should use the structure of the loop invariant proof presented in this chapter._

_d. What is the worst-case running time of bubble sort? How does it compare to the running time of insertion sort?_

a. A' is a permutation of A

b. 

	Init: A'[1..i] is sorted
	Maintenance: consider elements in A[i+1 .. n], compare two adjacent elements from right to left and swap two elements if the left one is smaller. thus, after the inner for loop, A'[1..i+1] is sorted.
	Terminate: A'[1..n] is sorted

c.

	Init: A'[1..i] is sorted, thus A'[1] <= A'[2] <= ... <= A'[i]
	Maintenance: consider elements in A[i+1 .. n], compare two adjacent elements from right to left and swap two elements if the left one is smaller. thus, after the inner for loop, A'[1..i+1] is sorted. Therefore, A'[1] <= A'[2] <= ... <= A'[i] <= A'[i+1]
	Terminate: A'[1] <= A'[2] <= ... <= A'[n].

d. Worst case: O(n^2). Compared to insertion sort, bubble sort cost O(n^2) even for best case; where insertion sort only cost O(n) in the same situation. 


##### 2-3 Correctness of Horner’s rule
The following code fragment implements Horner’s rule for evaluating a polynomial
	
	P(x) = \sum_{k=0}^n a_kx^k
		 = a_0 + x(a_1 + x(a_2 + ... + x(a_{n-1} + xa_n)...)),
given the coefficients a_0, a_1, ..., a_n and a value for x:

	1. y = 0
	2. for i = n downto 0 
	3.     y = a_i + x*sy

_a. In terms of ‚\Theta-notation, what is the running time of this code fragment for Horner’s rule?_

_b. Write pseudocode to implement the naive polynomial-evaluation algorithm that computes each term of the polynomial from scratch. What is the running time of this algorithm? How does it compare to Horner’s rule?_
	
_c. Consider the following loop invariant:_
	
_At the start of each iteration of the for loop of lines 2–3,_

	y = \sum_{k=0}^{n-(i+1)} a_{k+i+1}x^k

_Interpret a summation with no terms as equaling 0. Following the structure of the loop invariant proof prPesented in this chapter, use this loop invariant to show that, at termination,_ 

	y = \sum_{k=0}^n a_kx^k

_d. Conclude by arguing that the given code fragment correctly evaluates a poly- nomial characterized by the coefficients a_0, a_1, ..., a_n._

a. Running time = \Theta(n)

b. 

	naive_poly_eval
		y = 0
		for i = 0 to n
			acc = 1 
			for j = 0 to i
				acc = acc * x
			y = a_i * acc

Running time = \Theta(n^2)

Compared to Horner's rule, naive algorithm is much slower, \Theta(n) vs. \Theta(n^2)

c.

Consider the last iteration, where i = 0; from given loop invariant, we know at the beginning of the last iteration

	y = \sum_{k=0}^{n-(i-1)}a_{k+i+1}x^k = \sum_{k=0}^{n-1} a_{k+1}x^k 

From program, we know y = a_0 + x * y, which implies

	y = a_0 + x * y = a_0 + x * \sum_{k=0}^{n-1} a_{k+1}x^k
	                = a_0 * x^0 + \sum_{k=1}^n a_k x^k
					= \sum_{k=0}^n a_kx^k

d.

We know at the termination of loop (thus the end of program), 

	y = \sum_{k=0}^n a_kx^k = P(x)

##### 2-4 Inversions
Let A[1..n] be an array of n distinct numbers. If i < j and A[i] > A[j], then the pair(i, j) is called an inversion of A.

_a. List the five inversions of the array <2, 3, 8, 6, 1>_

_b. What array with elements from the set{1, 2, ..., n} has the most inversions? How many does it have?_

_c. What is the relationship between the running time of insertion sort and the number of inversions in the input array? Justify your answer._

_d. Give an algorithm that determines the number of inversions in any permutation on n elements in \Theta(nlg(n)) worst-case time. (Hint: Modify merge sort.)_

a. 

	<2, 1>, <3, 1>, <8, 6>, <8, 1>, <6, 1>

b. array <n, n-1, ..., 1> has the most inversions, which equals to n(n-1)/2

c. for each inversion, insertion sort have to go through the previous sorted subarray and do a insert operation. Thus the running time of insertion sort equals to O(NumOfInversions)

d. java code 

	int find_inversions(int[] arr) {
		if (arr == null || arr.length < 2) {
			return 0;
		}
		int mid = arr.length / 2;
		int left = find_inversions(arr, 0, mid);
		int right = find_inversions(arr, mid, arr.length);
		int[] buf = new int[arr.length];
		return left + right + merge(arr, buf, 0, mid, arr.length);
	}
	
	int merge(int[] arr, int[] buf, int start, int mid, int end) {
		int i = start;
		int j = mid;
		int k = start;
		int inversions = 0;
		while (i < mid && j < end) {
			if (arr[i] <= arr[j]) {
				buf[k] = arr[i];
				i++;
			} else {
				buf[k] = arr[j];
				inversions++
				j++;
			}	
			k++;
		}
		while (i < mid) {
			buf[k++] = arr[i++];
		}
		while (j < end) {
			buf[k++] = arr[j++]
		}
		for (int i=start; i < end; ++i) {
			arr[i] = buf[i];
		}
		return inversions;
	}
