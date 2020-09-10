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


#. In the cell containing ``x = x + 2``, I also asked you to type ``## What is happening here!?``  This is known as a **comment**, where you can use anything to the right of a ``#`` to provide a text annotation of what your code is doing.  Comments do not affect how your code runs, but they are **imperative** for how your code is used, both by others and your *future* self.  You can also use them while working through broken code to discover bugs by "commenting out" lines of code by placing a ``#`` at the beginning of the lines and then "uncommenting" them one by one until you find the part that's breaking.  This is how commenting works in Python, and is not unique to Jupyter.  

   As a pro-tip: you can comment or uncomment many lines at once by selecting them with your mouse and then entering ``cmd``/|cmd|``+ /``.  (Try this out for yourself!)  As a result of this, I often use a double ``##`` to indicate descriptive comments that I don't accidentally want to uncover with |cmd|+``/``, but this is not necessary.


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


Exercise 2.1
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

At this point, we've mostly been working with numbers, but part of Python's versatility is that it has the capability to work with arbitrary kinds of data, which are called **types**.  Python has several built-in types, which we'll discuss in turn, but eventually when you learn about classes, you will see how you can effectively make Python work for arbitrary data structures.  (This is because Python is *object-oriented*, but we'll unpack that more later.)

While this may not seem super crucial to know about right away, in Python it is important to know about data types because Python can do **different things with different types**.  That is, depending on the data type, Python will know automatically how to apply the  ``+`` operation, but for other types it will not.  We'll show how this makes sense as we go through the main Python types and explore their capabilities.

The `four basic Python types <https://docs.python.org/3/library/stdtypes.html>`_ are:

#. `Strings <https://docs.python.org/3/library/string.html>`_ - "strings" of alpha-numeric characters

#. Integers - self-explanatory, includes positive and negative integers

#. Floats - "floating-point numbers", or how computers store decimal numbers

#. Booleans - binary true or false variables.

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

















.. |cmd|     unicode:: U+2318 .. Mac Command Symbol