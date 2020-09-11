=========================
Data in Python
=========================

Now that you've entered your :doc:`first Python commands </1_Introduction/helloworld>` you're completely prepared to do practical things in Python!  `Open a new notebook <https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/execute.html>`_ and follow along.  Again, as a reminder, coding is a *creative* process so make sure to **type everything** that you see on this page!  (If not more!)

In this section of the tutorial, we're going to talk about how we can use **variables** in our code as containers to hold data.  We'll then talk about the different kinds, or **types**, of data that Python can work with and how the type of data that a variable holds determines what we can do with it.  We'll then discuss many of the useful and interesting things that you can do with Python's basic data types.

*************************
Variables in Python
*************************

We noted in the :doc:`previous section </1_Introduction/helloworld>` that Python can act most trivially as a calculator.  Of course, if this were all that Python could do, it would not be a very useful language!  Instead, the way that Python and most other programming languages move beyond simple operations is via the use of **variables**, which allow us to store and manipulate data more abstractly.

These variables operate very similar to the variables you may know from algebra: they are symbols that stand for a specific piece of data, and they can be manipulated abstractly (ignoring the specific values of the data) or evaluated explicitly (plugging in the data values).  Thinking of variables as analogous to those in math class can be useful.

In Python, we **assign** data to a variable using the assignment operator ``=``.  For example, the following code assigns the value 2 to the variable ``x``.

.. code-block:: python

	x = 2

Once you have executed this code (``shift + enter`` in the Jupyter cell), Python will now look at the symbol ``x`` and think to itself "2".  To see this, in a new cell type ``print(x)``.  The output will not be "x", but ``2``!

You can create as many variables as you want, and as long as they have different names (more on naming in a minute), Python will keep track of each of them.  For example, let's set ``var2 = 5``.  (Print ``var2`` and verify that it returns 5.)

What is exciting about all of this then is that we can operate on these variables and Python will operate on the underlying data as if we had only supplied that data!  For example, execute the following commands:

.. code-block:: python
	:linenos:

	print(x**2)
	print(y + 3)
	print(x + y)

We can also use variables to assign new variables:

.. code-block:: python

	x_times_var2 = x * var2

What is the value of ``x_times_var2``?

You can also use variables to update the value to which they have been assigned.  Type the following into a new cell:

.. code-block:: python

	print("Before self-assignment:", x)
	x = x + 2 ## What is happening here!?
	print("After self-assignment:", x)

.. sidebar::New Syntax!
	
	Notice the new syntax for :py:func:`print` in the example above.  Try removing the commas between ``"...assignment:"`` and ``x``.  What happens?

The value of ``x`` has been used to assign a new value to ``x``!  What happens if you run this cell again?  Return to the earlier cell where you typed only ``print(x)``, what is the output?  What you should see is that when you reassigned the value of ``x``, this change is propagated in the Python code *everywhere*.  This can make things tricky, so we'll make some quick notes about variables and working in Jupyter in just a moment.

As a final introductory point on creating variables, please type ``print(my_favorite_variable)`` into a new cell and execute it.  You should now see an angry **error message**!

.. code-block:: python

	-------------------------------------------------------------------------
	NameError                               Traceback (most recent call last)
	<ipython-input-3-eabb85222416> in <module>
	----> 1 print(my_favorite_variable)

	NameError: name 'my_favorite_variable' is not defined

Once you have overcome the shape of the odd message that Python has regurgitated, I ask that you read the last line: ``NameError: name 'my_favorite_variable' is not defined``.  This is Python telling you that there's been an error with a variable *name* (hence the ``NameError``).  Specifically, ``my_favorite_variable`` "is not defined"! This is because at no point in our notebook have we *defined* the ``my_favorite_variable`` variable by assigning data to it!  Try running ``my_favorite_variable = "This exists!"`` and then printing.  The error message disappears!  This is your first (guided) experience with error messages, but we will continue to practice parsing them.  Your take-away here should be that the last line of the error message gives the most direct reason why some code cannot run as you have written.

So, now that we know we have to *define* variables in order to use them in later pieces of code, and we know how to perform variable assignment in simple ways, it's time to make a few overarching comments about working in Jupyter and naming variables.

A Few Notes about Jupyter Notebooks
=====================================

