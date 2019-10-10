# GoGet test

The task is to create a very simple golang program which will demonstrate the use of channels, concurrency and the usage and importation of an external library in GO.
During your day to day work with GoGet you will be dealing with functions that pass and interact with data in a multithreaded setting.

To perform your task you will need to look up the following concepts:
* Structures in Go (Declaration, setting, accessing)
* Channels in go (Buffered and Unbuffered, sending and recieveing)
* For loops, range and Select statements
* Import packages and using functions from third parties
* Named functions and anonymous functions 
* Concurrency in Go. (GoRoutines)
* Pointers in Go. (Potentially)
* How to build and run your Go program. 

You will need the following installed: Go v1.13+, git

Disclaimer!: Don't stress so much over the completeness of this task. Its okay if something doesn't work so well, or arrives slightly out of order. This task is mostly to get you (the candidate) used to Go syntax and dealing with 
concurrency as this is what we will be doing in our daily work. 

This task is doable in a 1-2 hours if you manage to google up the basics and understand a bit of what is going on.

I suggest you READ the entirety of this document before starting the task ;)

# Deadline and submission

Please create a public git repo and link us to it. Send an email to kiril@gogetcorp.com
We expect that the program compiles and runs :)

You have a maximum of 3 days to submit this task.

If anything is unclear please do not hesitate to contact me: kiril@gogetcorp.com

# Task

Please submit a simple go program which will perform/has the following:

1. A GGevent structure should be declared holding a single member of type integer
* This is the type that we shall send into one of the channels
* The member inside the GGevent structure will be a counter, increasing with each iteration when processing GGevents

2. Write 2 functions one named and one anonymous
* There is no need for a return value as these two functions will only work on channels.
* You can choose any name you want for the first function
* The named function will accept 2 channels, A and B
* Channel A is responsible for holding GGevents
* Channel B is responsible for holding integers
* For every GGevent which comes into channel A increment the counter inside the structure
* When incrementing the counter and it is an even number, that number should be sent to Channel B

The anonymous function should take in 2 channels as parameters
* The first channel should process only integers, the second channel should process only errors
* For every error that we process (i.e recieve a value on the error channel), we should keep track of the number of times an error has occured as well as log it to the screen (stdout). If an error has occured more than 3 times. Exit the program with an error code of 1. 
* For every integer that has been recieved on the integer channel, simply log it to the screen (stdout)(you can use a logging package)

3. Error messages will be generated from a library package function that GoGet has open sourced. 
*You must use this in your code to produce the errors.*
See the following: https://github.com/GoGetCorp/gglib
* This package will need to be imported into your program
* You will need to call this function concurrently

All functions (the named and the anonymous one, and calling the function which produces errors) must be called concurrently.

A single GGEvent structure, with a counter initalized to 0 should be sent into the channel responsible for receiving GGevents. This will begin the chain of processing data for the named and the anonymous functions. :)

Expected number of files:
* 1 main.go file containing main + the task functions

# Task Output

The following is a sample output of how the task should work.
A successful task will exit with status code 1 due to the number of errors being generated from the library function we have provided.  

**Note that channels are EXTREMELY fast. The sample output includes a sleep `time.Sleep(1*time.second)` just after incrementing the counter in the named function). You can choose to add that or not. If you don't your output will probably be a number >4,000,000**

```Sample output
INFO[0002] Output from Process Events: 2                
INFO[0004] Output from Process Events: 4                
ERRO[0005] Annoying Error message, something went wrong 
INFO[0006] Output from Process Events: 6                
INFO[0008] Output from Process Events: 8                
ERRO[0010] Annoying Error message, something went wrong 
INFO[0010] Output from Process Events: 10               
INFO[0012] Output from Process Events: 12               
INFO[0014] Output from Process Events: 14               
ERRO[0015] Annoying Error message, something went wrong 
INFO[0016] Output from Process Events: 16               
INFO[0018] Output from Process Events: 18               
ERRO[0020] Annoying Error message, something went wrong 
exit status 1
```
# Potential issues
1. Your program might exit prematurely :) (you will have to do something about this)
2. Your program might have a deadlock (Readup on Channels!)

# Bonus
* A) If you are satisifed with the above task, a bonus is to include a make file capable of compiling and producing a binary for linux and a small README.md 
* B) If you have completed both the task and bonus A. Update your make file with the capability of producing a docker image that will run your binary on alpine linux.


# Useful resources
* Golang (tour of go) https://tour.golang.org/list  - Specifically the Flow Control, Structs and Concurrency
* General Googling :)
* https://github.com/GoGetCorp/gglib

# Hints
* You will probably need to use at least one Buffered channel.
* The source code of the gglib function is your friend :)
* Don't forget to send the incremented GGevent back into the GGevent channel after you have updated the structure 

Good luck!
