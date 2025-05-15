---
description: Test your functions!
icon: flask
---

# Test Fixtures

CliTester is easy to use, but this page talks about the usage of this library to be able to use it in your console application.

## Fixture types

CliTester provides functionality that allows you to define test fixtures that are of the following types:

* Unconditional fixtures: Test fixtures that fall into this category tests against functions that don't return a value (that is, returning `void`).
* Conditional fixtures: Test fixtures that fall into this category tests against functions that return a value (that is, returning a value other than `void`).

### Unconditional fixtures

Fixtures that don't compare the returned value with the expected value and that the function being tested returns `void` are unconditional fixtures. This type can be created using the constructor of either a generic version of the `FixtureUnconditional` class (i.e. you are required to provide a delegate type that returns `void`, such as `Action` or `Action<string>`) or a non-generic one for dynamic usage.

Unconditional fixtures can be defined like these example declarations:

```csharp
// Using a generic version
var genericNoArgs   = new FixtureUnconditional<Action>(nameof(UnconditionalFunctions.TestWrite), "Tests writing to console", UnconditionalFunctions.TestWrite);
var genericWithArgs = new FixtureUnconditional<Action<string>>(nameof(UnconditionalFunctions.TestWriteArgs), "Tests writing to console with arguments", UnconditionalFunctions.TestWriteArgs, "John");

// Using a non-generic version
var dynamicNoArgs   = new FixtureUnconditional(nameof(UnconditionalFunctions.TestWrite), "Tests writing to console", UnconditionalFunctions.TestWrite);
var dynamicWithArgs = new FixtureUnconditional(nameof(UnconditionalFunctions.TestWriteArgs), "Tests writing to console with arguments", UnconditionalFunctions.TestWriteArgs, "John");
```

Taking into consideration the example target functions that are defined in the `UnconditionalFunctions` static class like this:

```csharp
internal static void TestWrite()
{
    Console.WriteLine("Console.WriteLine is called");
    Console.WriteLine("Hello world!");
}

internal static void TestWriteArgs(string name)
{
    Console.WriteLine("Console.WriteLine is called with arguments");
    Console.WriteLine($"Hello, {name}!");
}
```

### Conditional Fixtures

In the other hand, fixtures that compare the returned value with the expected value and that the function being tested has a return value are conditional fixtures. This type can be created using the constructor of either a generic version of the `FixtureConditional` class (i.e. you are required to provide a delegate type that supports return value, such as `Func<int>` or `Func<double, double, double>`) or a non-generic one for dynamic usage.

Unconditional fixtures can be defined like these example declarations:

```csharp
// Using a generic version
var genericNoArgs   = new FixtureConditional<Func<int>>(nameof(ConditionalFunctions.TestRead), "Tests reading from console", ConditionalFunctions.TestRead, (int)'A');
var genericWithArgs = new FixtureConditional<Func<double, double, double>>(nameof(ConditionalFunctions.TestReadArgs), "Tests reading from console with arguments", ConditionalFunctions.TestReadArgs, 0d, 4, 2);

// Using a non-generic version
var dynamicNoArgs   = new FixtureConditional<Func<int>>(nameof(ConditionalFunctions.TestRead), "Tests reading from console", ConditionalFunctions.TestRead, (int)'A');
var dynamicWithArgs = new FixtureConditional(nameof(ConditionalFunctions.TestReadArgs), "Tests reading from console with arguments", ConditionalFunctions.TestReadArgs, 0d, 4, 2);
```

Taking into consideration the example target functions that are defined in the `ConditionalFunctions` static class like this:

```csharp
internal static int TestRead()
{
    Console.WriteLine("Console.Read is called. Write 'A' in uppercase");
    int charNum = Console.Read();
    return charNum;
}

internal static double TestReadArgs(double dividend, double divisor) =>
    dividend % divisor;
```

## Running the fixtures

When you need to run the fixtures, you'll need to take these tips into account:

*   Unconditional tests that are defined using the generic version of the `FixtureUnconditional` class can be run using the `RunTest<TDelegate>()` function in the `FixtureRunner` static class.



    ```csharp
    var fixture = new FixtureUnconditional<Action>(nameof(UnconditionalFunctions.TestWrite), "Tests writing to console", UnconditionalFunctions.TestWrite);
    bool result = FixtureRunner.RunTest(fixture, out var exc);
    ```


