

.. _textui:

============================
The Command-Line Test Runner
============================

The PHPUnit command-line test runner can be invoked through the
:file:`phpunit` command. The following code shows how to run
tests with the PHPUnit command-line test runner:

.. code-block:: bash

    $ phpunit ArrayTest
    PHPUnit 6.4.0 by Sebastian Bergmann and contributors.

    ..

    Time: 0 seconds

    OK (2 tests, 2 assertions)

When invoked as shown above, the PHPUnit command-line test runner will look
for a :file:`ArrayTest.php` sourcefile in the current working
directory, load it, and expect to find a ``ArrayTest`` test
case class. It will then execute the tests of that class.

For each test run, the PHPUnit command-line tool prints one character to
indicate progress:

``.``

    Printed when the test succeeds.

``F``

    Printed when an assertion fails while running the test method.

``E``

    Printed when an error occurs while running the test method.

``R``

    Printed when the test has been marked as risky (see
    :ref:`risky-tests`).

``S``

    Printed when the test has been skipped (see
    :ref:`incomplete-and-skipped-tests`).

``I``

    Printed when the test is marked as being incomplete or not yet
    implemented (see :ref:`incomplete-and-skipped-tests`).

PHPUnit distinguishes between *failures* and
*errors*. A failure is a violated PHPUnit
assertion such as a failing ``assertEquals()`` call.
An error is an unexpected exception or a PHP error. Sometimes
this distinction proves useful since errors tend to be easier to fix
than failures. If you have a big list of problems, it is best to
tackle the errors first and see if you have any failures left when
they are all fixed.

.. _textui.clioptions:

Command-Line Options
####################

Let's take a look at the command-line test runner's options in
the following code:

.. code-block:: bash

    $ phpunit --help
    PHPUnit 6.4.0 by Sebastian Bergmann and contributors.

    Usage: phpunit [options] UnitTest [UnitTest.php]
           phpunit [options] <directory>

    Code Coverage Options:

      --coverage-clover <file>    Generate code coverage report in Clover XML format.
      --coverage-crap4j <file>    Generate code coverage report in Crap4J XML format.
      --coverage-html <dir>       Generate code coverage report in HTML format.
      --coverage-php <file>       Export PHP_CodeCoverage object to file.
      --coverage-text=<file>      Generate code coverage report in text format.
                                  Default: Standard output.
      --coverage-xml <dir>        Generate code coverage report in PHPUnit XML format.
      --whitelist <dir>           Whitelist <dir> for code coverage analysis.
      --disable-coverage-ignore   Disable annotations for ignoring code coverage.

    Logging Options:

      --log-junit <file>          Log test execution in JUnit XML format to file.
      --log-teamcity <file>       Log test execution in TeamCity format to file.
      --testdox-html <file>       Write agile documentation in HTML format to file.
      --testdox-text <file>       Write agile documentation in Text format to file.
      --testdox-xml <file>        Write agile documentation in XML format to file.
      --reverse-list              Print defects in reverse order

    Test Selection Options:

      --filter <pattern>          Filter which tests to run.
      --testsuite <name,...>      Filter which testsuite to run.
      --group ...                 Only runs tests from the specified group(s).
      --exclude-group ...         Exclude tests from the specified group(s).
      --list-groups               List available test groups.
      --list-suites               List available test suites.
      --test-suffix ...           Only search for test in files with specified
                                  suffix(es). Default: Test.php,.phpt

    Test Execution Options:

      --dont-report-useless-tests Do not report tests that do not test anything.
      --strict-coverage           Be strict about @covers annotation usage.
      --strict-global-state       Be strict about changes to global state
      --disallow-test-output      Be strict about output during tests.
      --disallow-resource-usage   Be strict about resource usage during small tests.
      --enforce-time-limit        Enforce time limit based on test size.
      --disallow-todo-tests       Disallow @todo-annotated tests.

      --process-isolation         Run each test in a separate PHP process.
      --globals-backup            Backup and restore $GLOBALS for each test.
      --static-backup             Backup and restore static attributes for each test.

      --colors=<flag>             Use colors in output ("never", "auto" or "always").
      --columns <n>               Number of columns to use for progress output.
      --columns max               Use maximum number of columns for progress output.
      --stderr                    Write to STDERR instead of STDOUT.
      --stop-on-error             Stop execution upon first error.
      --stop-on-failure           Stop execution upon first error or failure.
      --stop-on-warning           Stop execution upon first warning.
      --stop-on-risky             Stop execution upon first risky test.
      --stop-on-skipped           Stop execution upon first skipped test.
      --stop-on-incomplete        Stop execution upon first incomplete test.
      --fail-on-warning           Treat tests with warnings as failures.
      --fail-on-risky             Treat risky tests as failures.
      -v|--verbose                Output more verbose information.
      --debug                     Display debugging information.

      --loader <loader>           TestSuiteLoader implementation to use.
      --repeat <times>            Runs the test(s) repeatedly.
      --teamcity                  Report test execution progress in TeamCity format.
      --testdox                   Report test execution progress in TestDox format.
      --testdox-group             Only include tests from the specified group(s).
      --testdox-exclude-group     Exclude tests from the specified group(s).
      --printer <printer>         TestListener implementation to use.

    Configuration Options:

      --bootstrap <file>          A "bootstrap" PHP file that is run before the tests.
      -c|--configuration <file>   Read configuration from XML file.
      --no-configuration          Ignore default configuration file (phpunit.xml).
      --no-coverage               Ignore code coverage configuration.
      --no-extensions             Do not load PHPUnit extensions.
      --include-path <path(s)>    Prepend PHP's include_path with given path(s).
      -d key[=value]              Sets a php.ini value.
      --generate-configuration    Generate configuration file with suggested settings.

    Miscellaneous Options:

      -h|--help                   Prints this usage information.
      --version                   Prints the version and exits.
      --atleast-version <min>     Checks that version is greater than min and exits.

