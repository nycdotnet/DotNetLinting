# .NET Linting
An actionable rant on .NET linting rules.

References:
  * [Roslyn Analyzers](https://learn.microsoft.com/en-us/visualstudio/code-quality/use-roslyn-analyzers?view=vs-2022)
  * [C# Formatting Options](https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/style-rules/csharp-formatting-options)

# General Principles

1. As a developer is working, they naturally create "bugs" as they type which will be resolved by the time they finish typing.  It is distracting and counter-productive to display errors that are likely to be fixed in a moment while the developer is working.

## CA1822: Member does not access instance data and can be marked as static
Default: `error` 👎

This is a reasonable rule and should be fixed.  However, it makes no sense to have this be an error.  It is very common for a method to be implemented during a development cycle which does not use any instance data *yet* but will in the immediate future - even within the same dev cycle.  It also boxes the programmer into an API corner.  The performance benefit could be real, and I am certainly a fan of pure functional programming when possile, therefore this rule should never be higher than a suggestion.

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

## IDE2000: Avoid multiple blank lines
Default `error` 🚒

The rule is generally a good one but the default severity is completely unreasonable because it gets in the way while a developer is working.  It is also a duplicate with SA1507.

```
dotnet_diagnostic.IDE2000.severity = warning
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
dotnet_diagnostic.SA1204.severity = none
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