#. You have already seen this, but once a cell has been executed, any variables that have been assigned or updated in that cell have also been assigned or updated in the workspace of *all other cells* in the notebook *even those above* that cell!  As a result, it is strongly recommended that your logical flow move downward through the notebook.  Use the print function *liberally* to make sure everything is working as you expect (you can always delete them once you're sure everything's ok).


#. Sometimes, thing will break or become confusing or messy.  Or maybe you're not sure whether you've defined a variable correctly above or below a new cell.  In this case, you should turn to the **Kernel** menu at the top toolbar.  There you will see several very useful options, especially **interrupt** and **restart**.  If something is taking too long (or forever), you can use interrupt to stop Python from continuing to execute, *interrupting* Python wherever it currently is in your code.  Less drastically, but also useful, you can use restart and its variants to clear away everything you've done and start the notebook over in terms of variable assignments but while keeping the code you've written.  This is a good way to make sure that your logical flow works (restart & run all) or to clean up your notebook before sharing (please do this before turning in notebooks for homework!).


.. sidebar:: Pro-Tip

	You can comment or uncomment many lines at once by selecting them with your mouse and then entering ``cmd + /``  or |cmd| ``+ /``.  (Try this out for yourself!)  As a result of this, I often use a double ``##`` to indicate descriptive comments that I don't accidentally want to uncover with |cmd| + ``/``, but this is not necessary.

#. In the cell containing ``x = x + 2``, I also asked you to type ``## What is happening here!?``  This is known as a **comment**, where you can use anything to the right of a ``#`` to provide a text annotation of what your code is doing.  Comments do not affect how your code runs, but they are **imperative** for how your code is used, both by others and your *future* self.  You can also use them while working through broken code to discover bugs by "commenting out" lines of code by placing a ``#`` at the beginning of the lines and then "uncommenting" them one by one until you find the part that's breaking.  This is how commenting works in Python, and is not unique to Jupyter.  



A Few Notes about Variable Names
==================================

With a few exceptions, you can use any set of connected alphanumeric characters (and the underscore, ``_``) to name your variables.  As a result, you may be tempted to use ``x`` and ``y`` as in math class.  This is not advised!  The flexibility of variable names means that you should err on the side of *descriptiveness* over brevity.  If you are calculating the length of bird's beaks, name your variable ``beak_lens``.  If you calculate the mean, save it as ``mean_beak_len``.  This may seem tedious, but space (in memory and on the screen) is cheap, and the description will help you and others know what your code is doing.  Furthermore, Jupyter (and many other Python IDEs) have **tab-completion** meaning that at any point in typing you can hit the ``tab`` button and a drop-down menu will populate with variables and functions that could complete the word you've already started, meaning that long variables take just as long as short ones!  (This also greatly diminishes typos!)

The only real constraint you might encounter on variable names are that they can't contain non-alphanumeric characters or the underscore (A-Z, a-z, 0-9, and ``_`` only) and that they can't start with a number.  (You *can* start a variable with ``_``.  In Python it is convention that variables that start with an underscore are **private** variables, which are not meant to be accessed by an end user.  You don't need to worry about this, I just want to point it out in case you see such a variable.)

Variable names are **case-sensitive**!  ``Var`` is different from ``var`` is different from ``vAR`` is different from ``VAR``.  As a result, don't use capitalization to distinguish variables!  It will quickly become very confusing!  (Similarly, don't use ``var1``, ``var2``, ``var3``, etc.  You will quickly forget what they all are!)

The other main exception to variable names is that you shouldn't give variables names that already correspond to Python functions, like ``print``.  To see why, type the following:

.. code-block:: python

	print = 43
	print(print)

You should get a ``TypeError: 'int' object is not callable``.  This is telling you that you have tried to "call" a function (``print``) but that ``print`` is now an "``int``" object that cannot be called!  (Python designates functions "callable" because you can "call" on them to do something.)  This is because you just said ``print = 43`` - you've assigned ``print`` to be the number 43 - so it no longer corresponds to the Python function of printing values to the screen.  This shouldn't come up too often, but the error message is opaque enough that you should be warned!

.. warning:: You will have to restart your kernel after this if you want to use ``print`` anymore!  (Kernel -> Restart)


Exercise 3.1
==============

