###############
FLOATS TO INTS
###############

Floats are turned into integers by simply returning the *integer* component of the float.  For example, :math:`1.9 = 1 + 0.9`, so ``int(1.9) = 1``, but :math:`2.1 = 2 + 0.1` so that ``int(2.1) = 2``.  Meanwhile :math:`-1.9 = -1 - 0.9`, so ``int(-1.9) = -1``, but :math:`-2.1 = -2 - 0.1` so that ``int(-2.1) = -2``.

.. warning::
	
	The :py:func:`int` function does **NOT** round to the nearest integer.