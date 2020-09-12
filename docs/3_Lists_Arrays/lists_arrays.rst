=========================
Lists and Arrays
=========================

In the previous section, we discussed working with variables that contained a single string/integer/number and how to check their type and convert them from one type to another.  While this was maybe interesting, real modern data is "`big <https://dilbert.com/strip/2012-07-29>`_", so we need to be able to deal with *collections* of data and not just one number at a time.  Thankfully, this is where Python has a native :py:class:`list` type and where we'll introduce the extremely useful `numpy <https://www.numpy.org>`_ array, (:py:class:`numpy.ndarray`) to handle many data points.

These data types are similar to those you just learned about except that now we have to worry about *where* our data is and not just *what* it is.  For example, if you have loaded into a variable the air temperature of Evanston, Illinois for the last 100 years, you might want to do an analysis of just the summer highs over time, so how do you access just those data points?  Alternately, you might be attempting to train a weather model, so you want to predict each time point based on the previous one in time, so how do you access elements in sequence?  These are the general techniques we'll explore in this section.  The upcoming section on :doc:`loops </4_Loops/loops>` will teach you how to apply operations and functions iteratively and in sequences (as in our time-series hypothetical), and the section on :doc:`conditional statements </5_ConditionalStatements/ifelse>` will give you the tools to select elements conditionally, so that you can only look at summer months, for example.  However, before we can use those techniques, we need to familiarize ourselves with the basics of lists and arrays in Python.

Please open a new Jupyter notebook and follow along by **copying** all Python commands!

*******************
Lists
*******************

The Python :py:class:`list` is one of the most flexible data structures in any programming language.  Most simply, a list operates as an **ordered** container of other variables, regardless of their type.  We'll see shortly that Python lists can be appended to, iterated over, and edited.  Their **elements**, or list entries, can be accessed with **indices**, and we'll see later that we can easily apply functions to all elements of a list with **list comprehensions**.  Simply put, if you only had Python lists to work with, you could probably get most computational tasks accomplished.

Most simply, we indicate a Python list using square brackets, ``[]``.  When entering a list manually, we separate elements with commas, as shown below.

.. code-block:: python
	:linenos:

	list1 = ['abcd', 1, 3.1415, False]
	print(list1)
	print(type(list1))

The above list contains a string, integer, float, and boolean data point in turn, but the variable ``list1`` is type :py:class:`list`.  

There isn't any restriction on what can be put in lists, so we're free to do things like:

.. code-block:: python
	:linenos:

	crazy_list = ['abcd', [12, 4, 'no'], ['yes', [True, 'unique element']], 'False', False]
	print(crazy_list)

	empty_list = []
	print(empty_list)

	all_lists = [list1, crazy_list, empty_list]
	print(all_lists)

That is, we can have nested lists inside of lists!

Accessing List Elements
=========================

Of course, creating lists is all great and good, but once we've collected data, we need to be able to pull it back out.  To do this we use **indices**, which are just integers that indicate which element of the list we'd like to access, where the first element of a list is indicated by a **0**, the second by a 1, the third by a 2, and so on.  Specifically, we put these indices again into a square bracket notation as shown below:

.. code-block:: python
	:linenos:

	animals = ['dogs', 'cats', 'birds']
	first_animal = animals[0]  ## This is the SYNTAX for the FIRST ELEMENT
	second_animal = animals[1] ## This is the SYNTAX for the SECOND ELEMENT
	print(animals)
	print(first_animal)
	print(second_animal)

.. sidebar:: Zero-Indexing

	Programming languages often either `start counting <https://en.wikipedia.org/wiki/Comparison_of_programming_languages_(array)>`_ at 0 or 1.  **Python starts at 0.**  This is just something to get used to compared to MATLAB and Fortran (1-indexed) or C and Perl (zero-indexed).

So we use the syntax ``list[index]`` to grab the ``index+1``th element from the list.  This applies regardless of what type the list element is, for example

.. code-block:: python
	:linenos:

	third_crazy_element = crazy_list[2]
	print(third_crazy_element)

	second_third_crazy_element = third_crazy_element[1]
	print(second_third_crazy_element)

	second_second_third_crazy_element = second_third_crazy_element[1]
	print(second_second_third_crazy_element)

	other_element = crazy_list[2][1][1]  ## What's happening here!?
	print(other_element)