Now that we've given you an overview of what variables are and how we can and can't (and should and shouldn't) assign them, give these exercises a whirl!

#.  Create two variables assigned to your favorite numbers.  Use these two variables to create another new variable ``num1_times_num2`` that contains their product.


#.  Calculate the *average* of your favorite numbers and save it as a new variable, ``my_favorite_sum``.  Print your favorite numbers and this average with a description using the ``print("My message goes here", my_var)`` syntax.


#.  Implement the compound interest formula below in a cell **without defining any variables**.  

	.. math:: 

	   A = P\left(1 + \frac{r}{n}\right)^{nt}

	That is, your cell should just have

	.. code-block:: python

		A = some_operations_involving P, r, n, t
		print(A)

	Execute the cell to get a ``NameError``.  Which variable is said to be undefined?  

	Add a new cell above the cell containing your formula (Hint: look at the `Command mode <https://jupyter-notebook.readthedocs.io/en/stable/examples/Notebook/Notebook%20Basics.html#Command-mode>`_ shortcuts) and execute:

	.. code-block:: python

		P = 1000 ## Principal (in dollars)
		r = 0.07 ## A great interest rate!
		n = 12   ## Compounded monthly
		t = 5    ## Years invested

	Use ``A`` and ``P`` to verify that you will have made over $400 on your investment!  That is, print out (with a descriptive message) exactly how much your investment has *increased*, not just the final amount, ``A``. 


*************************
Python Data Types
*************************

At this point, we've mostly been working with numbers, but part of Python's versatility is that it has the capability to work with arbitrary kinds of data, which are called **types**.  Python has several `built-in types <https://docs.python.org/3/library/stdtypes.html>`_, which we'll discuss in turn, but eventually when you learn about classes, you will see how you can effectively make Python work for arbitrary data structures.  (This is because Python is *object-oriented*, but we'll unpack that more later.)

While this may not seem super crucial to know about right away, in Python it is important to know about data types because Python can do **different things with different types**.  That is, depending on the data type, Python will know automatically how to apply the  ``+`` operation, but for other types it will not.  We'll show how this makes sense as we go through the main Python types and explore their capabilities.

The four basic Python types are:

#. `Strings <https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str>`_ - "strings" of alpha-numeric characters

#. `Integers <https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex>`_ - self-explanatory, includes positive and negative integers

#. `Floats <https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex>`_ - "floating-point numbers", or how computers store decimal numbers

#. `Booleans <https://docs.python.org/3/library/stdtypes.html#boolean-values>`_ - binary true or false variables.

To check what type a variable is, you can apply the :py:func:`type` function.  Execute the following to see:

.. code-block:: python
	:linenos:

	string = "Hello World!"     ## Notice the quotation marks!
	integer = 9                 ## Notice the LACK of a decimal
	floating_point = 3.1415926
	boolean = True              ## The options are True and False

	print(string)
	print(type(string))

	print(integer)
	print(type(integer))

	print(float)
	print(type(float))

	print(boolean)
	print(type(boolean))

If you ever receive a ``TypeError``, it is, somewhat expectedly, an error arising from something being the wrong type!  We saw this earlier when we tried to treat an integer as a function - integers can't be "called", so it caused a ``TypeError``.


Integers and Floats
======================

You've already seen variables holding these data types in action, and they largely operate as you'd expect.  We only note that because computers have finite memory, they can only store numbers to a finite precision.  Typically, Python uses 32 `bits <https://en.wikipedia.org/wiki/Bit>`_ to store integers, meaning that the integer type can represent any integer from :math:`-2^{31}` to :math:`2^{31}-1` because it has one bit to indicate whether the integer is positive or negative and then 31 leftover 0's and 1's.  Similarly, floats use 64 bits, so that they can represet :math:`2^{64}` numbers between :math:`\pm 6.02\times 10^{23}`.  As a result, there are some (most) decimals that cannot be perfectly represented by your computer, which can result in `roundoff error <https://mathworld.wolfram.com/RoundoffError.html>`_, which can be a big problem in numerical calculations.  In practice, this means that you might see that Python returns 0.30000000000000004 when you enter ``print(3 * 0.1)`` instead of 0.3, as you hoped.  This error is :math:`4\times 10^{-16}`, which can be negigible in most applications.

Booleans
==========

These are perhaps the most straightforward data type: they are either ``True`` or ``False``.  We'll see that these can be very useful in selecting data that meet certain conditions, so we'll take care to explain how booleans operate in comparison to other types later.  Briefly however, consider the following code:

.. code-block:: python
	:linenos:

	truth = True
	falsehood = False

	print(truth)
	print(falsehood)

	print(truth + falsehood)
	print(truth - falsehood)
	print(truth * falsehood)
	print(truth ** falsehood)

	print(truth and falsehood)
	print(truth or falsehood)
	print(truth and (truth or falsehood))

	print(truth / falsehood)

