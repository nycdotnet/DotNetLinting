# .NET Linting
An actionable rant on .NET linting rules.

References:
  * [Roslyn Analyzers](https://learn.microsoft.com/en-us/visualstudio/code-quality/use-roslyn-analyzers?view=vs-2022)
  * [C# Formatting Options](https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/style-rules/csharp-formatting-options)

# General Principles

1. As a developer is working, they naturally create "bugs" as they type which will be resolved by the time they finish typing.  It is distracting and counter-productive to display errors that are likely to be fixed in a moment while the developer is working.

## CA1822: Member does not access instance data and can be marked as static
Default: `error` 👎

This is a reasonable rule and should be raised to the developer.  However, it makes no sense to have this be an error.  It is very common for a method to be implemented during a development cycle which does not use any instance data *yet* but will in the immediate future - even within the same dev cycle.  It also boxes the programmer into an API corner.  The performance benefit could be real, and I am certainly a fan of pure functional programming when possible, therefore this rule should never be higher than a suggestion.

```
dotnet_diagnostic.CA1822.severity = suggestion
```

## IDE0005: Using directive is unnecessary.
Default: `error` 👎

This should be cleaned up but there is no way this should be an error.

```
dotnet_diagnostic.IDE0005.severity = warning
```

## IDE0058: Expression value is never used
Default: `error` ☣️

This breaks C# and causes you to add `_ =` all over your code base.  The people who created this rule hate you and especially hate your tidy code base.

```
dotnet_diagnostic.IDE0058.severity = none
```

## IDE0059: Unnecessary assignment of a value to variable
Default: `error` ☣️

This is an insane rule - any new variable that you create will have this "error" immediately.  This rule makes C# more like Golang which means it makes it worse.

```
dotnet_diagnostic.IDE0059.severity = suggestion
```

## IDE2000: Avoid multiple blank lines
Default `error` 🚒

The rule is generally a good one but the default severity is completely unreasonable because it gets in the way while a developer is working.  It is also a duplicate with SA1507.

```
dotnet_diagnostic.IDE2000.severity = warning
```


## IDE2003: Blank line required between block and subsequent statement
Default `error` 🚒

The rule is generally a good one but the default severity is unreasonable because it gets in the way while a developer is working.

```
dotnet_diagnostic.IDE2003.severity = suggestion
```

## S1854: Remove this useless assignment to variable
Default `error` 🚒

This rule in particular causes breaks while using hot reload with modern .NET.  It is well intentioned but should be a warning.  This is implemented by the SonarAnalyzer.

```
dotnet_diagnostic.S1854.severity = warning
```

## S4457: Split this method in two, one handling the parameters check and one handling the async code
Default `error` 🚒

This rule can make sense if you're doing a fire and forget sort of thing (aka not `await`ing on the Task) but it's generally not interesting and can lead to code sprawl.

```
dotnet_diagnostic.S4457.severity = suggestion
```

## SA1009: Closing parenthesis should not be preceded by a space
Default `error` ☣️

This is a whitespace opinion and can be implemented automatically - therefore it should not be an error.

```
dotnet_diagnostic.SA1009.severity = suggestion
```

## SA1028: Code should not contain trailing whitespace
Default `error` 🚒

This is a whitespace opinion and can be implemented automatically - therefore it should not be an error.

```
dotnet_diagnostic.SA1028.severity = warning
```

## SA1111: Closing parenthesis should be on line of last parameter
Default `error` ☣️

This is a whitespace opinion and can be implemented automatically - therefore it should not be an error.

```
dotnet_diagnostic.SA1111.severity = suggestion
```

## SA1116: The parameters should begin on the line after the declaration, whenever the parameter spans across multiple lines

Default `error` ☣️

This is a whitespace opinion and can be implemented automatically - therefore it should not be an error.

```
dotnet_diagnostic.SA1116.severity = suggestion
```

## SA1117: The parameters should all be placed on the same line or each parameter should be placed on its own line

Default `error` ☣️

This is a whitespace opinion and can be implemented automatically - therefore it should not be an error.

```
dotnet_diagnostic.SA1117.severity = suggestion
```

## SA1122: Use `string.Empty` for empty strings

Default `error` ☣️

This is literally from a performance bug in .NET 1.0 where the compiler couldn't optimize uses of "" and so many empty strings would get allocated.  This was fixed in .NET 1.1 more than 20 years ago, and there is no benefit to use `string.Empty` except to make your code longer.  It is toxic to make this an error.

```
dotnet_diagnostic.SA1122.severity = none
```

## SA1202: Elements must be ordered by access
Default `error` ☣️

This is a completely unreasonable rule in C#.  This is a holdover from other programming languages where there was a line which separated public from private.  This is a completely useless rule and it should be suppressed.

```
dotnet_diagnostic.SA1202.severity = none
```

## SA1204: Static elements must appear before instance elements
Default `error` 🚒

This is a completely unreasonable rule in C# and harms the ability to follow differences in a file in source control.  One might want their IDE to auto-implement this change, in theory, so this rule can be allowed to exist as a suggestion only.

```
dotnet_diagnostic.SA1204.severity = suggestion
```

## SA1413: Use trailing comma in multi-line initializers
Default `error` ☣️

This is a preposterous idea that came over from JavaScript.  The idea is that in future commits you will only have one line to change if you add something to a list.  It is optimizing a theoretical future for the actual present.

```
dotnet_diagnostic.SA1413.severity = none
```

## SA1505: An opening brace should not be followed by a blank line
Default `error` 🚒

This is a fine idea but it is insane to make this an error while a developer is working.

```
dotnet_diagnostic.SA1505.severity = suggestion
```

## SA1507: Code should not contain multiple blank lines in a row
Default `error` 🚒

The rule is generally a good one but the default severity is completely unreasonable because it gets in the way while a developer is working.  It is also a duplicate with IDE2000.

```
dotnet_diagnostic.SA1507.severity = suggestion
```

## SA1508: A closing brace should not be preceeded by a blank line
Default `error` 🚒

This is a whitespace opinion and can be implemented automatically - therefore it should not be an error.

```
dotnet_diagnostic.SA1508.severity = suggestion
```

## SA1513: Closing brace should be followed by blank line
Default `error` ☣️

This is a whitespace opinion and can be implemented automatically - therefore it should not be an error.  This one also has a bad interaction with the new collection syntax in C# (`[]`), so it should just be disabled.

```
dotnet_diagnostic.SA1513.severity = none
```

## SA1515: Single-line comments should be preceded by blank line
Default `error` ☣️

This is a whitespace opinion and can be implemented automatically - therefore it should not be an error.  This is particularly toxic in multi-property object initializers when trying to explain why something is set to the value it is.

```
dotnet_diagnostic.SA1516.severity = none
```

## SA1516: Elements should be separated by blank line
Default `error` ☣️

This is a whitespace opinion and can be implemented automatically - therefore it should not be an error.

```
dotnet_diagnostic.SA1516.severity = suggestion
```

## SA1518: File is required to end with a single newline character
Default `error` ☣️

This is a whitespace opinion and can be implemented automatically - therefore it should not be an error.

```
dotnet_diagnostic.SA1518.severity = suggestion
```

## SA1629: Documentation text should end with a period
Default `error` ☣️

This is an outrage.  This is not Golang which requires stupid comments even on obvious code, and of course it's not smart enough to understand URLs or other technical things that might get corrupted by the addition of a period.  Utterly trash.

```
dotnet_diagnostic.SA1518.severity = none
```

## SA1642: Constructor summary documentation should begin with standard text
Default `error` ☣️

This could be even worse than SA1629.  It's a constructor - obviously it creates an instance of the relevant class or struct.  What bloat!!  This is not Golang.

```
dotnet_diagnostic.SA1642.severity = none
```

## C# New Line Before

There was a bug in the ASP.NET Templates for a while which caused else and finally blocks to want to collapse.  While in my opinion, `} else {`, which is preferred in the JS world is totally fine, having a line feed after the else, but not before it pleases no one.  I think C# should use the tall formatting that it has always had.

```
csharp_new_line_before_open_brace = all
csharp_new_line_before_else = true
csharp_new_line_before_catch = true
csharp_new_line_before_finally = true
```

It should be noted that I believe this problem is somewhat widespread due to the settings in the default .editorconfig distributed with the Visual Studio templates.  In the ASP.NET repo at least, this issue [has been corrected](https://github.com/dotnet/aspnetcore/blob/1a9343b510b37451d99338552d64b7bf8d75d597/.editorconfig#L46-L48) at least.
