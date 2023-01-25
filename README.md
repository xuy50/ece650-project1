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

| FF | Runing Time | Fragmentation | BF | Runing Time | Fragmentation |
|  ----  | ----  |  ----  | ----  |  ----  | ----  |
| ff_equal_size_allocs | 22.52s | 0.45 | bf_equal_size_allocs | 22.34s | 0.45 |
| ff_small_range_rand_allocs | 7.27s | 0.060 | bf_small_range_rand_allocs | 1.84s | 0.022 |
| ff_large_range_rand_allocs | 55.07s | 0.093 | bf_large_range_rand_allocs | 67.67s | 0.042 |
<br>

## Analysis of The Results

**equal_size_allocs**<br>
&emsp;&emsp;The `equal_size_allocs` tests' running time are almost the same, and the fragmentation are the same. I found that all data malloced into the heap are the same size which is `ALLOC_SIZE = 128`, and the data would be freed in order, so I think both the bf and ff way will use the same free region in the free list which is the first fit region in the free list. Therefore, both of `equal_size_allocs`'s running time and fragmentation should be the same, but because of normally time erorr the time will be very close but not the same.<br>

**small_range_rand_allocs**<br>
&emsp;&emsp;The `small_range_rand_allocs`'s results have a very large difference. For the fragmentation, the best fit way will choose the best matched free region, and the first fit will choose the first free region, which may not be the best matched one, so the first fit way's fragmentation will larger than the best fit way's. And the runing time also has a grate difference. For this case, there are many small range regions in the free list. The first fit way will use the first free region, which may not be the best matched one, so it can do split operations, then there may not be enough space left for after requests, and the `sbrk()` function will be called, which is a system call founction, so it will spend a lot of time. For example, the free list has five free regions, whose size in order are `[1,2,3,4,5]`, then try to malloc 5 regions to use whose size in order are `[5,4,3,2,1]`, then the first fit way will call two more times `sbkr()` than best fit way. What's more, the best fit way may reduce the length of the free list after each best match operation, which can reduce the times of traversing the free list, which can reduce the running time.<br>

**large_range_rand_allocs**<br>
&emsp;&emsp;<br>
<br>




