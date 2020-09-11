=========================
Lists and Arrays
=========================

In the previous section, we discussed working with variables that contained a single string/integer/number and how to check their type and convert them from one type to another.  While this was maybe interesting, real modern data is "`big <https://dilbert.com/strip/2012-07-29>`_", so we need to be able to deal with *collections* of data and not just one number at a time.  Thankfully, this is where Python has a native :py:class:`list` type and where we'll introduce the extremely useful `numpy <https://www.numpy.org>`_ array, (:py:class:`numpy.ndarray`) to handle many data points.

These data types are similar to those you just learned about except that now we have to worry about *where* our data is and not just *what* it is.  For example, if you have loaded into a variable the air temperature of Evanston, Illinois for the last 100 years, you might want to do an analysis of just the summer highs over time, so how do you access just those data points?  Alternately, you might be attempting to train a weather model, so you want to predict each time point based on the previous one in time, so how do you access elements in sequence?  These are the general techniques we'll explore in this section.  The next section on :doc:`loops </4_Loops/loops>` will teach you how to apply operations and functions iteratively and in sequences (as in our time-series hypothetical), and the following section on :doc:`conditional statements </5_ConditionalStatements/ifelse>` will give you the tools to select elements conditionally, so that you can only look at summer months, for example.  However, before we can use those techniques, we need to familiarize ourselves with the basics of lists and arrays in Python.

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

Lists have Length
-------------------

Lists can be Sorted
---------------------

Some Useful Lists
-------------------

Useful List Functions
-----------------------

Exercise 4.2
==============


