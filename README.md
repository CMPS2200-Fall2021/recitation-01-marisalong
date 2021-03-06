# CMPS 2200  Recitation 01

**Name (Team Member 1):** Marisa Long
**Name (Team Member 2):** Anna Schoeny

In this recitation, we will investigate asymptotic complexity. Additionally, we will get familiar with the various technologies we'll use for collaborative coding.

To complete this recitation, follow the instructions in this document. Some of your answers will go in this file, and others will require you to edit `main.py`.


## Setup
- Login to Github.
- Click on the assignment link sent through canvas and accept the assignment.
- Click on your personal github repository for the assignment (e.g., https://github.com/tulane-cmps2200/recitation-01-your_username).
- [Clone](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) the repository to your local device
- Complete the lab task
- [Add, commit, and push](https://docs.github.com/en/github/managing-files-in-a-repository/managing-files-using-the-command-line/adding-a-file-to-a-repository-using-the-command-line) your completed lab back up to GitHub.
  - You will need to issue `git add` for all files that you have modified, e.g., `main.py`, `README.md`, and any others that you modify as well.
  - For example, on the command line, in the same directory as your cloned lab:
```
$ git add main.py
$ git commit -m "Implement Required Functions"
$ git push origin main
```

You'll work with a partner to complete this recitation. You will be able to code together in the same `repl.it` instance. You can choose whose repl.it instance you will share. This person will click the "Share" button in their repl.it instance and email the lab partner.

## Turning in your work
- Only one team member needs to push your completed lab to github.
- In the README.md file, include the name of the team members.


## Comparing search algorithms

We'll compare the running times of `linear_search` and `binary_search` empirically.

- [ ] 1. In `main.py`, the implementation of `linear_search` is already complete. Your task is to implement `binary_search`. Implement a recursive solution using the helper function `_binary_search`.

- [ ] 2. Test that your function is correct by calling from the command-line `pytest main.py::test_binary_search`

- [ ] 3. Write at least two additional test cases in `test_binary_search` and confirm they pass.

- [ ] 4. Describe the worst case input value of `key` for `linear_search`? for `binary_search`?

**TODO: your answer goes here**
The worst case input value for `linear_search` would be a key that either is placed at the last index in the list or
is not contained in the list. In both of these cases, `linear_search` would check each element in the list in order and compare it to the key until it reached the end of the list. This runtime would be O(n) because it is linear.
The worst case input value for `binary_search` would occur if the key did not exist in the list. In this case, `binary_search` would keep checking the middle against the key and splitting the list in half until it reached a final number that would not match the key. This runtime would be O(log_2 n) because the list is reduced to half with each iteration.


- [ ] 5. Describe the best case input value of `key` for `linear_search`? for `binary_search`?

**TODO: your answer goes here**
The best case input value for `linear_search` would be if the key matched the value at index 0.
The best case input value for `binary_search` would be if the key matched the value at the middle index of the list located at (right+left)//2.
For both of these, the best case runtime would be O(1) because the key would be matched to the value on the first iteration.

- [ ] 6. Complete the `time_search` function to compute the running time of a search function. Note that this is an example of a "higher order" function, since one of its parameters is another function.

- [ ] 7. Complete the `compare_search` function to compare the running times of linear search and binary search. Confirm the implementation by running `pytest main.py::test_compare_search`, which contains some simple checks.

- [ ] 8. Call `print_results(compare_search())` and paste the results here:

**TODO: add your timing results here**
|        n |   linear |   binary |
|----------|----------|----------|
|       10 |    0.003 |    0.004 |
|      100 |    0.010 |    0.005 |
|     1000 |    0.107 |    0.008 |
|    10000 |    1.305 |    0.015 |
|   100000 |   14.704 |    0.031 |
|  1000000 |  207.099 |    0.032 |
| 10000000 | 2113.163 |    0.049 |

- [ ] 9. The theoretical worst-case running time of linear search is $O(n)$ and binary search is $O(log_2(n))$. Do these theoretical running times match your empirical results? Why or why not?

**TODO: your answer goes here**
The theoretical and empirical results for both linear and binary search seem to roughly match. For linear search, the empirical results show that each time n increases by a factor of 10, the linear search time increase by roughly a factor of 10. Theoretically, the worst-case runtime for linear search is O(n) for n elements, which yields the same result.  For binary search, the empirical results show that each time n increases by a factor of 10, the binary search time increases by roughly a factor of log_2 10. Theoretically, the worst-case runtime for linear search is O(log_2 n) for n elements, which aligns with our empirical results. 

- [ ] 10. Binary search assumes the input list is already sorted. Assume it takes $\Theta(n^2)$ time to sort a list of length $n$. Suppose you know ahead of time that you will search the same list $k$ times.
  + What is worst-case complexity of searching a list of $n$ elements $k$ times using linear search? **TODO: your answer goes here**
  The worst-case complexity using linear search in this situation would be the worst-case runtime of n elements, which is O(n), multiplied by the number of searches, k. This gives us k*O(n).
  + For binary search? **TODO: your answer goes here**
  The worst-case complexity using binary search in this situation would require sorting the list first, which takes Theta(n^2). It would then also take the worst-case runtime for n elements, which is O(log_2 n), multiplied by the number of searches, k. This gives us k*O(log_2 n)+Theta(n^2).
  + For what values of $k$ is it more efficient to first sort and then use binary search versus just using linear search without sorting? **TODO: your answer goes here**
  For k = 1, it will always be better to use linear search because it doesn't require the time-consuming sort first. Otherwise, it may be quicker to use binary search because the sorting only occurs once and each search then only takes O(log_2 n). Since we don't have to re-sort with binary search, the point at which binary search becomes more efficient occurs when k * O(log_2 n) + Theta(n^2) < k * O(n). This can be translated as larger values of k will make binary more efficient than linear search.
