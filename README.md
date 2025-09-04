# CMPS 2200  Recitation 01

**Name (Team Member 1):** Kiet Huynh
**Name (Team Member 2):** Tri Huynh

In this recitation, we will investigate asymptotic complexity. Additionally, we will get familiar with the various technologies we'll use for collaborative coding.

To complete this recitation, follow the instructions in this document. Some of your answers will go in this file, and others will require you to edit `main.py`. All tests are in `test_main.py`.

## Install Python Dependency

We need Python library of "tabulate" to visualize the results in a good shape. Please install it by running 'pip install tabulate' or 'pip install -r requirements.txt' in Shell Tab of Repl.  

## Running and testing your code

- To run tests, from the command-line shell, you can run
  + `pytest test_main.py` will run all tests
  + `pytest test_main.py::test_one` will just run `test_one`
  + We recommend running one test at a time as you are debugging.

## Turning in your work

- Once complete, click on the "Git" icon in the left pane on repl.it.
- Enter a commit message in the "what did you change?" text box
- Click "commit and push." This will push your code to your github repository.
- Although you are working as a team, please have each team member submit the same code to their repository. One person can copy the code to their repl.it and submit it from there.

## Comparing search algorithms

We'll compare the running times of `linear_search` and `binary_search` empirically.

`Binary Search`: Search a sorted array by repeatedly dividing the search interval in half. Begin with an interval covering the whole array. If the value of the search key is less than the item in the middle of the interval, narrow the interval to the lower half. Otherwise, narrow it to the upper half. Repeatedly check until the value is found or the interval is empty.

- [ ] 1. In `main.py`, the implementation of `linear_search` is already complete. Your task is to implement `binary_search`. Implement a recursive solution using the helper function `_binary_search`. 

- [ ] 2. Test that your function is correct by calling from the command-line `pytest test_main.py::test_binary_search`

- [ ] 3. Write at least two additional test cases in `test_binary_search` and confirm they pass.

- [ ] 4. Describe the worst case input value of `key` for `linear_search`? for `binary_search`? 

**TODO: your answer goes here**

For linear search, the worst case is when 'key' is not in the list because the algorithm has to check all n elements.

For binary search, the worst case is when 'key' is not in the list or is located at the very last search step. The algorithm must keep halving until the search space is empty.

- [ ] 5. Describe the best case input value of `key` for `linear_search`? for `binary_search`? 

**TODO: your answer goes here**

For linear search, the best case is when key is the first element in the list, so only one comparison is needed.

For binary search, the best case is when key is the middle element of the list, so it is found immediately on the first comparison.

- [ ] 6. Complete the `time_search` function to compute the running time of a search function. Note that this is an example of a "higher order" function, since one of its parameters is another function.

- [ ] 7. Complete the `compare_search` function to compare the running times of linear search and binary search. Confirm the implementation by running `pytest test_main.py::test_compare_search`, which contains some simple checks.

- [ ] 8. Call `print_results(compare_search())` and paste the results here:

**TODO: add your timing results here**
|        n |   linear |   binary |
|----------|----------|----------|
|       10 |    0.002 |    0.004 |
|      100 |    0.004 |    0.002 |
|     1000 |    0.039 |    0.002 |
|    10000 |    0.423 |    0.003 |
|   100000 |    4.193 |    0.009 |
|  1000000 |   41.741 |    0.012 |
| 10000000 |  427.828 |    0.015 |

- [ ] 9. The theoretical worst-case running time of linear search is $O(n)$ and binary search is $O(log_2(n))$. Do these theoretical running times match your empirical results? Why or why not?

**TODO: your answer goes here**

Yes, they match in general.
+ Linear search grows proportionally with n (the timings increase roughly linearly).
+ Binary search stays nearly flat, growing very slowly with n, consistent with O(log n).

But not exactly equal to theory:
+ For small input sizes, both searches run extremely fast and may look similar because of overhead (function calls, Python interpreter).
+ For large n, the difference becomes obvious: linear search times blow up, binary stays tiny.

- [ ] 10. Binary search assumes the input list is already sorted. Assume it takes $\Theta(n^2)$ time to sort a list of length $n$. Suppose you know ahead of time that you will search the same list $k$ times. 
  + What is worst-case complexity of searching a list of $n$ elements $k$ times using linear search? **TODO: your answer goes here** 
  O(k*n)
  + For binary search? **TODO: your answer goes here**
  O(k*log n)
  + For what values of $k$ is it more efficient to first sort and then use binary search versus just using linear search without sorting? **TODO: your answer goes here**
  - If list starts unsorted, the worst-case complexity of first sorting and then using binary search is O(n^2 + k log n).
  - Binary search becomes more efficient when n^2 + k*log n < k*n => k > n^2/n - log n