*   Unconditional tests that are defined using the non-generic version of the `FixtureUnconditional` class can be run using the `RunUnconditionalTest()` function in the fixture runner class.



    ```csharp
    var fixture = new FixtureUnconditional(nameof(UnconditionalFunctions.TestWrite), "Tests writing to console", UnconditionalFunctions.TestWrite);
    bool result = FixtureRunner.RunUnconditionalTest(fixture, out var exc);
    ```


*   Conditional tests that are defined using the generic version of the `FixtureConditional` class can be run using the `RunTest<TDelegate, TValue>()` function in the `FixtureRunner` static class, but you are required to provide both the delegate type and the value type in the `RunTest()` type parameters.



    ```csharp
    var fixture = new FixtureConditional<Func<int>>(nameof(ConditionalFunctions.TestRead), "Tests reading from console", ConditionalFunctions.TestRead, (int)'A');
    bool result = FixtureRunner.RunTest<Func<int>, int>(fixture, out var exc);
    ```


*   Conditional tests that are defined using the non-generic version of the `FixtureConditional` class can be run using the `RunConditionalTest<TValue>()` function in the `FixtureRunner` static class, but you are required to provide the value type in the `RunConditionalTest()` type parameter.



    ```csharp
    var fixture = new FixtureConditional<Func<int>>(nameof(ConditionalFunctions.TestRead), "Tests reading from console", ConditionalFunctions.TestRead, (int)'A');
    bool result = FixtureRunner.RunConditionalTest<int>(fixture, out var exc);
    ```


*   Test fixtures can also be run with the `RunGeneralTest()` function if you don't know whether the fixture is unconditional or conditional.



    ```csharp
    var fixture = new FixtureConditional<Func<double, double, double>>(nameof(ConditionalFunctions.TestReadArgs), "Tests reading from console with arguments", ConditionalFunctions.TestReadArgs, 0d, 4, 2);
    bool result = FixtureRunner.RunGeneralTest(fixture, out var exc);
    ```



All the fixture runners return a Boolean value indicating whether the test passed or failed. If the test has passed, then the exception output parameter value is `null`. Otherwise, it's populated with exception information that tells you what happened.

## Fixture selector

To be able to make your console demo application more interactive, you can leverage the use of the fixture selector function that allows the end user to select a test fixture from the full-screen menu. This requires making a new array of type `Fixture[]` that stores all the test fixtures that you want. An example of array declaration of all the test fixtures (unconditional or not) is:

```csharp
Fixture[] fixtures =
[
    new FixtureUnconditional<Action>(nameof(UnconditionalFunctions.TestWrite), "Tests writing to console", UnconditionalFunctions.TestWrite),
    new FixtureUnconditional<Action<string>>(nameof(UnconditionalFunctions.TestWriteArgs), "Tests writing to console with arguments", UnconditionalFunctions.TestWriteArgs, "John"),
    new FixtureConditional<Func<int>>(nameof(ConditionalFunctions.TestRead), "Tests reading from console", ConditionalFunctions.TestRead, (int)'A'),
    new FixtureConditional<Func<double, double, double>>(nameof(ConditionalFunctions.TestReadArgs), "Tests reading from console with arguments", ConditionalFunctions.TestReadArgs, 0d, 4, 2),
    new FixtureConditional<Func<double, double, double>>(nameof(ConditionalFunctions.TestReadArgs) + "Fail", "Tests reading from console with arguments (failure expected)", ConditionalFunctions.TestReadArgs, 0d, 5, 2),
];
```

After that, you can use this variable to launch the fixture selector like this:

```csharp
FixtureSelector.OpenFixtureSelector(fixtures);
```

If you've defined all the test fixtures correctly, you should now see a menu that looks similar to this:

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

For each test, there is a status box that indicates whether the test has been run, has succeeded, or has failed.

* `[ ]`: For tests that are yet to run, this is shown.
* `[*]`: For tests that have succeeded, this is shown.
* `[X]`: For tests that have failed, this is shown.

You can press ENTER to start a test fixture. If the test has succeeded, you'll get a green text saying that the test has passed. If the test has failed, you'll get a red text saying that the test has failed with an error message that may tell you why.

{% hint style="info" %}
The fixture selector requires a working terminal which meets [Terminaux](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-checker)'s requirements.
{% endhint %}