Each of the elements was a list, so we could continue asking for indices.  (If I'd added another layer you could have asked for the `fifth element <https://www.imdb.com/title/tt0119116/>`_.)  The last line, which defines ``other_element`` shows how we can chain together index requests into nested lists.  This should not be super obvious, but as we'll continue, we'll see how Python commands can often be concatenated into one-liners like above.

There are then some caveats to this.  In Python, you cannot ask for an element at an index that does not exist.  Consider the following example:

.. code-block:: python

	tenth_animal = animals[9]  ## Index 9 is asking for the TENTH element

This should result in an ``IndexError: list index out of range`` because the index you asked for, 9, was beyond the range of this 3-element list.  (There is no 10th element to return!)

Lists are often flexible and we don't always know their length, so we can use the :py:func:`len` function to return the number of elements in a list.

.. code-block:: python
	:linenos:

	third_crazy_element = crazy_list[2]
	print(f"The length of the third element is {len(third_crazy_element)}")

	second_third_crazy_element = third_crazy_element[1]
	print(f"The length of the second-third element is {len(second_third_crazy_element)}")

	## Write down your prediction before running!
	# second_second_third_crazy_element = second_third_crazy_element[1]
	# print(f"The length of the second-second-third element is {len(second_second_third_crazy_element)}")

This also offers an easy way to access the last element in a list:

.. code-block:: python
	:linenos:

	longer_list = ['a', 'b', 'c', 'd', 'e', 1, 2, 3]

	len_list = len(longer_list)

	## Guess which one will work before uncommenting!
	# last_element = longer_list[len_list]
	# last_element = longer_list[len_list - 1]
	print(last_element)

However, Python also supports **negative indexing** where entering negative integers counts from the *end* of the list to the front.  

.. code-block:: python
	:linenos:

	last_el = longer_list[-1]
	second_to_last_el = longer_list[-2]

	print(last_el)
	print(second_to_last_el)

	print(longer_list[-20])  ## Does this work!?

Most importantly we can also access list elements via **slicing**; we can ask for a "slice" of the list using the ``list[start:end:increment]`` notation, which gives elements starting at index ``start``, up to **but not including** ``end``, in steps of size ``increment``.  For example, consider

.. code-block:: python

	print(longer_list[::2]) # This grabs every other element starting at 0
	print(longer_list[1::2]) # This grabs every other element starting at 1
	print(longer_list[0:6:3]) # Every third element starting at 0, ending at 6

This might seem confusing, or really simple, but having a strong grasp of indexing is *essential* to coding in Python, so please take the time to complete the following exercises:


Exercise 4.1
=========================

#. Make a list containing the integers 1 through 13 and the first 8 letters of the English alphabet.  Save into new variables the:
	#. First 5 elements of the list
	#. The last 12 elements of the list
	#. The odd-indexed elements of the list
	#. Every other even-indexed element of the list


#. Put the names of yourself and three friends into a list called ``names`` and put your corresponding favorite colors into ``colors``.  Confirm that these lists have the same length using the :py:func:`len` function and an appropriately formatted print statement.  Define a variable ``idx = 0`` and write a print statement that prints out you and your friends' names and corresponding favorite colors by accessing ``names[idx]`` and ``colors[idx]``.  Copy and paste this printing code four times and insert ``idx = idx + 1`` in between each print.  Can you describe each of you and your friends' favorite colors in turn?


#. Create several variables containing an integer, boolean, string, and list data type in turn.  Print the result of applying the :py:func:`list` function to them in turn.


#. Consider the following code and explain the output in the context of what you know about boolean variables.

	.. code-block:: python
		:linenos:

		print(bool([True]))
		print(bool(['True']))
		print(bool(['False']))
		print(bool([False]))
		print(bool([False, False, False]))
		print(bool([]))

Modifying Lists
=================

Now that you can access list elements, it's important to note that lists are `mutable <https://medium.com/@meghamohan/mutable-and-immutable-side-of-python-c2145cf72747#>`_ data types in that they can be changed (mutated).  That is, once we've defined a variable as a list, we can come back, after the fact, and edit the elements, size, and structure of the list.  This is not always the case with data structures, so it's worth point out.  There are many ways to modify lists in Python, and I'll point out the most useful here.

Modifying Elements
--------------------

Consider our earlier ``crazy_list``.  We can always change any specific element by directing an assignment operation at it.  For example:

.. code-block:: python
	:linenos:
	
	print(crazy_list)
	best_list_element = crazy_list[2]
	print(best_list_element)
	crazy_list[2] = 4
	print(crazy_list)
	print(crazy_list[2])

We see that we've changed the 3rd element of crazy list from ``best_list_element = ['yes', [True, 'unique element']]`` to ``4``.

Adding Elements
-----------------

Elements can be added to lists in several ways.  First of all, we can concatenate lists with the ``+`` operation:

.. code-block:: python
	:linenos:

	some_animals = ['dog', 'cat', 'gerbil']
	other_animals = ['iguana', 'flying squirrel', 'parakeet']
	print(some_animals)
	print(other_animals)

	many_animals = some_animals + other_animals
	print(many_animals)

But we can also use the :py:func:`list.append` and :py:func:`list.insert` methods to add elements to either the end or a specific index of a list, respectively.

.. code_block:: python
	:linenos:

	many_animals.append('chinchilla')
	print(many_animals)

	many_animals.insert(2, 'turtle')
	print(many_animals)

	many_animals.insert(2, 'tortoise')
	print(many_animals)

Additionally, we can multiply lists using the ``*`` operator as with strings.  Try ``print(4*many_animals)`` and ``print(24*[True, 0])`` and see what happens!

Removing Elements
-------------------

Similarly, we can remove elements from either the end or a specific index of a list using :py:func:`list.pop`.

.. code_block:: python
	:linenos:
	
	last_animal = many_animals.pop()
	print(last_animal)
	print(many_animals)

	middle_animal = many_animals.pop(3)
	print(middle_animal)
	print(many_animals)

Notice that the :py:func:`list.pop` function can save the removed value into a variable.  This can be useful if you need to iterate through a list and use each element for something one time.

You can also use the :py:func:`list.remove` function to remove elements *by value*.  That is, we can remove the *first* instance of a specific value with :py:func:`list.remove`.

.. code-block:: python
	:linenos:
	
	many_animals.insert(2, 'turtle')
	many_animals.insert(-1, 'turtle')
	many_animals.insert(0, 'turtle')

	print(many_animals)

	many_animals.remove('turtle')
	print(many_animals)
	many_animals.remove('turtle')
	print(many_animals)
	many_animals.remove('turtle')
	print(many_animals)

Copying Lists
---------------

In previous examples we have done things like ``x = y`` to copy values to multiple variables with impunity.  Unfortunately we can't continue this with lists.  To see why, consider the following:

.. code-block:: python
	:linenos:

	print(many_animals)
	copied_list = many_animals

	copied_list[4] = 'tiger'
	print(copied_list)
	print(many_animals)  ## This list has a tiger in it now!

We can see that the ``copied_list`` wasn't just a copy because modifying it also changed the original list, ``many_animals``.  This is because in Python, variables don't actually *contain* the data we've assigned them to, instead they *point* to that data in the computer's storage.  So when we type ``copied_list = many_animals``, we're just telling Python that *both* ``copied_list`` and ``many_animals`` should direct to the same data in storage.

This may seem like an odd point to make, but this is an insidious problem to encounter because it will raise no error messages, but data that you don't expect to change might be modified if you don't copy lists correctly.  The easiest way to truly create a *new* copy of data is to use the ``copy = old[:]`` syntax, where the ``[:]`` simply says "create a slice of everything," which Python dutifully places in an actually new list (a new part of your computer's storage is allocated).

Other List Information
========================

There are several other useful things you can do with lists that we'll discuss below.  You should not worry about memorizing these, just try to keep in mind that these sort of things can be done with lists.

The :py:func:`list` Function
------------------------------

Just as we saw with :doc:`other data types </2_Variables_DataTypes/vars_types>`, we can attempt to convert variables into a list with the :py:func:`list` function.  For some data types, this will simply add a pair of square brackets around your data, but for other data types that you'll eventually learn about, such as arrays, this type conversion can be more signficant.  In particular, Python thinks of lists as *collections* of stuff so for some data types that can't really be thought of that way, like a single integer or float, :py:func:`list` will throw a ``TypeError`` as you'll see below.  Try out the code below to see how this works.

.. code-block:: python
	:linenos:

	my_str = "the quick brown fox"
	my_int = 6543
	my_float = 65.43
	my_bool = True or False

	print(list(my_str))  ## What happened here!?
	## What errors do these lines create?
	# print(list(my_int))  
	# print(list(my_float))
	# print(list(my_bool))

	## What about this?
	# print([my_int])
	# print(type([my_int]))
	# print(list([my_int]))
	# print(type(list([my_int])))

Lists have Length
-------------------

We've already mentioned this, but it can be very useful to know how many elements are in your lists.  This is done via the :py:func:`len` like this:

.. code-block:: python

	my_list = ['a', 1234, 'list_element', True, True, 4+6]
	list_len = len(my_list)
	print(f"There are {list_len} elements in 'my_list'")

We can see that the :py:func:`len` function returns the number of elements in a list.  This may seem simple, but it can be very useful in many contexts.

We'll see that this output is always a non-negative integer, where we can get a length of 0 by asking for the length of an `empty list <https://stackoverflow.com/questions/2972212/creating-an-empty-list-in-python>`_ like so:

.. code-block:: python

	empty_list = []  ## Square brackets with nothing in between!
	print("This is an empty list:", empty_list)

	zero_length = len(empty_list)
	print(f"The length of the empty list is {zero_length}")

We'll use this frequently in the :doc:`section on loops </4_Loops/loops>` to *intialize* code that will be repeated many times, using the :py:func:`list.append` function, for example, to fill the list with useful calculations.

The Range Function
--------------------

We'll talk in a moment about a bunch of useful list functions, but the :py:func:`range` function is too useful to not highlight specifically.  The ``range`` function can be used to make collections of integers to cover a specific range (hence the name).  We can use the :py:func:`list` type conversion function to return a list of these numbers.  Try out the example below and use ``help(range)`` to read the documentation.

.. code-block:: python
	:linenos:

	start, stop, step = 0, 10, 2
	my_range1 = range(start, stop, step)
	print(my_range1)
	print(type(my_range1))  ## What type does 'my_range1' appear to be?

	## Apply the list() function:
	my_range1 = list(my_range1)  
	print(my_range1)
	print(type(my_range1))

	## If we don't supply a step size, it increments by 1
	print(list(range(start, stop)))

	## If we don't supply a starting point, it assumes 0
	print(list(range(stop)))

	## We can use negative step sizes
	print(list(range(stop, start, -step)))

	## Is 'stop'=10 in this list?
	print(list(range(10)))

	## What happens if we try to use a float?
	# print(list(range(10.1)))

Note that range only works for integers and that the ``stop`` input is *excluded* from the range.

This function will again be extremely useful in the :doc:`section on loops </4_Loops/loops>`, but having a way to get a regularly spaced range of numbers is something that could be handy in a variety of circumstances.


Useful List Functions
-----------------------

As a final note, I just want to highlight a few really useful list functions.

If we have a list of all "numbers", then the :py:func:`sum`, :py:func:`max`, and :py:func:`min` functions can be very useful!  

.. code-block:: python

	num_list = list([3, 6.3, 8, 12.52, 4, 4, 3, True, 3, 0.1])
	list_max = max(num_list)
	list_min = min(num_list)
	list_sum = sum(num_list)

	print(f"The max of 'num_list' is {list_max}")
	print(f"The min of 'num_list' is {list_min}")
	print(f"The sum of 'num_list' is {list_sum}")

We can *sort* lists using the :py:func:`sorted` function or the :py:func:`list.sort` method.  The difference between these is that :py:func:`sorted` returns a *copy* of the list that is now sorted, while :py:func:`list.sort` will sort the list **in-place**.  This is somewhat important, because if the order of your original list is important, then you don't want to mess that up with a :py:func:`list.sort`.

.. code-block:: python
	:linenos:

	orig_names = ['Eric', 'Madhav', 'Bill', 'Caroline', 'Tiffany']
	names_to_sort = orig_names[:]

	sorted_names = sorted(names_to_sort)
	print(names_to_sort)
	print(sorted_names)

	names_to_sort.sort()
	print(names_to_sort)

	## We can reverse the sort order with the "reverse" keyword:
	sorted_names = sorted(names_to_sort, reverse=True)
	names_to_sort.sort(reverse=True)
	print(sorted_names)
	print(names_to_sort)

We can *count* the number of times a certain element appears in a list with the :py:func:`list.count` method.  Using the ``num_list`` from the earlier example, we can see:

.. code-block:: python
	:linenos:

	num_3 = num_list.count(3)
	num_4 = num_list.count(4)
	num_8 = num_list.count(8)
	print(f"There are {num_3} 3s in 'num_list'")
	print(f"There are {num_4} 4s in 'num_list'")
	print(f"There are {num_8} 8s in 'num_list'")

Finally, we can check if an element exists in a list using the ``in`` operation.  If an element exists in the list, we can find the **index** of *the first instance* of it using the :py:func:`list.index` function.

.. code-block:: python
	:linenos:

	print(3 in num_list)
	print(5 in num_list)

	idx_3 = num_list.index(3)
	idx_5 = num_list.index(5)  ## What is the error message here?

	print(f"There is a 3 in 'num_list' at index {idx_3}")

If this is your first time working with lists, don't worry about trying to memorize everything you've seen here.  Coding is a *skill* and you will remember things that you use more frequently and look up things that you don't.  I have been coding in Python for years and I constantly look up functions or syntaxes.  These notes on lists have thus been given to you as a reference and to show you the things that you *could do* with a Python list, which you *should* try and remember.  That is, you should know that there's a function for sorting lists, but it's ok if you don't remember the exact syntax off the top of your head.  For a good reference on list methods, see `python.org <https://docs.python.org/3/tutorial/datastructures.html>`_.

Exercise 4.2
==============

#. Create a nested list using your ``names`` list from exericise 4.1.2 by placing ``names`` in between two square brackets.  Save this list to a variable ``names_colors``.  
	#. What is the length of this list?  What is the length of ``names_colors[0]``? 
	#. Undo the extra bracketing with ``names_colors = names_colors[0]``.  Set ``idx=0`` and use ``idx`` as an index to replace each element of ``names_colors`` with a list ``[names[idx], colors[idx]]`` (where ``colors`` is the same list from 4.1.2).  You should now have a list of lists, where each sub-list has a name and a color.
	#. You've had a falling out and need to remove the last friend from ``names_colors``.  However, at the same time, you've made two new friends!  Add one of them (and their favorite color) right after your name+color using :py:func:`list.insert`.  Add the other friend to the end of ``names_colors`` using :py:func:`list.append`.
	#. Use :py:func:`sorted` to sort ``names_colors``.  How did it sort the list?  Execute the following code and try to explain what happened differently.

	.. code-block:: python
		sorted_friends = sorted(names_colors, key = lambda x: x[1])

#. Create a list containing 10 numbers of your choice.  Use the :py:func:`sum` and :py:func:`len` functions to calculate the average of the list elements.  Print this result to the screen in a formatted string.

#. Let's practice using the :py:func:`range` function:
	#. Create a list of all the integers from -12 to 8.
	#. Create a list containing the first 10,000 even integers.
	#. Create a list of the first 5 positive integers that are divisible by 7 as ``list_of_sevens``.  Use ``idx = list(range(len(list_of_sevens)))`` to make a list of indices for the elements in ``list_of_sevens``.  Use ``ii = idx.pop()`` and ``list_of_sevens[ii]`` several times to print out the elements in reverse order in a formatted string.

#. Consider the `problem here <http://rosalind.info/problems/dna/>`_. Save the sample DNA as a string and use string formatting to print the number of A's, C's, G's and T's to the screen.

#. Convert a string containing a DNA sequence into the corresponding RNA, as indicated `here <http://rosalind.info/problems/rna/>`_.  This process involves replacing all T's in the DNA with U's.  As a hint, consider using :py:func:`list.index` or :py:func:`list.replace`.

*******************
Numpy Arrays
*******************

Hopefully the first part of this section has convinced you that Python lists might be useful and flexible tools for holding multiple data points.  However, Python lists are sometimes *too flexible*, in allowing for the collection of arbitrary data, they lose some potentially useful functionality.  In particular, applying operations to each element in a list requires that we access each list element individually (which you will still do in the :doc:`section on loops </4_Loops/loops>`), which can quickly become very slow!  To fill the need for a slightly more structured collection of data, the `numpy <https://numpy.org/>`_ package was developed as "The fundamental package for scientific computing in Python."  Going forward as a data scientist, familiarity with numpy will be essential.  

Here we'll introduce you to the :py:class:`numpy.ndarray`, which is the data structure we're looking for.  We'll see that this structure, informally known as a numpy **array**, trades some of the list's flexibility for functionality and speed.  But before we talk about working with numpy, let's spend a moment talking about Python **packages**.

Importing Packages in Python
==============================

In the :doc:`Introduction </1_Introduction/introduction>`, I noted that Python has a large, active online community of developers.  What this means is that **packages** (also called **modules**) of Python code are constantly being created and disseminated for all sorts of applications.  This is facilitated by the Python programming language via the powerful :py:func:`import` operation that let's a programmer "import" the contents of any other package on their computer into a Python code to be used.  That is, if you write a couple tools for doing some useful data analysis, you can send them to me (or put them on the internet!) and I can use :py:func:`import` to give my code access to your tools.  This may sound somewhat complicated or abstract, and it can be, which is why environments like Anaconda can be especially useful.

In particular, advanced projects may involve building on dozens of other people's code in many packages.  It could quickly become tedious to download and manage new packages.  To assist with this, Python installs generally include the :py:class:`pip` function, or the Anaconda Navigator has the `environments <https://docs.anaconda.com/anaconda/navigator/overview/#environments-tab>`_ tab.  As a bonus, Anaconda also includes common packages, such as numpy and matplotlib, pre-installed.  However, to install a new package using Anaconda, you can search for the package in the environments tab.  If you are not using Anaconda, follow the instructions `here <https://packaging.python.org/tutorials/installing-packages/>`_, typically the important command will be ``pip install my_package``.  Again, this is mostly for your reference later on, anyone using Anaconda will not have to worry about the next step.  

The important information on importing packages is then how to use the :py:class:`import` functionality in your code.  Typically what this looks like is
the line ``import numpy as np`` near the top of your code.  In a Jupyter notebook, put this in the first cell in the notebook and run it, so that all cells have access to the package.  What this command tells Python  is that you are importing the numpy package, and you're calling it ``np``, so that numpy functions can be accessed as ``np.function_I_want``.  

There are several options for the import statement.  For example, you can import all functions without the nickname using ``from numpy import *``, where ``*`` is a `wildcard character <https://en.wikipedia.org/wiki/Wildcard_character>`_ so that Python reads "from the numpy package, import everything matching \*", but the \* matches everything, so it imports all the numpy functions.  This is not usually recommended, as you are not guaranteed that a package won't have a function with the same name as something you already have.  So, if numpy also has a ``print`` function, Python wouldn't know whether to use the built-in ``print`` or numpy's.  This is cleared up by insisting that the functions be prepended with something, so there's no ambiguity between ``np.print`` and ``print``.  Also, ``import numpy`` imports numpy functions that can now be accessed with ``numpy.function``, the ``as np`` just makes things easier to type.

You can also import specific functions or sub-modules from a package using the ``from package import func1, func2`` syntax.  This is useful when you know you're only going to be using a few things from the package.

.. admonition:: TLDR: importing packages

	Going forward, we'll often use ``import numpy as np`` to tell Python we want to access numpy functions.  Throughout the rest of the tutorial, if you see ``np.function``, it is *assuming* that you have imported numpy at the beginning of your code.

Numpy Arrays
==============

As promised, we will now introduce the :py:class:`numpy.ndarray`, or the numpy (N-dimensional) array.  Most simply, an array operates like a matrix that you may know from math class, or like an Excel spreadsheet.  Elements are laid in a grid so that each element can be identified by its row and column.  The caveat is that arrays can *only contain one data type*, unlike lists.

To make an array, we can apply the :py:func:`np.array` function to a list.  We can also use the :py:func:`np.empty` function to make an "empty" array of a given size or the :py:func:`np.zeros` and :py:func:`np.ones` functions to make arrays of zeros or ones, respectively.

.. code-block:: python
	:linenos:

	num_list = list([3, 6.3, 8, 12.52, 4, 4, 3, True, 3, 0.1])
	num_arr = np.array(num_list)
	print(num_arr)
	print(type(num_arr))
	print(num_arr.dtype)

	n_rows, n_cols = 5, 3
	empty_arr = np.empty((n_rows, n_cols)) ## SYNTAX ALERT NOTE THE DOUBLE
										   ## PARENTHESES
	zero_arr = np.zeros((n_rows, n_cols))
	one_arr = np.ones((n_rows, n_cols))

	print(f"\nArrays of size {n_rows} x {n_cols}")
	print("\nAn empty array:")
	print(empty_arr)
	print("\nAn zero array:")
	print(zero_arr)
	print("\nAn one array:")
	print(one_arr)

In these examples, you can see that converting a list of mixed types (``num_list`` has ints, floats, and booleans) coerced everything into one type in ``num_arr`` (floats, in this case).  You can check the **datatype** using the :py:attr:`numpy.ndarray.dtype` **attribute**.  We haven't talked about attributes yet, but you can think of them as properties of a piece of data.

You should also see that the :py:func:`np.empty`, :py:func:`np.zeros`, and :py:func:`np.ones` functions all made 5 by 3 arrays.  The important note is that the input to these functions is a `tuple <https://docs.python.org/3.3/library/stdtypes.html#tuples>`_ of the dimension sizes.  Tuples are another data type that we won't spend time on that are indicated like a list, with elements separated by commas, but using parentheses, ``()``, instead of square brackets.

As a final note, you can see that the ``empty_arr`` is definitely not empty!  This is because what it tells Python to do is to just set aside some space in the storage for the array data to be placed.  Since your computer generally doesn't actually "delete" things by setting all the bits to zero, when you ask Python what's in the empty array, it looks at the bits that have been allocated, and interprets them according to ``dtype`` (float in this case).  So this part of memory could have previously been some file I'd written, but when interpreted as an array of floats, looks like some weird numbers.  As a result, this function, while ostensibly faster than :py:func:`np.zeros` or :py:func:`np.ones`, can be more dangerous because it's harder to detect what is real data vs uninitialized elements.

Array Size, Dimension, and Type
---------------------------------

Keeping track of your arrays is essential in more complicated programs.  To do this, it is often useful to check that the arrays you are creating are the correct shape, dimension, and type.  To check these, you can use the :py:attr:`shape`, :py:attr:`ndim`, and :py:attr:`dtype` attributes.

.. code-block:: python
	:linenos:

	n_rows, n_cols = 5, 3
	zero_arr = np.zeros((n_rows, n_cols))
	arr_shape = zero_arr.shape
	arr_ndim = zero_arr.ndim
	arr_datatype = zero_arr.dtype

	print(f"The shape of 'zero_arr' is {arr_shape}")
	print(f"The number of dimensions of 'zero_arr' is {arr_ndim}")
	print(f"The type of data in 'zero_arr' is {arr_datatype}")

Note that the :py:attr:`shape` attribute returns a tuple, so that we can use it to create similarly sized arrays.  We can access tuple elements using normal list indexing (``tuple[index]``) and we can use the :py:func:`numpy.empty_like`, :py:func:`numpy.zeros_like`, :py:func:`numpy.ones_like` functions to create empty, zero-filled, and one-filled arrays of the same size as an input array, respectively.

.. code-block:: python
	:linenos:

	more_cols = np.zeros((arr_shape[0], 10))
	print(more_cols)

	fewer_rows = np.ones((2, arr_shape[1]))
	print(fewer_rows)

	same_but_ones = np.ones_like(zero_arr)
	print(same_but_ones)

Accessing Array Elements
--------------------------

As noted just above, accessing tuple elements uses the same syntax as for listsA: ``my_tuple[index_I_want]``.  The same syntax holds for arrays, except now we have multiple dimensions whose indices we need to specify.  The syntax for array indexing is ``my_arr[index1, index2, index3]``  where each subsequent index corresponds to each subsequent dimension of the array: the first index indicates the row, the second the column, the third the "sheet", etc.  We can use the slicing operations above on any dimension, using different slices in different dimensions to grab different sections of the array.

.. code-block:: python
	:linenos:

	big_arr = big_arr = np.array(2 * (list('abcdefghijklmnopqrstuvwxyz') + ['aa', 'bb'])).reshape(8, 8)

	print(big_arr)

	print(f"The shape of 'big_arr' is {big_arr.shape}")
	print(f"The number of dimensions of 'big_arr' is {big_arr.ndim}")
	print(f"The type of data in 'big_arr' is {big_arr.dtype}\n")

	first_row = big_arr[0]
	first_col = big_arr[:, 0]

	print("The first row is:", first_row)
	print("The first column is:", first_col)

	subset1 = big_arr[1:3, 2:6]
	subset2 = big_arr[-3:, :5]
	print("\n'subset1' is:")
	print(subset1)
	print(f"The shape of 'subset1' is {subset1.shape}")
	print("'subset2' is:")
	print(subset2)
	print(f"The shape of 'subset2' is {subset2.shape}")

We can also access array elements via **masking** which we'll talk more about in the :doc:`section on conditional statements </5_ConditionalStatements/ifelse>` and by providing lists or arrays of indices directly.  For example, if we want to access the first and third rows of a list directly, we can use ``my_arr[[0, 2]]``.

Useful Array Functions
------------------------

As you may have seen in the previous example, we can use the :py:func:`numpy.reshape` function to change the size of an array.  So if we use the :py:func:`range` function to make a list of numbers, we can do ``np.array(range(20)).reshape(4, 5)`` to make a 4x5 array.

.. code-block:: python
	:linenos:

	reshaped_arr = np.array(range(20)).reshape(4, 5)
	print(reshaped_arr)

Perhaps the most useful thing that we can do with arrays is **vectorize** our code by applying operations **element-wise**.  For example,

.. code-block:: python
	:linenos:

	added_arr = reshaped_arr + 3.4
	minus_arr = added_arr - reshaped_arr
	mult_arr = (4 * reshaped_arr / 5.345)**2.3

	print(added_arr, "\n")
	print(minus_arr, "\n")
	print(mult_arr)

If we have row or column arrays that match the size of another array, Python will assume that we want to do the operations row-wise or column-wise.  This is known as `broadcasting <https://numpy.org/doc/stable/user/basics.broadcasting.html>`_.

.. code-block:: python
	:linenos:

	row_arr = np.arange(5)
	col_arr = np.arange(4).reshape(-1, 1)  ## WHAT DOES THE -1 DO HERE?
										   ## (check the shape!)
										   ## (try removing the reshape)
	print("\n'reshaped_array':")
	print(reshaped_arr)
	print("\n'row_arr':")
	print(row_arr)
	print("\n'col_arr':")
	print(col_arr)

	row_added = reshaped_arr + row_arr
	col_added = reshaped_arr + col_arr

	print("\nAdding a row array:")
	print(row_added)
	print("\nAdding a column array:")
	print(col_added)

Generally, arrays have pre-set sizes, but the :py:func:`numpy.concatenate`, :py:func:`numpy.hstack`, :py:func:`numpy.vstack` functions can be used to combine arrays (if their shapes match!).  The :py:func:`numpy.concatenate` function will assume that you want to use the last dimension for concatenating, :py:func:`numpy.hstack` assumes you want to concatenate along rows, and :py:func:`numpy.vstack` assumes columns.

Alongside the :py:func:`numpy.ndarray.reshape` function, the :py:func:`numpy.ndarray.squeeze` function "squeezes" the array to get rid of extra dimensions.

We also can still use :py:func:`sum`, :py:func:`min`, and :py:func:`max`, but now we also can use the numpy versions :py:func:`numpy.sum`, :py:func:`numpy.min`, and :py:func:`numpy.max` which allow for the specification along which dimension (or **axis**) that we want to perform the operation:

.. code-block:: python

	arr_mean = np.mean(reshaped_arr)
	row_mean = np.mean(reshaped_arr, axis=1)
	col_mean = np.mean(reshaped_arr, axis=0)
	print(f"The mean of 'reshaped_arr' is {arr_mean}")
	print(f"The row-wise mean of 'reshaped_arr' is {row_mean}")
	print(f"The column-wise mean of 'reshaped_arr' is {col_mean}")

The numpy package also has a `host of functions <https://numpy.org/doc/stable/reference/routines.html>`_ for scientific and numeric purposes.  The `mathematical functions <https://numpy.org/doc/stable/reference/routines.math.html>`_ in particular are especially useful, including :py:func:`numpy.mean`, :py:func:`numpy.exp`, :py:func:`numpy.log`, and :py:func:`numpy.round`.  You can use :py:func:`numpy.info` to access detailed numpy documentation.  If you ever want a basic math operation in Python, Google "python numpy my_operation" first!

Exercise 4.3
===============

#. The numpy analog to :py:func:`range` is :py:func:`numpy.arange`.  Use it to make an array of integers from -50 to 50.  Divide by 25 to make an array of 101 equally spaced numbers from -2 to 2.

#. Use :py:func:`numpy.info` to look up how the :py:func:`numpy.linspace` function works.  Use it to make an array of 101 numbers between -2 and 2 named ``my_grid``.

#. Create an array of indices for ``my_grid`` (using ``arange``??).  Add this array of indices to ``my_grid``.

#. Create a new array omitting the last element using slicing.  Name this array ``my_grid2``.  What is ``len(my_grid2)``?  Reshape ``my_grid2`` into a 10x10 array named ``my_arr``. What is ``len(my_arr)``?  How does it seem that ``len`` works?  Try reshaping into a 25x4 array or a 4x25 array as a hint!

#. Create a new array ``y_values`` from ``my_grid3 = np.linspace(-2, 2, 100)`` using the function :math:`y = \frac{6}{5}x^{-2} + x - 3.4`.  (:math:`y` is ``y_values`` and ``my_grid3`` is :math:`x`.)  What are the maximum and minimum values of ``y_values``?  Use the :py:func:`numpy.argmin` and :py:func:`numpy.argmax` functions to find *where* (the index location) of these maximum and minimum values - save them as ``max_idx`` and ``min_idx``.  Use ``max_idx`` and ``min_idx`` to show the values of ``my_grid3`` at which the min and max occur!

#. Apply :py:func:`numpy.unique` to the list ``num_list`` from earlier in the section.  What does it seem to do?






