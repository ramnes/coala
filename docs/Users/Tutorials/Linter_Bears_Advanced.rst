Linter Bears - Advanced feature reference
=========================================

[Abstract]

Custom processing functions with ``process_output``
---------------------------------------------------

[...] [TODO Mention also the idea of splitting up output-processing!]

Additional prerequisite check
-----------------------------

Linter supports doing an additional executable check before together with the
normal one. For example this is useful to test the existence of non-python
modules (for example Java modules). [TODO - See prerequisite_check_command]

Caching arguments only dependent on section values
--------------------------------------------------

[Often arguments created by ``create_arguments`` are repetitive. Especially for
 large --> configurations <--??? this can slow down the execution. ...]

[TODO: Section is already guaranteed to be not changed from coala side, though
 this is still not completely safe from user perspective.
 Wait for FrozenSection?]
