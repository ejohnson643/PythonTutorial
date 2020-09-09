======
PAGE 1
======


Testing out some intersphinx thingy does this cross ref? :py:func:`io.open`

Paragraphs are things!

We can do *italics*, **boldface**, and ``code samples``!  Or we can do 
thisis\ *one*\ word!

* This is a bulleted list.
* It has two items, the second
  item uses **two lines**

1. This is a numbered list.
2. It has two items as well.

#. This is an autonumbered list?
#. Does it start at 1 or 3??
	#. We can also make sublists.
	#. What an idea!

term (up to a line of text)
	The definition of term is ``term``, which must be indented

	But it can have multiple paragraphs!

next term
	Is described

| These lines have
| breaks that are perfectly
| preserved.

This is normal text, but this is a code sample (a literal block)::

	It is not processed in any way, except
	that the indentation is removed!

	It can span many lines.

But now it is over and this is a normal paragraph again.

We can also do "doctest" blocks:

>>> 1 + 1
2

Ok well making tables is a bit more annoying

+------------------------+----------+----------+----------+
| Header row, column 1   | Header 2 | Header 3 | Header 4 |
| (header rows optional) |          |          |          |
+========================+==========+==========+==========+
| body row 1, column 1   | column 2 | column 3 | column 4 |
+------------------------+----------+----------+----------+
| body row 2             | ...      | ...      | ...      |
+------------------------+----------+----------+----------+

But there are simpler tables too:

=====  =====  =======
A      B      A and B
=====  =====  =======
False  False  False
True   False  False
False  True   False
True   True   True
=====  =====  =======

I think you can make links like `this <https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html#hyperlinks/>`_

Or we can do it `like this`_.

.. _like this: https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html#hyperlinks


We can do sections!

########
PART 1
########

*********
Chapter 1
*********

.. _section-1:

Section 1
=========

Subsection 1
------------

SubSubSection 1
^^^^^^^^^^^^^^^

Paragraph 1
""""""""""""

WOW!  This follows the `Python\'s Guide for Documenting <https://docs.python.org/devguide/documenting.html#style-guide/>`_

And if we modify the Table of Contents in :doc:`index.rst </index>`, we can 
get these sections to show up on the main page!

Field Lists are sequences of fields

:fieldname: Field content

They are commonly used in Python documentation::

	def my_function(my_arg, my_other_arg):
		"""A function just for me!

		:param my_arg: The first of my arguments.
		:param my_other_arg: The second of my arguments.

		:returns: A message (just for me, of course).
	"""

Roles are things? Oh I see, we can also do :emphasis:`emphasis`, :strong:`strong`, :literal:`literal`, :subscript:`subscript`, :superscript:`superscript`, and
:title-reference:`title-reference`.

Then there are *directives* which sound cool.  Like this one: that gives Python-style documentation for a function.

.. function:: foo(x)
			  foo(y, z)
	:module: some.module.name

	Return a line of text input from the user

.. attention:: There's the `attention <http://docutils.sourceforge.net/docs/ref/rst/directives.html#attention/>`_ directive

.. caution:: There's the `caution <http://docutils.sourceforge.net/docs/ref/rst/directives.html#caution/>`_ directive


.. danger:: There's the `danger <http://docutils.sourceforge.net/docs/ref/rst/directives.html#danger/>`_ directive

.. error:: There's the `error <http://docutils.sourceforge.net/docs/ref/rst/directives.html#error/>`_ directive

.. hint:: There's the `hint <http://docutils.sourceforge.net/docs/ref/rst/directives.html#hint/>`_ directive

.. important:: There's the `important <http://docutils.sourceforge.net/docs/ref/rst/directives.html#important/>`_ directive

.. note:: There's the `note <http://docutils.sourceforge.net/docs/ref/rst/directives.html#note/>`_ directive

.. tip:: There's the `tip <http://docutils.sourceforge.net/docs/ref/rst/directives.html#tip/>`_ directive

.. warning:: There's the `warning <http://docutils.sourceforge.net/docs/ref/rst/directives.html#warning/>`_ directive

and the generic 

.. admonition:: There's the `admonition <http://docutils.sourceforge.net/docs/ref/rst/directives.html#admonition/>`_ directive
	
	Which maybe needs more stuff?  Oh no, this one lets you put your own title.

They note that really only "note" and "warning" are usually formatted.  Obvs the default also has "danger"/"error" as well.

We can also do

.. contents::

Do I need to break stuff up here?

.. topic:: Topic1

	This is a topic?

	What if I keep going?

Oh and then there are sidebars, which maybe actually go to the side???  That would be cool I'm trying to write enough text to test this...

.. sidebar:: Sidebar1

	This is a sidebar?

	What if I keep going?

Maybe I need text after it! Let's try that!

Aha!  That worked, now there's a sidebar next to my main stuff!  COOL

An important one might be Images

.. image:: The_GNU_logo.png
	:height: 100px
	:align: center
	:alt: The GNU logo

How do I get text?  Nvm

We can do Footnotes! [#f1]_ Or noted-foots, as I like to call them [#f2]_ !

Similarly, we can do references. [Ref]_


Then there are `Roles <https://www.sphinx-doc.org/en/master/usage/restructuredtext/roles.html/>`_.

I think they help with cross-referencing?

.. function:: install()

	This function installs a `handler` for every signal known by the :mod:`signal` module.  See the section :ref:`section-1` for more information. Changes!  Ok so we use ``:ref:`` to do references to things.

We can do math!  :math:`a^2 + b^2 = c^2`.  Neat!

.. hlist::
   :columns: 3

   * A list of
   * short items
   * that should be
   * displayed
   * horizontally

.. code-block:: python
   :linenos:
   :caption: this.py
   :name: this-py
   :emphasize-lines: 3,5

   def some_function():
       interesting = False
       print 'This line is highlighted.'
       print 'This one is not...'
       print '...but this one is.'

.. rubric:: Footnotes

..	[#f1] This is a footnote.
..	[#f2] This is a noted foot.

.. rubric:: References

.. [Ref] A totally legit reference (2020) Eric's Journal of Pretty Good Stuff

