Execution order of the queries
--------------------------------

In general the user of the library should not need to worry about the execution order, however for curious user, bellow is a is a brif overview on how it works. There are many if's and but's, about the order, each step bellow explains more complexity. 

1
-
If the there is no mb_station_header and mb_station_footer, no if-statements, then the execution is linear. The 1st query execute first, then the 2nd, and so on. After the last query the proccess will start over.

2
-
If one or more queries are surrounded by a if-statement, then order of execution may change. The reason for this is becouse query-id the queries occupies, will be given to other queries when the if-statment change state. There is however no change that a resualt from query should end in a other query.    

3
-
With the mb_station_header, and mb_station_footer the complexity increase quite a lot. This FC's are not require, but they include many Useful functionality, by manupulate mb_query. The first query in the first station block will be executed, then first query in the secound station block will be introduced and so on. When all the first queries has been executeded, then the secound query in all station block will be executed, starting with the first station block. Section 2, can still interfer this execution order. 

4
-
If a device encounter sveral timeout, then the communication-error-flag will be set for the station block, and queries will be executed less frequently.

5
-
...
