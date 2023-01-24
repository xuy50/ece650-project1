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
&emsp;&emsp;The malloc need to find a enough sapce region in the free space in the total heap space, so I think the linked list a good way to store the free regions. If we need to find a required free region, we can traverse the linked list to find it.<br>

## Results from My Performance Experiments

&emsp;&emsp;For the first fit methods:<br>

**ff_malloc**<br>
&emsp;&emsp;.<br>

**ff_free**<br>
&emsp;&emsp;.<br>

&emsp;&emsp;For the best fit methods:<br>

**bf_malloc**<br>
&emsp;&emsp;.<br>

**bf_free**<br>
&emsp;&emsp;.<br>

&emsp;&emsp;For the two performance study report methods:<br>

**get_data_segment_size**<br>
&emsp;&emsp;.<br>
<br>

**get_data_segment_free_space_size**<br>
&emsp;&emsp;.<br>
<br>

## Analysis of The Results

**tital**<br>
&emsp;&emsp;.<br>

**tital**<br>
&emsp;&emsp;.<br>

**tital**<br>
&emsp;&emsp;.<br>

**tital**<br>
&emsp;&emsp;.<br>

**tital**<br>
&emsp;&emsp;.<br>

**tital**<br>
&emsp;&emsp;.<br>
<br>




