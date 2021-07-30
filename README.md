# COMP 3430 lab 3

## Chen Dong, 7792042

# Screenshots for this lab

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

# Question 4
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
