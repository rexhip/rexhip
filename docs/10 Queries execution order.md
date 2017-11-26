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
Each station block has there own internal loop of execution, when all queries has been executed the loop will start over again. If one SB has 5 queries while another has 15, then the first query will have its queries executed three times as fast as the second one.

5
-
By default only one query in each station block is executed for each loop. A bus is shared resource, and a device shouldn't be allowed to occupy the bus for long periods of time. However this cycle can be changed if some devices need more priority then otheres. By changing the variable «#s.conf.exec_n_quries» in the station block, setting this variable to three for example, will let this one station block execute three queries for each loop, while other station blocks only execute one query on the same loop.

6
-
If a device encounter sveral timeout, then the communication-error-flag will be set for the station block, and queries will be executed less frequently. This make the trafic on the flow more effectively, by avoiding waiting for timeouts.

7
-
If more then one device have communication problems, then only one of them is allowed to make retry for each loop. The devices with error_comm-flag set will altnerative witch one will do a retry on the query loop.

8
-
Each SB has a disable flag, if it's set the queries inside the SB will be skipped, when it's the SB's turn to execute a query. The execution will continue in the next SB.

9
-
Each SB has a disable flag, if it's set the queries inside the SB will be skipped, when it's the SB's turn to execute a query. The execution will continue in the next SB.

10
-
Each SB has a read_only flag. If this flag is set and the SB contains write query. Then each time this write-query is going to be executed, the library whill skip the query, and let the following SB, execute a query instead. No query in the current SB will be executed at that loop. On the next loop the query after the write-query will be executed.

11
-
...

----------------------------------

This are the main rule of execution in the library, and all the rules apply at the same time. As mention on the top, the developer should need to worry about the order she or he just need to know that they all will be executed, regardsless in which order.

