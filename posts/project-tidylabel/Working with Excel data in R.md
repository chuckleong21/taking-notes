
<aside class='def'><a href='[Functional Programming Tools • purrr (tidyverse.org)](https://purrr.tidyverse.org/#usage)'>basic usage of purrr</a></aside>
### `For` loops, `apply`, and `map`
Previously, we set our [[From a function to a production#^d50ba3|first goal]] and method to carry it out. Since more often than not, we have more than one label, we are going to use `for` loops, or the tidyverse approach of `for` loops: `{purrr}`.

First we are reading the file : 
<aside class='descr'>The <code>sheet</code> argument indicates which worksheet is to be loaded</aside>
```r
 raw <- readxl::read_excel("../Emma/static/МРТ021 маркировка.xlsx", sheet = 2)
```
![[Pasted image 20240121163749.png|This is the output]]

There are few things noticable:
<aside class='descr'>Because <code>readxl</code> only recognizes text data</aside>
1. The `tibble` has 11 rows, 50 columns while there are 12 in the Excel table.
2. Empty header cells have repairing column names.

We want to grab every two columns, the traditional for loop would be:
```r
raw_list <- list()
for(i in seq(0, ncol(raw) - 2, 2)) {
  raw_list <- append(raw_list, list(raw[, 1:2 + i]))
}
head(raw_list, 3)
```
![[Pasted image 20240121165725.png]]
<aside class='descr'><code>list</code> can contain everything from numeric vector, matrices, to data frames, which, in fact, are lists that have equal length. </aside>
Before the beginning of the loop, a empty `list()` must be initiated to store the results, then we `append` the previous `raw_list` to the one in the current loop. `raw_list` shown above appears to be what we want.

<aside class='danger'>That being said, there are often times for loops are more <b>stable</b> than functional programming <code>map_*</code> functions since for loop does not restrict the type of output.</aside>
But[ building vectors is slow using for loops](https://stackoverflow.com/a/7144801) in R, the reason simply being the general writing idiom of a for loop: iterations involve growing and copying that take up memory. If the memory is allocated prior to the start of the loop. This problem should alleviate. We have the `map_*` functions `{purrr}` and `apply` family functions for this approach.





```r
# apply
raw_list_apply <- lapply(seq(0, ncol(raw) - 2, 2), function(i) raw[, 1:2 + i])

# map
raw_list_map <- map(seq(0, ncol(raw) - 2, 2), \(i) raw[, 1:2 + i])

identical(raw_list_apply, raw_list_map)
# [1] TRUE
```

> [!info]- Benchmark on for loops
> ```r
> 

| expression | min | median | itr/sec | total time |
| ---- | ---- | ---- | ---- | ---- |
| raw_list_apply | 415μs | 441μs | 2211 |  |
| raw_list_map | 451μs | 471μs | 2084 |  |
```