``phpunit UnitTest``

    Runs the tests that are provided by the class
    ``UnitTest``. This class is expected to be declared
    in the :file:`UnitTest.php` sourcefile.

    ``UnitTest`` must be either a class that inherits
    from ``PHPUnit\Framework\TestCase`` or a class that
    provides a ``public static suite()`` method which
    returns a ``PHPUnit_Framework_Test`` object, for
    example an instance of the
    ``PHPUnit_Framework_TestSuite`` class.

``phpunit UnitTest UnitTest.php``

    Runs the tests that are provided by the class
    ``UnitTest``. This class is expected to be declared
    in the specified sourcefile.

``--coverage-clover``

    Generates a logfile in XML format with the code coverage information
    for the tests run. See :ref:`logging` for more details.

    Please note that this functionality is only available when the
    tokenizer and Xdebug extensions are installed.

``--coverage-crap4j``

    Generates a code coverage report in Crap4j format. See
    :ref:`code-coverage-analysis` for more details.

    Please note that this functionality is only available when the
    tokenizer and Xdebug extensions are installed.

``--coverage-html``

    Generates a code coverage report in HTML format. See
    :ref:`code-coverage-analysis` for more details.

    Please note that this functionality is only available when the
    tokenizer and Xdebug extensions are installed.

``--coverage-php``

    Generates a serialized PHP_CodeCoverage object with the
    code coverage information.

    Please note that this functionality is only available when the
    tokenizer and Xdebug extensions are installed.

``--coverage-text``

    Generates a logfile or command-line output in human readable format
    with the code coverage information for the tests run.
    See :ref:`logging` for more details.

    Please note that this functionality is only available when the
    tokenizer and Xdebug extensions are installed.

``--log-junit``

    Generates a logfile in JUnit XML format for the tests run.
    See :ref:`logging` for more details.

``--testdox-html`` and ``--testdox-text``

    Generates agile documentation in HTML or plain text format for the
    tests that are run. See :ref:`other-uses-for-tests` for
    more details.

``--filter``

    Only runs tests whose name matches the given regular expression
    pattern. If the pattern is not enclosed in delimiters, PHPUnit
    will enclose the pattern in ``/`` delimiters.

    The test names to match will be in one of the following formats:

    ``TestNamespace\TestCaseClass::testMethod``

        The default test name format is the equivalent of using
        the ``__METHOD__`` magic constant inside
        the test method.

    ``TestNamespace\TestCaseClass::testMethod with data set #0``

        When a test has a data provider, each iteration of the
        data gets the current index appended to the end of the
        default test name.

    ``TestNamespace\TestCaseClass::testMethod with data set "my named data"``

        When a test has a data provider that uses named sets, each
        iteration of the data gets the current name appended to the
        end of the default test name. See
        :numref:`textui.examples.TestCaseClass.php` for an
        example of named data sets.

        .. code-block:: php
            :caption: Named data sets
            :name: textui.examples.TestCaseClass.php

            <?php
            use PHPUnit\Framework\TestCase;

            namespace TestNamespace;

            class TestCaseClass extends TestCase
            {
                /**
                 * @dataProvider provider
                 */
                public function testMethod($data)
                {
                    $this->assertTrue($data);
                }

                public function provider()
                {
                    return [
                        'my named data' => [true],
                        'my data'       => [true]
                    ];
                }
            }
            ?>

    ``/path/to/my/test.phpt``

        The test name for a PHPT test is the filesystem path.

    See :numref:`textui.examples.filter-patterns` for examples
    of valid filter patterns.

    .. code-block:: php
        :caption: Filter pattern examples
        :name: textui.examples.filter-patterns

    See :numref:`textui.examples.filter-shortcuts` for some
    additional shortcuts that are available for matching data
    providers.

    .. code-block:: php
        :caption: Filter shortcuts
        :name: textui.examples.filter-shortcuts

