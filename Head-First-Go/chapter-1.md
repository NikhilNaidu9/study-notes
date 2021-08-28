#  Chapter 1 - let's get going: Syntax Basics

## Origin Story 
* In 2007, Google search engine had a problem. 
* They had to maintain programs with millions of lines of code.
* Before they could test any changes they had to compile the code into runnable form, a process which took about an hour.
* This was obviously very bad for developer productivity.
* So Google engineers Robert Griesemer, Rob Pike, and Ken Thompson decided some goals for a new language:
	1. Fast compilation
	1. Less cumbersome code
	1. Unused memory freed automatically ( garbage collection )
	1. Easy-to-write software that does several operation simultaneoulsy ( concurrency )
	1. Good support for processors with multiple cores
* After couple years of work, Google had created Go: a language that was fast to write code for and produced programs that were fast to compile and run.
* The project switched to open source license in 2009. 

## First Program
'''
package main

import "fmt"

func main() {
        fmt.Println("Hello, World")
}
'''
* Every Go file starts with a package clause.
* A package is a collection of code that does all the similar things, like formatting strings and drawing images.
* The package clause gives the name of the package that the file's code will become part of.
* In this case, we use the special package main, which is required if this code is going to run directly ( usually from terminal )
* Next, Go files almost always have one or more import statements. 
* Each file needs to import other packages before it code can use the code those other packages contain.
* Loading all the Go code on your computer at once would result in a big, slow program, so instead you specify only the packages you need by importing them.
* The last part of every Go file is the actual code which is often spilt up into one or more functions.
* A function is a group of one or more lines of code that you can call from other places in your program.
* When a Go program is run, it looks for the function named main and runs that first, which is why we named this function `main`.























