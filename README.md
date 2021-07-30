# COMP 3430 lab 3

## Chen Dong, 7792042

# Screenshots for this lab
Set the timer to 5 seconds.
<img width="806" alt="futex" src="https://user-images.githubusercontent.com/66326548/127590759-e0c1007a-eb09-43f7-8f95-c9c599fc9e47.png">

Added an infinity loop to the end of this program.
<img width="839" alt="infinityloopthread" src="https://user-images.githubusercontent.com/66326548/127590836-3878a5d2-d943-4665-aff1-412920d4f7cc.png">

## successful running 
<img width="681" alt="Screen Shot 2021-07-29 at 9 34 01 PM" src="https://user-images.githubusercontent.com/66326548/127591389-e9ffa90c-ab3a-4401-b506-25c26f329b26.png">
<img width="1023" alt="Screen Shot 2021-07-29 at 9 34 24 PM" src="https://user-images.githubusercontent.com/66326548/127591393-84452f14-8581-4471-81dd-b2bb32ccc49b.png">


## output and gdb output(these output were taken after Finished queuing work)
<img width="343" alt="lab3-2cores-gdb" src="https://user-images.githubusercontent.com/66326548/127590894-788823d5-6ae9-429c-ae22-5ad34b21ee86.png">
<img width="670" alt="lab3-2coresoutput" src="https://user-images.githubusercontent.com/66326548/127590911-4e62d95d-2bfb-494d-afd6-2f2d3067a3ab.png">


# Question 1

## futex

# Question 2

## By looking at the output of this program, I recognize that the lock whose address is 0x6032c0 has the most contention which is 7632 times, and the variable name that refers the address is pool_mutex. The program is using pool_mutex to protect the pool data which is frequently used in the program.

# Question 3(ordered from highest to lowest)

 1:lock 0x6032c0 contended 7632 times and 4745 avg us, total waiting time = 7632*4745 = 36213840 us

 2:lock 0x603300 contended 3766 times and 1732 avg us, total waiting time = 3766*1732 = 6522712 us

 3:lock 0x603304 contended 329 times and 5607 avg us, total waiting time = 329*5607 =   1844703 us

 4:lock 0x7f12a24c6320 contended 33 times and 10142 avg us, total waiting time = 33*10142 = 334686 us

 5:lock 0x603344 contended 1 times and 7397 avg us, total waiting time = 7397 us

 6:lock 0x603284 contended 1 times and 3792 avg us, total waiting time = 3792 us

# Question 4(My VM ware only allows me to do 1,2,3 and 4 cores)
## 1,2,3 and 4 cores output screenshots, demonstration 

with 1 core

<img width="683" alt="1coreoutput" src="https://user-images.githubusercontent.com/66326548/127591445-bab7c537-2df3-48be-b67c-e030f4c8cae8.png">

with 2 cores

<img width="670" alt="lab3-2coresoutput" src="https://user-images.githubusercontent.com/66326548/127591481-930b971c-f418-45e5-b922-5321cceff8cb.png">

with 3 cores

<img width="686" alt="3coresoutput" src="https://user-images.githubusercontent.com/66326548/127591489-67ccad17-62ca-46cd-942b-10bab575ac06.png">

with 4 cores

<img width="724" alt="4coresoutput" src="https://user-images.githubusercontent.com/66326548/127591490-d72b2c66-41c6-4b24-90b0-115b3f77fc49.png">


summarize output and generate a table below:
| # of cores | lock address | variable name (+ 4) | contended times | avg in us | total waiting time in us)|
| :--------: | :----------: | :-----------------: | :-------------: | :-------: | :----------------: |
|1           | 0x6032c0     |   pool_mutex        |    679          |  11632    |       7898128      |
|1           |    0x603304  |   pool_workcv+4   |    1            |   24278   |       24278        |
|1           |  0x603344    |   pool_waitcv+4   |    1            |    6398   |       6398         |
|1           |    0x603284  |   pool_busycv+4   |    1            |    1366   |       1366         |
|2           | 0x6032c0     |   pool_mutex        |    7632          |  4745    |       36213840     |
|2           |    0x603300  |   pool_workcv       |    3766          |   1732   |       6522712      |
|2           |  0x603304    |   pool_workcv+4   |    329            |    5607   |     1844703      |
|2           |0x7f12a24c6320 |    N/A             |    33            |    10142   |     334686       |
|2           |    0x603344  |   pool_waitcv+4   |    1            |    7397   |       7397         |
|2           |  0x603284    |   pool_busycv+4   |    1            |    3792   |       3792         |
|3           | 0x6032c0     |   pool_mutex        |    18677          |  4129    |      77117333     |
|3           |    0x603300  |   pool_workcv       |    9691          |   1462   |       14177014      |
|3           |  0x603304    |   pool_workcv+4   |    17            |   6515   |       110755       |
|3           |0x7f12a24c6320 |    N/A             |    59            |    7829   |      461911       |
|3           |    0x603344  |   pool_waitcv+4   |    1            |    11966   |       11966         |
|3           |  0x603284    |   pool_busycv+4   |    1            |    10503   |       10503         |
|4           | 0x6032c0     |   pool_mutex        |    24672          |  5657    |      139569504     |
|4           |    0x603300  |   pool_workcv       |    7952          |   1444   |       11482688      |
|4           |  0x603304    |   pool_workcv+4   |    5            |   17019   |       85095       |
|4           |0x7f12a24c6320 |    N/A             |    59            |    12305   |      725995       |
|4           |    0x603344  |   pool_waitcv+4   |    1            |    10606   |       10606         |
|4           |  0x603284    |   pool_busycv+4   |    1            |    2393   |       2393         |

By observation from this table, we can see that with more cores, the total waiting time is increasing. For example, the lock with address 0x6032c0 whose variable name is pool_mutex, while we have 1 core, the average waiting time is 11632 and total waiting time is 7898128, with 2 cores, the average waiting time is 4745 and total waiting time is 36213840, with 3 cores, the average waiting time is 4129 and total waiting time is 77117333, and with 4 cores, the average waiting time is 5657 and total waiting time is 139569504, the average waiting time is decreasing but the total waiting time is increasing. And it is the same with lock whose address is 0x603304, and so on. In general, while the number of cores increases, the total waiting for each is increasing. My VMware doesn't allow me to set core to 8, but with this observation, with 8 cores, for example the pool_mutex will have much more total waiting time than 4 cores. I think the reason causeed this could be more cores will process each task faster, so the average wait time decreases, so it will more frequently contend locks which cause more contention times, so the total waiting time increases. 
