# MATLAB Style Guide

The following summary style guide has been adapted from *The elements of MATLAB style* by Richard Johnson [1] to distill the most important elements. Deviations from Johnson's style are marked with (†).

## General

Avoid causing confusion! Emphasize the following characteristics in your code:

- Simplicity
- Clarity
- Completeness
- Consistency
- Robustness

Avoid throw-away code. Everything you save in an `.m` file could be used again by you or somebody else. If it's worth saving, it's worth cleaning up to meet these style guides.

Following these principles helps the reader, which could be a stranger or a future you. The time taken to refactor code often saves far more time that might have been spent trying to understand or troubleshoot poorly written code.

Finally, document any intentional style deviations. You are allowed to break any of the rules in this guide, as long as you justify and document why you have done so.


# MATLAB Style, Part 1: Formatting

**General**

Format the code to make it more readable. Avoid long lines and multiple statements per line so that the code is easier to scan. Indent consistently to reveal logical structure. Use spaces consistently in appropriate places to make each line easier to read and interpret. In particular, insert spaces around operators and expressions to reveal the structure and meaning of statements. Write your code in logical blocks that can be read as paragraphs so that the program can be understood in chunks.

## 1.a. Line length
Lines should be no longer than 80 characters. Split long code lines at graceful points (commas, spaces, operators), and use one or more subexpressions on multiple lines rather than a single complicated expression where possible.

## 1.b. Indentation
Indentation should be 4 spaces and used consistently to structure code blocks. Avoid deeply nested indentation blocks and use subfunctions where appropriate.

## 1.c. Whitespace
(†) Use a single whitespace around all commas and operators. Do not use whitespace around parentheses, colons or semicolons.

## 1.d. Alignment
Align multiple lines with whitespace padding only if it enhances readability. In general, do not align operators or assignments across multiple statements.

```matlab
% avoid unnecessary whitespace padding between lines
row      = 3;
column   = 4;
diagonal = 5;

% use consistent operator spacing instead
row = 3;
column = 4;
diagonal = 5;

```

## 1.e. Code groups
Break code into logical groups by leaving one blank line between statements of different types (e.g. assignment statements and operational statements), and two blank lines between different functional code sections (e.g. an initialisation block and a looping block).


# MATLAB Style, Part 2: Naming conventions

## 2.a. lowerCamelCase variable and function names
Use lowerCamelCase style for general variable and function names, e.g. `velocity, angularAcceleration`.

## 2.b. Variable name length
Variable and function names should be at least three characters long, except when the scope of the variable is small, such as in a mathematical expression in a subfunction.

## 2.c. Numeric prefix
Use the prefix `n` for variables representing a number, e.g. `nFiles, nSegments` rather than `numFiles, numberOfSegements`. Using prefix `m` is permitted in the context of matrix dimensions.

## 2.d. Loop counters
Avoid using `i` and `j` as indices or loop counters. Where loops are nested, consider using `i, j, k` as a prefix for iterator variables, e.g.

```matlab
for iFile = 1:nFiles
    for jLine = 1:nLines
        % ...
    end
end

```

## 2.e. Shadowing names
Avoid variable and function names that shadow built-in functions or objects from a higher scope.

## 2.f. Readability
Variable and function names should be readable and relevant to their use. Avoid ambiguous abbreviations or acronyms, and don't use / re-use a variable name outside the intended context.

## 2.g. Numbers
Avoid using numbers in variable or function names, particularly to denote version (e.g. `foo1, foo2`), with the exception of the common case of "2" in place of "to" in functions such as `rad2deg`.

## 2.h. Scope of constants
Limit the scope of hard-coded constant values. Where constants are necessary in a larger scope, create a function to return that value instead (e.g. `pi`).

## 2.i. Uppercase constants
Constants specific to a single `.m` file should be written in uppercase, with a single underscore to separate, e.g. `MAX_ITERATIONS = 10`.

## 2.j. UpperCamelCase structures
Use UpperCamelCase style for structures, e.g. `Segment, JointTrajectory`.

## 2.k. Structure field names
Fieldnames of structures should follow general variable name conventions, and should not repeat the name of the parent structure.

## 2.l. Function prefixes
Use prefixes in functions consistently:
  - `find...` should return an index and / or the value at that index
  - `is...` should be reserved for boolean functions
  - `get/set...` should be reserved for setting or retrieving object properties