``--testsuite``

    Only runs the test suite whose name matches the given pattern.

``--group``

    Only runs tests from the specified group(s). A test can be tagged as
    belonging to a group using the ``@group`` annotation.

    The ``@author`` annotation is an alias for
    ``@group`` allowing to filter tests based on their
    authors.

``--exclude-group``

    Exclude tests from the specified group(s). A test can be tagged as
    belonging to a group using the ``@group`` annotation.

``--list-groups``

    List available test groups.

``--test-suffix``

    Only search for test files with specified suffix(es).

``--report-useless-tests``

    Be strict about tests that do not test anything. See :ref:`risky-tests` for details.

``--strict-coverage``

    Be strict about unintentionally covered code. See :ref:`risky-tests` for details.

``--strict-global-state``

    Be strict about global state manipulation. See :ref:`risky-tests` for details.

``--disallow-test-output``

    Be strict about output during tests. See :ref:`risky-tests` for details.

``--disallow-todo-tests``

    Does not execute tests which have the ``@todo`` annotation in its docblock.

``--enforce-time-limit``

    Enforce time limit based on test size. See :ref:`risky-tests` for details.

``--process-isolation``

    Run each test in a separate PHP process.

``--no-globals-backup``

    Do not backup and restore $GLOBALS. See :ref:`fixtures.global-state`
    for more details.

``--static-backup``

    Backup and restore static attributes of user-defined classes.
    See :ref:`fixtures.global-state` for more details.

``--colors``

    Use colors in output.
    On Windows, use `ANSICON <https://github.com/adoxa/ansicon>`_ or `ConEmu <https://github.com/Maximus5/ConEmu>`_.

    There are three possible values for this option:

    -

      ``never``: never displays colors in the output. This is the default value when ``--colors`` option is not used.

    -

      ``auto``: displays colors in the output unless the current terminal doesn't supports colors,
      or if the output is piped to a command or redirected to a file.

    -

      ``always``: always displays colors in the output even when the current terminal doesn't supports colors,
      or when the output is piped to a command or redirected to a file.

    When ``--colors`` is used without any value, ``auto`` is the chosen value.

``--columns``

    Defines the number of columns to use for progress output.
    If ``max`` is defined as value, the number of columns will be maximum of the current terminal.

``--stderr``

    Optionally print to ``STDERR`` instead of
    ``STDOUT``.

``--stop-on-error``

    Stop execution upon first error.

``--stop-on-failure``

    Stop execution upon first error or failure.

``--stop-on-risky``

    Stop execution upon first risky test.

``--stop-on-skipped``

    Stop execution upon first skipped test.

``--stop-on-incomplete``

    Stop execution upon first incomplete test.

``--verbose``

    Output more verbose information, for instance the names of tests
    that were incomplete or have been skipped.

``--debug``

    Output debug information such as the name of a test when its
    execution starts.

``--loader``

    Specifies the ``PHPUnit_Runner_TestSuiteLoader``
    implementation to use.

    The standard test suite loader will look for the sourcefile in the
    current working directory and in each directory that is specified in
    PHP's ``include_path`` configuration directive.
    A class name such as ``Project_Package_Class`` is
    mapped to the source filename
    :file:`Project/Package/Class.php`.

``--repeat``

    Repeatedly runs the test(s) the specified number of times.

``--testdox``

    Reports the test progress as agile documentation. See
    :ref:`other-uses-for-tests` for more details.

``--printer``

    Specifies the result printer to use. The printer class must extend
    ``PHPUnit_Util_Printer`` and implement the
    ``PHPUnit_Framework_TestListener`` interface.

``--bootstrap``

    A "bootstrap" PHP file that is run before the tests.

``--configuration``, ``-c``

    Read configuration from XML file.
    See :ref:`appendixes.configuration` for more details.

    If :file:`phpunit.xml` or
    :file:`phpunit.xml.dist` (in that order) exist in the
    current working directory and ``--configuration`` is
    *not* used, the configuration will be automatically
    read from that file.

``--no-configuration``

    Ignore :file:`phpunit.xml` and
    :file:`phpunit.xml.dist` from the current working
    directory.

``--include-path``

    Prepend PHP's ``include_path`` with given path(s).

``-d``

    Sets the value of the given PHP configuration option.

.. admonition:: Note

   Please note that as of 4.8, options can be put after the argument(s).


