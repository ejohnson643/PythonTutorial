######################
EVERYTHING TO BOOLEAN
######################

In Python only "zero" elements are returned as ``False``.  So ``bool(0)`` is ``False``, but ``bool(-1)`` and ``bool(3)``.  A similar statement holds for floats.

For strings, only the **empty string** ``""`` gets returned as ``False``, all other non-empty strings get converted into ``True`` to indicate the presence of *something* in the data.