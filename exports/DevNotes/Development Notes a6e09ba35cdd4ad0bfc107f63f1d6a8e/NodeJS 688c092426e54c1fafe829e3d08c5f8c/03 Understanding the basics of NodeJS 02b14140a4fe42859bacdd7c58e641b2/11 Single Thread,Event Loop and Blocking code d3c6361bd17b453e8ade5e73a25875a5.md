# 11.Single Thread,Event Loop and Blocking code

Our NodeJS scripts are by default designed to run in a single thread, so to perform operations such as file I/O operations we send those tasks to a seperate pool of threads called the worker threads which do all the heavy lifting, while the event loops only handle fast taks like callbacks, once the task in the worker pool ends, it triggers a callback and the event loop handles it again,This is done automatically by the system 

![Untitled](11%20Single%20Thread,Event%20Loop%20and%20Blocking%20code%20d3c6361bd17b453e8ade5e73a25875a5/Untitled.png)

# The Event Loop

The order of execution of events by the event loop is as follows 

![Untitled](11%20Single%20Thread,Event%20Loop%20and%20Blocking%20code%20d3c6361bd17b453e8ade5e73a25875a5/Untitled%201.png)

First it checks for any timers to execute, then any pending callbacks such as I/O operations .

Secondly, it polls and checks if any new I/O events are to be executed and executes their callbacks (i.e it jumps back to pending callbacks or Timers). 

Then it executes `setImmediate()` callbacks, and after this `close()` callbacks. 

If there are no pending event listeneres i.e `refs==0` and a process.exit() is called, the event loop will terminate