## 2.m. Classes
Classes and objects should be named the same way as structures, properties the same way as variables, and methods the same way as functions.


# MATLAB Style, Part 3: Documentation and comments

## 3.a. Useful comments
Make comments useful. Avoid simply restating what the code does, but describe why or how it works. Ensure comments are up-to-date with the actual code.

## 3.b. Function and class documentation
All functions and class definitions require header comments that support the behaviours of the inbuilt `help`, `lookfor` and `doc` functions.
  - For functions, the H1 line must be a short fragment summarising the behaviour, with a capitalised first letter and ending with a period. The subsequent lines should show and describe usage examples of all supported combinations of input and output variables, where the displayed variable names should match the function variable names. Bonus points for using `See also` and hyperlinks to more information. See also: [How to create help text for functions](https://www.mathworks.com/help/matlab/matlab_prog/add-help-for-your-program.html). An example function header is shown below.
  - For classes, this includes at minimum a single line summary of the class, constructor and main public properties and methods. Bonus points for further documentation. See also: [How to create help text for classes](https://www.mathworks.com/help/matlab/matlab_prog/create-help-for-classes.html).

```matlab
[a, b] = myExampleFunction(x, y, z)
% Combines scalar values in some exemplary way.
%   a = myFunction(x, y) combines scalar inputs x and y
%   in some way to create a scalar output a.
%   [a, b] = myFunction(x, y) additionally returns a vector
%   b as some combination of x, y and a.
%   myFunction(..., z) optionally takes a third scalar z
%   which offsets the returned values in some way.

```

## 3.c. Attribution
Any attribution, versioning or licensing comments should be separated by a new line from the header so it does not appear in the help text. In general, avoid documenting authorship or version if it is already contained in the version control system.

## 3.d. Restrictions
Enforce restrictions in code, not comments.  

```matlab
% beta must be greater than 0  <-- avoid
% replace with:
assert(beta > 0, 'myFunction:Beta', 'beta must be greater than 0.');

% make sure b is between a and c  <-- avoid
% replace with:
b = max(b,a);
b = min(b,c);

```

## 3.e. Dead code
Delete code rather than commenting it out. Where commented code blocks are used to show example behaviour of a program, consider moving it into an executable example script, function help text or external markdown documentation.

## 3.f. In-line comments
Avoid end-line comments in favour of comments in a separate line directly before the associated code.

## 3.g. Comment indentation
Comments should be indented to match the associated program code, with a single whitespace after the comment symbol `%`.

## 3.h. Section breaks
Use double percent signs `%%` only for section breaks and in formatted header comments. Section breaks should have a corresponding section title capitalised after a single whitespace, e.g. `%% Section title`, with further description in regular comments on the following lines as necessary. Never use more than two comment symbols (e.g. avoid `%%% comment`).

## 3.i. Multi-line comments
Multi-line comments should use complete sentences, though simple one-line comments can be brief.

## 3.j. Comment blocks
Avoid using comment blocks (`%{ ... }%`).


# MATLAB Style, Part 4: Programming

## 4.a. Global variables
Minimize the use of global variables and constants. Access the workspace scope only when explicitly necessary as part of the function behaviour.

## 4.b. Local constants
Define local constants only once. If a constant is used only once, define it just before it is used. Otherwise, define it near the top of the relevant file or subfunction.

## 4.c. Floating point values
Write floating point values with a digit before the decimal points, e.g. `0.5`, and avoid showing excessive decimal places.

## 4.d. Explicit conversions
Be explicit with datatype conversion and comparisons when using multiple datatypes.

## 4.e. Group data
Use structures to group related data. Use the function [`orderfields`](https://www.mathworks.com/help/matlab/ref/orderfields.html) when generating large structures to sort fields alphabetically to make them more readable.

## 4.f. Array orientation
Follow the MATLAB convention for data array orientation. Sequential or time series data should be stored as columns, such that a one-dimensional array of N positions should have size `1xN`. Keep in mind that MATLAB uses column-major layout for indexing multi-dimensional arrays, and sizes are shown as `row x column`. Standard functions such as `sum` and `mean` operate on the first dimension with length greater than 1.

## 4.g. Preallocation
Initialise or preallocate variables that are updated in a loop using `nan` or `false`, rather than dynamically resizing arrays or initialising values with `zeros` or `ones`.

```matlab
residual = nan(nRows);
for row = 1:nRows
    residual(row) = % ...
end

```

## 4.h. Loops
Keep loops readable, consistent and efficient. Where possible:
  - Do not change the loop index variable within the loop.
  - Minimize the use of `break` and `continue` statements.
  - Use [vectorisation](https://uk.mathworks.com/help/matlab/matlab_prog/vectorization.html) in place of loops unless it causes problems with readability or memory consumption.

## 4.i. If statements
(†) Simplify and reduce `if` statements where possible. Avoid `else` and `elseif` unless necessary, and try to use functions in place of `if` statements.

```matlab
% find the smallest of three values

% avoid this syntax
if x <= y
    if x <= z
        smallest = x;
    else
        smallest = z;
    end
else
    if y <= z
        smallest = y;
    else
        smallest = z;
    end
end

% this produces the same result more simply
smallest = min([x, y, z]);

```

## 4.j. Modular functions
Write code as modular functions wherever possible. Keep the scope of a function small and the behaviour simple. Use anonymous functions, local subfunctions and path functions in that order depending on the size and scope of the re-used code.

## 4.k. Level of abstraction
Maintain a consistent level of abstraction within any given scope. A high-level function should not perform algebraic computations in between general function calls. In these cases, replace the lower levels of abstractions with local functions.

## 4.l. Input arguments
Reduce the number and complexity of required arguments in public functions.
  - Consider replacing a long list of related arguments (more than four) with a structure.
  - Use `varargin` when there are multiple optional arguments in a logical sequence.
  - Consider using an [inputParser](https://uk.mathworks.com/help/matlab/ref/inputparser.html) object with parameter-value pairs when multiple optional arguments have no logical sequence.

## 4.m. Input validation
When defining a public function, use the native [Function Argument Validation](https://www.mathworks.com/help/matlab/matlab_prog/function-argument-validation-1.html) code block.
This eliminates clumsy argument-checking code and improves the readability and maintainability of the code.
  - The arguments block must start before the first executable line of the function, but after the function description,
    with a separating blank line (see example below).
  - [Function Argument Validation](https://www.mathworks.com/help/matlab/matlab_prog/function-argument-validation-1.html) should not
    be used in local and private functions. Also, it cannot be used in nested functions, abstract methods, or handle class destructors.
  - The function argument declaration can include any of these kinds of restrictions: **size**, **class** (i.e. `char`, `double`, `string`, etc.) ,
    **functions** (a comma-separated list of [validation functions](https://www.mathworks.com/help/matlab/matlab_prog/argument-validation-functions.html), enclosed in braces)
  - It is possible to specify a default value in the argument declaration. Please note that this will render the argument optional:
    all optional arguments must be positioned after required arguments. MATLAB will then use the default value when the argument is not included in the function call.

``` matlab
function out = myFunction(A, B, C)  
%  This mockup function takes input A, B, C and returns nothing

arguments
    A double
    B (1,3) cell {mustBeNonempty}
    C (1,1) double {mustBeNumeric, mustBeNonnegative} = 1
end

% Function code
...
end

```

## 4.n. Input parsing and processing
Separate data input or data parsing functions from data processing functions (see also 4.j.).

## 4.o. Processing and output
Separate data output or output formatting functions from data processing or computational functions.

## 4.q. Simple classes
Keep classes simple. If a class seems too big, refactor it into smaller classes, though be careful to avoid redundancy or overlap between classes. Only define necessary methods and properties.

## 4.r. Class properties
Keep properties private where possible. Define methods to modify or access properties with appropriate validation and update linked behaviours.

## 4.s. Class methods
Overload standard functions in place of custom named methods to provide consistent and recognisable behaviour between objects.


# MATLAB Style, Part 5: Errors and warnings

## 5.a. Expect errors
Expect and catch errors early and often. Use `try ... catch` to handle or resolve errors at a low-level before raising the error to a higher scope.

## 5.b. Warnings and errors
Use `warning` when the remainder of the function scope can still complete without error, but when the output may be affected. Some example cases for warnings might be numerical stability, missing data fields, ignored imaginary number components, or even . Use `error` whenever continued function execution would cause further errors, or when the output would be rendered incorrect or unusable.

## 5.c. Assertions
Use `assert` in place of an `if ..., error` sequence unless additional teardown logic is required before halting.

## 5.d. Displaying warnings
Never use `disp`, `fprintf` or similar in place of `warning`.

## 5.e. Informative errors
Make error and warning messages informative, and always include a message ID for additional context and to allow selective disabling and error verification. The message ID should contain the function name, local function name (if applicable), and  short error code, while the message itself should be a short descriptive sentence.

```matlab
% example warning and error
warning('jacobian:outOfRange', 'Joint positions are outside of robot limits.')
error('myMathFunction:mySquareRoot:mustBePositive', 'The input to mySquareRoot must be positive.')

% a warning ID can be used to selectively disable a warning
warning('off', 'jacobian:outOfRange')

% an error ID can be used to verify the expected error in a test context
testCase.verifyError(@() myMathFunction(-1), 'myMathFunction:mySquareRoot:mustBePositive')

```


# MATLAB Style, Part 6: Tests

**General**

## 6.a. Test files
Create a separate test file for every public function or class. Do not write tests within the program code itself.

## 6.b. Test names
Name a test file the same as the function or class it is testing with a `test_` prefix, and save it in the same directory. For example, `test_calculateResidual.m` should exist in the same directory as the `calculateResidual.m` function it is testing.

## 6.c. Test format
Test files should be evaluated with the [`runtests`](https://uk.mathworks.com/help/matlab/ref/runtests.html) function, and therefore must comply with the standard format for [function-based](https://uk.mathworks.com/help/matlab/function-based-unit-tests.html) or [class-based](https://uk.mathworks.com/help/matlab/class-based-unit-tests.html) unit tests.

## 6.d. Test scope
Keep tests small and uncoupled. In general, each section of test code should include its own setup, evaluation, and cleanup. Write a high level test execution function, and use subfunctions for each test case.

## 6.e. Test cases
Test expected edge cases, errors and exceptions.


# MATLAB Test Guide

Writing tests can seem tedious and unnecessary, particularly for small and simple functions. But, even a simple function can be misinterpreted and have unintended behaviour when used by different people and projects. Test code demonstrates to reviewers that the implementing author has considered the success and failure modes of a function, and in many cases can serve as a usage example. Ultimately, good test code helps the author design clear input / output interfaces in their implementations and accelerates the review cycle.

In this section, the important elements of the MATLAB testing framework are described, along with some examples on writing and running test code.

## The MATLAB test framework

This section is just a summary of the elements of a function unit test. Please see the MATLAB documentation on [function-based](https://uk.mathworks.com/help/matlab/function-based-unit-tests.html) or [class-based](https://uk.mathworks.com/help/matlab/class-based-unit-tests.html) unit tests for more detail.

As specified in the style guide, a test file should be created with the same name as the function it is testing, with the added `test_` prefix. The file should also be saved in the same location as the function to be tested. Every main test function should begin as follows:

```matlab
function tests = test_myFunction
    tests = functiontests(localfunctions);
end

```

Here, `functiontests` is the mechanism that will handle setup and teardown of the test framework, evaluate each test case within the file, and generate a test result structure. `localfunctions` is simply used to provide `functiontests` with handles to the local functions of the test file.

**Test fixtures**

Below the main function definition, local "fixture" functions can be added. A fixture is a specific state, condition or set of variables that ensures tests are decoupled from the surrounding environment. **Setup** fixtures happen in advance of tests and ensure that they always start with the same context, while **teardown** fixtures happen after tests and ensure that the surrounding environment or scope is unaffected.

**File fixtures** are routines that happen once for the entire test file, while **fresh fixtures** are evaluated again for each local test. The following standard fixtures are available to use:

```matlab
% file setup fixture, evaluated once before any test starts
function setupOnce(testCase)
    % example uses:
    % change directory or add to path
    % create temporary files and folders
    % ...
end

% file teardown fixture, evaluated once after all test finish
function teardownOnce(testCase)
    % example uses:
    % reset original directory
    % close figures and files
    % delete temporary files and folders
    % ...
end

% fresh setup fixture, evaluated before every test
function setup(testCase)
    % prepare a specific file, figure or path
    % re-initialise a shared variable
end

% fresh teardown fixture, evaluated after every test
function teardown(testCase)
    % reset an open figure
    % clear a modified file
end

```

Only include the fixtures that your test file needs - if they are empty, they can be removed.

**Local tests**

After the fixtures are defined, the local test functions can be added. They must begin or end with `test` for `runfunctions` to handle them correctly. For consistency, the recommended naming for a `test_myFunction` file is `testMyFunction[Case]`, where `[Case]` is a specific local test. For example:

````matlab
function testMyFunctionSuccess(testCase)
    % specific test code
end

function testMyFunctionInvalidInputs(testCase)
    % specific test code
end

````

**Test methods and qualifications**

The input argument to each of these local tests and fixtures  is `testCase`, an instance of a [`FunctionTestCase`](https://uk.mathworks.com/help/matlab/ref/matlab.unittest.functiontestcase-class.html). `testCase` is generated by `functiontests`, and is passed to every local function. If a local function never accesses `testCase`, replace the argument with a tilde, i.e. `setup(~)`.

The two main uses for `testCase` are to share data between local functions, and to provide testing methods in the correct context.

For sharing data, `testCase` contains a `TestData` field, which can be populated with any data. For example, you might specify `testCase.TestData.path = pwd` in the `setupOnce` function before changing directory. Then, you can revert to the original directory in `teardownOnce` using `cd(testCase.TestData.path)`.

The `testCase` object also contains test methods. Test methods compare function behaviour to some expected behaviour in specific ways, such as checking equality, type, size, or errors. Each of these methods has variants that determine the effect of test failure, known as "qualifications", The MATLAB testing framework provides four types of testing qualifications:

- Verifications: Produce and record failures without throwing an exception, meaning the remaining tests run to completion. Test methods use the `verify` prefix.
- Assumptions: Ensure that a test runs only when certain preconditions are satisfied and the event should not produce a test failure. When an assumption failure occurs, the testing framework marks the test as filtered. Test methods use the `assume` prefix.
- Assertions: Ensure that the preconditions of the current test are met. Test methods use the `assert` prefix.
- Fatal assertions: Use this qualification when the failure at the assertion point renders the remainder of the current test method invalid or the state is unrecoverable. Test methods use the `fatalAssert` prefix.

Below are some commonly used test methods. For a full breakdown of available options, see the [table of verifications, assertions and other qualifications](https://uk.mathworks.com/help/matlab/matlab_prog/types-of-qualifications.html).

```matlab
% most methods are clear logical conditions
testCase.verifyEqual(a, b)
testCase.verifyGreaterThan(c, d)
testCase.verifyInstanceOf(5.0, 'double')

% the error method takes a handle to the function and expects
% a specific error ID to be thrown
testCase.verifyError(@() myFun(a,b), 'myFun:myErrorCode')

% if an assumption fails, the rest of the local test will be skipped
testCase.assumeTrue(isfield(S, 'field'))
% in this case the previous assumption ensures that accessing the field
% will not cause an unhandled test error
testCase.verifySize(S.field, [2, 3])

```

To experiment with the `testCase` object and its associated test methods outside of the test function, an instance can be created in the MATLAB prompt:  `testCase = matlab.unittest.TestCase.forInteractiveUse;`

## Recommendations for writing tests

Writing test code can be straightforward, provided you know where to start and when to stop.

There's not much point writing redundant and unnecessary test code just for the sake of it. It's rarely feasible to test every value and combination of supported inputs, particularly for functions with real-valued, continuous inputs. It's equally difficult to cover every combination of *unsupported* inputs.

This section contains an implementation guide for effective and well scoped tests. The following function will be used as an example:

```matlab
function u = normalise(v)
% normalise
%   u = normalise(v) takes a vector input v,
%  and returns a unit direction vector u

arguments
    v double {mustBeNumeric, mustBeNonempty}
end

u = v ./ norm(v);
end

```

To begin, create a `test_normalise` file with the appropriate heading:

```matlab
function tests = test_normalise
    tests = functiontests(localfunctions)
end

```

To create the test body, proceed in the following order:

1) Test that the function completes without errors under a representative use-case.

```matlab
function testNormaliseVector(~)
    normalise([1, 2, 3]);
end

```

2) Test that values returned by the function have the expected properties (size, type, structure) depending on the input arguments. Here, the concern is not the returned *value* itself, but rather the properties. This decouples the structural elements of the tested function from the numerical or logical behaviour.

```matlab
function testNormaliseDimensions(testCase)
    v = [1, 2, 3];
    u = normalise(v);
    testCase.verifySize(u, size(v));

    v = [4, 5]';
    u = normalise(v);
    testCase.verifySize(u, size(v));
end

```

3) Test that the input validation of the function correctly handles unsupported arguments. Prioritise cases that are likely to occur. It is not necessary to include unrealistic or unlikely input combinations.

```matlab
function testNormaliseUnsupportedInputs(testCase)
    e = [];
    testCase.verifyError(@() normalise(e), 'MATLAB:expectedVector');
    M = [1, 2; 3, 4];
    testCase.verifyError(@() normalise(M), 'MATLAB:expectedVector');

    % this is a valid but unnecessary test case
    s = "vector";
    testCase.verifyError(@() normalise(s), 'MATLAB:invalidType');
end

```

4) Finally, test the behaviour of specific real-valued inputs and edge-cases.

```matlab
function testNormaliseSpecificCases(testCase)
    v = [1, 2, 3];
    u = normalise(v);
    testCase.verifyEqual(u, [0.2673, 0.5345, 0.8018], 'AbsTol', 1e-3);

    v = [0, 0, 0];
    u = normalise(v);
    testCase.verifyEqual(u, nan(size(v)));
end

```

After writing the test cases in this order, it might become clear where common setup and teardown fixtures can be used. Add these as appropriate. In some cases, a local test can handle multiple conditions, but be sure to keep the scope of each local test to a specific condition, so that any test failure is simple to fix.

The full test code might ultimately look as follows:

```matlab
function tests = test_normalise
    tests = functiontests(localfunctions)
end

function setupOnce(testCase)
    testCase.TestData.testVec = [1, 2, 3];
    testCase.TestData.normalisedVec = [0.2673, 0.5345, 0.8018];
    testCase.TestData.tol = 1e-3;
end

function testNormaliseVector(testCase)
    % check succesful evaluation
    normalise(testCase.TestData.vec);
end

function testNormaliseDimensions(testCase)
    % check dimensionality is preserved
    a = [1, 2];
    u = normalise(a);
    testCase.verifySize(u, size(a));

    b = [-3; -4; -5; -6]';
    u = normalise(b);
    testCase.verifySize(u, size(b));
end

function testNormaliseUnsupportedInputs(testCase)
    % check 0D and 2D input sizes are not supported
    e = [];
    testCase.verifyError(@() normalise(e), 'MATLAB:expectedVector');
    M = [1, 2; 3, 4];
    testCase.verifyError(@() normalise(M), 'MATLAB:expectedVector');
end

function testNormaliseSpecificCases(testCase)
    % check that the normalised vector elements have the expected value
    u = normalise(testCase.TestData.testVec);
    testCase.verifyEqual(u, testCase.TestData.normalisedVec, ...
        'AbsTol', testCase.TestData.tol);
    testCase.verifyEqual(norm(u), 1, testCase.TestData.tol);

    % check that zero length vector returns a NaN vector
    testCase.verifyEqual(normalise([0, 0, 0]), nan(size(v)));
end

```


## Running tests

In the MATLAB command prompt, evaluate all tests in the repository by navigating to the top-level directory and using the command `runtests(pwd,'IncludeSubfolders',true)`. As long as the test files are correctly named and stored with their respective source functions, the test runner will automatically step through all directories and tests in the repo.

Alternatively, evaluate only the tests in the current directory by using the command `runtests`, or selectively evaluate a single test using `runtests test_myFunction`, where `test_myFunction.m` is on the MATLAB path.

Using `runtests` displays test progress and returns a [`TestResult`](https://uk.mathworks.com/help/matlab/ref/matlab.unittest.testresult-class.html) array, which contains data and details of each evaluated test as well as a summary of test outcomes. An example successful TestResult will contain the following summary:

```
Totals:
   3 Passed, 0 Failed, 0 Incomplete.
   0.010467 seconds testing time.
```


**Command line testing**

If you want to evaluate tests without opening the MATLAB desktop application, you can use the following command line syntax:

```shell
/path/to/matlab -nodesktop -nosplash -sd /path/to/control_repo -batch "runtests(pwd,'IncludeSubfolders',true)"
```

Replace `/path/to/matlab` with the respective launcher path or prompt according to [MacOS](https://uk.mathworks.com/help/matlab/ref/matlabmacos.html), [Linux](https://uk.mathworks.com/help/matlab/ref/matlablinux.html) or [Windows](https://uk.mathworks.com/help/matlab/ref/matlabwindows.html) installation, and replace `/path/to/control_repo` with the path to the local copy of this repository.
