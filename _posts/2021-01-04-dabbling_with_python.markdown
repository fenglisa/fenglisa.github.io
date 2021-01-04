---
layout: post
title:      "Dabbling with Python"
date:       2021-01-04 15:34:28 -0500
permalink:  dabbling_with_python
---


Recently, I was presented with a coding exercise that required me to write a function that takes in a list of integers and *n* as arguments and removes the integers that appear at least *n* times from the given list. The list would contain no more than 99 integers, the order of the integers should not be changed, and the duplicates as well as the first occurence of the integer should be removed (for example: given [10, 15, 5, 10] and 2, the solution should output [15, 5]). We were allowed to implement the solution in either Java or Python, neither of which, at the time, I had learned. 

The first thing I had to familiarize myself with was what kind of collection data types Python had. Turns out, Python has four collection types:
* **List** - a collection which is ordered and changeable. Allows duplicate members.
* **Tuple** - a collection which is ordered and unchangeable. Allows duplicate members.
* **Set** - a collection which is unordered and unindexed. No duplicate members.
* **Dictionary** - a collection which is unordered and changeable. No duplicate members.

[(source)](https://www.w3schools.com/python/python_lists.asp)

From my Ruby and JavaScript background, I was familiar with arrays and a Python list sounded a lot like an array. Now I had to figure out how to iterate over and change a list. 
To loop through a list, Python has a for statement:
```
thislist = ["apple", "banana", "cherry"]
for x in thislist:
  print(x)
```
[(source)](https://www.w3schools.com/python/python_lists_loop.asp)

This would print each element (or "x") in the list. We could easily call a `remove()`method instead of the `print()` statement to change `thislist`.

Next I had to determine how many times each integer occured in the list. Luckily, Python has a `count()` method that returns exactly that. Combining the for statement with an if statement inside, I could set up a condition for making a new list.
```
thislist = ["apple", "banana", "cherry", "apple"]
newlist = []

for x in thislist:
  if thislist.count(x) < 2:
    newlist.append(x)
		
print(newlist)
```
This would print `['banana', 'cherry']`.

Personally, I'm a fan of one-liner code (`ternary operator > if statement ? high-five : disappointment`) so naturally I was drawn to Python's [list comprehension](https://www.w3schools.com/python/python_lists_comprehension.asp).
With list comprehension, the code above would look like this:

```
thislist = ["apple", "banana", "cherry", "apple"]
newlist = []
newlist = [x for x in thislist if thislist.count(x) < 2]

print(newlist)
```
This would also print `['banana', 'cherry']`.

I was able to provide a solution using these methods that admittedly is not very scalable, but with the given parameters, adequate. Documenting my introduction to Python has also surprisingly furthered my curiosity of it and I intend to take a more comprehensive "dip" into the language. 


