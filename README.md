# ece650-project1

 - Author: Yang Xu
 - netID: yx248
 - Data: 01/24/2023
 - Instructor: Rabih Younes
 - Course: ECE651

## The Allocation Policies Implementation:

&emsp;&emsp;For this project we should implement the allocation policies. We should implement `6 method`:<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`//First Fit malloc/free`<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`void *ff_malloc(size_t size);`<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`void ff_free(void *ptr);`<br>

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`//Best Fit malloc/free`<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`void *bf_malloc(size_t size);`<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`void bf_free(void *ptr);`<br>

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`unsigned long get_data_segment_size(); //in bytes`<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`unsigned long get_data_segment_free_space_size(); //in byte`<br>
<br>

&emsp;&emsp;For the allocation policies, we should apply for enough heap space to store the required size space by `malloc method`. And free the specific address with `free method`.<br>
&emsp;&emsp;The malloc need to find a enough sapce region in the free space in the total heap space, and for the addresses are ordered in the free region list, so I think the doubled linked list a good way to store the free regions. If we need to find a required free region, we can traverse the linked list to find it. If we need store a new free region into the list, we can add or merge or split it easily by the properties of linked lists.<br>

The first fit methods:<br>

**ff_malloc**<br>
&emsp;&emsp;Firstly, check the free list, when find the first free region which is enough for the require size with the metadata size, split or use the free region. If the region's left part is lager than metadata size, split the size need to use for require size; otherwise, use the total region space. Then, if no free region is enough, use the sbrk system call to increase the heap size for require size, if no enough memory space can be increase for heap, return NULL.<br>

**ff_free**<br>
&emsp;&emsp;Check the address need to be freed whether it is NULL, if it is NULL, return back. Find the correct position for the address which need to be freed. The first address which is large the require address will be the required freed address next. And check whether the required freed address is contious with its prev or next, merge them together.<br>

The best fit methods:<br>

**bf_malloc**<br>
&emsp;&emsp;Firstly, check all of the free list, check the closest enough size free region, split or use the free region. If the region's left part is lager than metadata size, split the size need to use for require size; otherwise, use the total region space. Then, if no free region is enough, use the sbrk system call to increase the heap size for require size, if no enough memory space can be increase for heap, return NULL.<br>

**bf_free**<br>
&emsp;&emsp;Because the `bf_free()` is totally the same as the `ff_free()`, so I call the `ff_free()` to implement the `bf_free()`<br>

Two performance study report methods:<br>

**get_data_segment_size**<br>
&emsp;&emsp;This function is for return the totally heap size. I set a global variable to update the heap size when it use the system call `sbrk()` function.<br>

**get_data_segment_free_space_size**<br>
&emsp;&emsp;This function is for return the totally free region size in the heap. I set a global varialbe to update the free size when do free operation or do malloc operations for the free region.<br>
<br>

## Results from My Performance Experiments

| FF | Runing Time | Frag | BF | Runing Time | Frag |
|  ----  | ----  |  ----  | ----  |  ----  | ----  |
| ff_equal_size_allocs | 22.52s | 0.45 | bf_equal_size_allocs | 22.34s | 0.45 |
| ff_small_range_rand_allocs | 7.27s | 0.060 | bf_small_range_rand_allocs | 1.84s | 0.022 |
| ff_large_range_rand_allocs | 55.07s | 0.093 | bf_large_range_rand_allocs | 67.67s | 0.042 |
<br>

## Analysis of The Results

**title**<br>
&emsp;&emsp;.<br>

**title**<br>
&emsp;&emsp;.<br>

**title**<br>
&emsp;&emsp;.<br>

**title**<br>
&emsp;&emsp;.<br>

**title**<br>
&emsp;&emsp;.<br>

**title**<br>
&emsp;&emsp;.<br>
<br>




