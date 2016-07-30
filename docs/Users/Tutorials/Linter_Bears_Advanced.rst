Linter Bears - Advanced Feature Reference
=========================================

[Abstract]

Supplying Configuration Files with ``generate_config``
------------------------------------------------------

Often tools require a configuration file to run. ``@linter`` supports that
easily with overriding ``generate_config()``.

::

    @linter(executable='...')
    class MyBear:
        @staticmethod
        def generate_config(filename, file):
            config_file = ("value1 = 1\n"
                           "value=2 = 2")
            return config_file

The string returned from this method is written into a temporary file before
invoking ``create_arguments()``. If you return ``None``, no config-file is
generated.

The path of the temporary configuration-file can be accessed inside
``create_arguments()`` via the ``config_file`` parameter:

::

    @linter(executable='...')
    class MyBear:
        @staticmethod
        def generate_config(filename, file):
            config_file = ("value1 = 1\n"
                           "value=2 = 2")
            return config_file

        @staticmethod
        def create_arguments(filename, file, config_file):
            return "--use-config", config_file

.. note::

    By default no configuration file is generated.

Custom Processing Functions with ``process_output``
---------------------------------------------------

[...] [TODO Mention also the idea of splitting up output-processing!]

Additional Prerequisite Check
-----------------------------

Linter supports doing an additional executable check before running the bear
together with the normal one (checking if the executable exists). For example
this is useful to test the existence of external modules (for example Java
modules).

To enable this additional check with your commands, use the
``prerequisite_check_command`` parameter of ``@linter``.

::

    @linter(executable='...'
            prerequisite_check_command=('python3', '-c', 'import my_module'))
    class MyBear:
        pass

If the default error message does not suit you, you can also supply
``prerequisite_check_fail_message`` together with
``prerequisite_check_command``.

::

    @linter(executable='...'
            prerequisite_check_command=('python3', '-c', 'import my_module'),
            prerequisite_check_fail_message='my_module does not exist.')
    class MyBear:
        pass

Caching Arguments only Dependent on Section Values
--------------------------------------------------

[Often arguments created by ``create_arguments`` are repetitive. Especially for
 large --> configurations <--??? this can slow down the execution. ...]

[TODO: Section is already guaranteed to be not changed from coala side, though
 this is still not completely safe from user perspective.
 Wait for FrozenSection?]