The output might not make sense right now, but make sure to read the error message at the end!  Notice that we introduced the new operations ``and`` and ``or``.  What do they seem to do?

Strings
=========

The most nuanced of our basic data types are **strings**, which are sets of characters that we enclose with either single (``'``) or double (``"``) quotation marks.  We did this in the earlier example with  ``string = "Hello World!"``, but we can also use one type of quotation mark to enclose a string containing the other.  For example:

.. code-block:: python

	quote = "Harold Abelson once said, 'Programs must be written for people to read.'"
	print(quote)

The start and end quotation marks must match, however:

.. code-block:: python

	errorful_string = "This is a bad string'

Take the time to read this message!  Why does this cause a ``SyntaxError``?


Operations with Strings
--------------------------

Strings are an interesting data type because they really show how type dictates output in Python.  For example, try the following (remember to try commenting out lines that throw errors to move on in a program):

.. code-block:: python
	:linenos:

	string1 = "This and"
	string2 = 'that'
	number1 = 4
	print(string1, string2, number1) ## NOTE NEW SYNTAX

	string3 = string1 + string2
	print(string3)

	string4 = string1 - string2   ## COMMENT THIS OUT IF IT DOESN'T WORK
	print(string4)				  ## What does it mean to "subtract" two
								  ## strings anyways?

	string_plus_int = string2 + number1 ## Does this work?
	print(string_plus_int)

	string_times_int = string2 * number1 ## Does this work?
	print(string_times_int)

What you will see above is that you can concatenate strings with the ``+`` operator and you can multiply a string by an integer to produce a string containing ``integer`` multiples of the string!  This is definitely different from how those operators worked on integers!

Special Characters
--------------------

Strings can also be used to indicate whitespace other than spaces with the ``\n`` **newline** and ``\t`` **tab** characters.  As an example, consider the following:

.. code-block:: python

	untabbed_string = "I'm here!"
	tabbed_string = "\tI'm over here!"
	print(untabbed_string)
	print(tabbed_string)

	print()   ## What does this do?  Comment it out and see what changes!

	multiline_string = "This str\ning has \n ma\n\nny lines!"
	print(multiline_string)

We'll see shortly that aside from holding data that can only be stored as words or characters, string manipulation is also very useful for *annotating* outputs of your codes.

String Formatting
-------------------

The following will be the most syntax-heavy code that you've been exposed to, but is too useful to omit for much longer.  At some point in your Python career, you are going to want to format the legend of a plot or the header of an output file based on the *value* of a variable.  These will necessarily be strings because they will be combinations of words and (maybe) numbers, but part of the string will be filled in by Python via **string formatting**.  There are a few ways to accomplish this in Python, but I'll bring up the two ways that I prefer.

First, we can use the :py:func:`format` function like this:

.. code-block:: python
	:linenos:

	my_int = 2
	my_float = 1234.56789
	my_string = "The integer is {}.  The float is {}.".format(my_int, my_float)
	print(my_string)

	my_other_string = "The float is {1}. The integer is {0}.".format(my_int, my_float)
	print(my_other_string)

	## NOTE the 'f' at the beginning of the string!
	another_string = f"The integer is {my_int}.  The float is {my_float}."
	print(another_string)

Basically we can call the :py:func:`format` function in a couple ways, or use the "f-string" (``f`` *before* the quotation mark) to tell Python that we'd like to fill in the ``{}`` with variables that are either given to ``format`` as input (first and second strings) or put directly inside the braces (only works with f-strings).  The order in which they are inserted into the string is inferred from the order they are given to ``format`` or by a number indicating which input to put where (0 indicates the first input, 1 the second, etc.).  I prefer f-strings because they are the most concise, but all of these are equally valid by Python.  You can also specify how the inputs are formatted into the string (say you want fewer decimal places shown) by adding inputs as given `here <https://docs.python.org/3.4/library/string.html#format-string-syntax>`_.  

.. admonition:: String Formatting is Descriptive!

	Throughout the rest of this tutorial I will encourage you to use string formatting to make it clear to yourself and any one else looking at your work what it is that you're doing!  In real code for real problems, this is often very useful for diagnosing problems or communicating with users.

String Functions
------------------

Now that we've opened the can of worms with string formatting, it's worth pointing out that there are several other functions that operate on strings to produce interesting changes.  We'll highlight a few here that may seem cosmetic, but are useful for introducing you to the **method**-style for calling functions.  Consider the following:

.. code-block:: python

	my_name = "eric johnson"
	my_capitalized_name = my_name.capitalize()
	my_corrected_name = my_name.title()
	print(f"My name is {my_name}...")
	print(f"My name is {my_capitalized_name}...")
	print(f"My name is {my_corrected_name}...")

	num_e = my_name.count("e")
	num_E = my_name.count("E")  ## This is a bad variable name outside this context!!!
	print(f"My name has {num_e} e's in it?")
	print(f"My name has {num_E} E's in it?")

There are many `string methods <https://docs.python.org/3.4/library/stdtypes.html#string-methods>`_, but the syntax for these **methods** is ``my_str.method(input1, input2)``.  We'll talk more about what makes a function a method :doc:`later </11_Classes/classes>`, but for now it suffices to note that there are functions in Python that exist **independent** of any variable, such as ``print`` and ``help``, and there are those that are attached to a variable, such as ``str.captialize()``.  Methods are the latter type.  Going forward, you will see both types of funtions, but you can always think of them as input-output relationships: they take some input, crank a wheel, and spit something out.  The syntax indicates whether it is something special that only strings (for example) can do, or whether it's an operation outside any specific data structure.

As another example of a non-method function, consider the :py:func:`len` function, which we'll discuss more in the :doc:`next section </3_Lists_Arrays/lists_arrays>`.  This function returns the length of a string in characters, as you can see:

.. code-block:: python
	
	my_name = "eric johnson".title() ## What is this output!?
	my_str = "Eric is a good name"
	my_tabbed_str = "Eric,\tis a good name"

	print(f"The length of {my_name} is {len(my_name)}")
	print(f"The length of {my_str} is {len(my_str)}")
	print(f"The length of {my_tabbed_str} is {len(my_tabbed_str)}")

.. sidebar:: How am I supposed to keep track of all of this!?

	The short answer is: you don't.  You should get in the habit of Googling "python string capitalization", for example.  Eventually you remember the useful stuff and you'll learn where to resource the rest.  By the end of the tutorial, you'll be able to cobble together what you need!  Don't make not knowing the function name the roadblock in this process!

You may want to look into these `string methods <https://docs.python.org/3.4/library/stdtypes.html#string-methods>`_, but I'll highlight that :py:func:`str.isnumeric`, :py:func:`str.join`, :py:func:`str.strip`, and :py:func:`str.lower` are ones that I use with some frequency.  Getting the length of a string with  :py:func:`len` is also very useful.

Converting Data Types
=======================

One of the most interesting (and sometimes overwhelming) things about Python is the way that these data types can interact with each other.  For example, we already saw that adding booleans maybe results in integers, and that multiplying a string by and integer results in a longer string.  As a result, it's worth noting how all these different data types interact and, when it's not what you're looking for, how you can convert between these types.

More specifically, these Python types come with associated functions :py:func:`int`, :py:func:`float`, :py:func:`bool`, and :py:func:`str`, that when applied to a variable, will attempt to convert it into the function's named data type.  For example, consider:

.. code-block:: python
	:linenos:

	number_str = "1234"
	print(f"'number_str' = {number_str} is type {type(number_str)}")
	floated_number_str = float(number_str)
	print(f"'floated_number_str' = {floated_number_str} is type {type(floated_number_str)}")

	## Put this in a second cell!
	not_number_str = "abcd"
	print(f"\n'not_number_str' = {not_number_str} is type {type(not_number_str)}")
	floated_not_number_str = float(not_number_str)
	print(f"'floated_not_number_str' = {floated_not_number_str} is type {type(floated_not_number_str)}")

.. sidebar:: ``ValueError``

	Note that this code generated a ``ValueError`` because the :py:func:`float` function wasn't upset with the *type* of the input, ``not_number_str``, but with its *value*.

You will see that ``number_str`` is originally a string type (indicated by ``<class 'str'>>``), but can successfully be converted to a float with the ``float`` function.  On the other hand, the ``not_number_str`` cannot, because Python doesn't know how to turn "abcd" into a number.  Conversely, you will find that Python has few problems converting things into strings.  As a result, the other way to format strings is to coerce everything into a string using :py:func:`str` and then add the strings together.

We'll leave it to the exercise to explore all the options, but I do want to draw your attention to two special cases.  First, consider several floats that we want to convert into integers.  Before you type the code, please write down what you **expect** the output to be.

.. code-block:: python
	:linenos:

	pos1 = 2.1
	pos2 = 1.9

	neg1 = -2.1
	neg2 = -1.9

	int_pos1 = int(pos1)
	int_pos2 = int(pos2)

	int_neg1 = int(neg1)
	int_neg2 = int(neg2)

	## Comment this out AFTER you have made your predictions.
	# print(f"int('pos1' = {pos1}) is {int_pos1}")
	# print(f"int('pos2' = {pos2}) is {int_pos2}")
	# print()
	# print(f"int('neg1' = {neg1}) is {int_neg1}")
	# print(f"int('neg2' = {neg2}) is {int_neg2}")

To see the explanation, :doc:`go here </2_Variables_DataTypes/floats2ints>`

The other interesting case is what Python thinks should be turned into a ``True`` or a ``False`` in the context of booleans.  Again, first write down for yourself what you **expect** to result from the following code, then execute it.

.. code-block:: python
	:linenos:

	pos_int = 4
	neg_int = -3
	zero_int = 0

	pos_float = 7.13
	small_pos_float = 0.0003
	neg_float = -4.67
	zero_float = 0.0

	number_str = "3.12"
	zero_str = "0"
	letter_str = "abcdef"
	empty_str = "" ## What is this??? Check the type!

	## Comment this out AFTER you have made your predictions.
	# print(f"Converting {pos_int} to boolean gives {bool(pos_int)}")
	# print(f"Converting {neg_int} to boolean gives {bool(neg_int)}")
	# print(f"Converting {zero_int} to boolean gives {bool(zero_int)}")

	# print(f"\nConverting {pos_float} to boolean gives {bool(pos_float)}")
	# print(f"Converting {small_pos_float} to boolean gives {bool(small_pos_float)}")
	# print(f"Converting {neg_float} to boolean gives {bool(neg_float)}")
	# print(f"Converting {zero_float} to boolean gives {bool(zero_float)}")

	# print(f"\nConverting {number_str} to boolean gives {bool(number_str)}")
	# print(f"Converting {zero_str} to boolean gives {bool(zero_str)}")
	# print(f"Converting {letter_str} to boolean gives {bool(letter_str)}")
	# print(f"Converting {empty_str} to boolean gives {bool(empty_str)}")


To see the explanation, :doc:`go here </2_Variables_DataTypes/everything2bool>`

At this point, you've seen enough of the details of types in Python to start to see how we can use Python to hold and start to manipulate different pieces of data.  After these exercises, the next section will introduce you to how you deal with *lots of data* and you will have your first introduction to `numpy <https://numpy.org/>`_, which is "the fundamental package for scientific computing in Python".  With those pieces in place, you'll be ready to start shredding real data of all shapes and sizes.

Exercise 3.2
==============
#. Create a variable for your name and another for your age.  Use string formatting to introduce your name and age to Python.  Create the same for a  friend (real or imaginary).  Then create a `Frankenstein's monster <https://www.gutenberg.org/files/42324/42324-h/42324-h.htm>`_ of you and your friend by concatenating your names and averaging your ages.  Print your creation to the screen using string formatting.

#. Recreate the pattern on the screen below with **one print statement** using string concatenation, string multiplication, and newline characters/tabs.  Use only ``star = "*"``, ``up = "^"``, ``line = '|'`` and ``space = ' '`` as initial variables (you may create intermediates!).

   .. code-block:: python

       *
      ^^^
     *^*^*
    ^^*^*^^
      |||

#. Perform the reverse of the last section: convert ``True`` and ``False`` into integer, float, and string types.  Write *in words* what happens.  Practice *predicting* what might happen and then connecting that with what actually happened.

#. **BONUS** Consider the following:

	.. code-block:: python

		a, b = 'Eric', "Johnson"  ## Can we do *double* assignment!?
		print(a, b)
		b, a = a, b
		print(a, b)
		my_name = ", ".join([a, b])  ## This is NEW SYNTAX
		print(my_name)
		output = a = b
		print(a, b, output)
		output = (a = b)
		print(a, b, output)

	Write a sentence or two about what you think is happening.   In particular, which direction does assignment "flow" in line 3?  Again, comment out lines that cause errors if you want to ignore them.

.. |cmd|     unicode:: U+2318 .. Mac Command Symbol