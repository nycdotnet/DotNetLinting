# .NET Linting
An actionable rant on .NET linting rules

# General Principles

As a developer is working, they naturally create "bugs" as they type which will be resolved by the time they finish typing.  It is distracting and counter-productive to display errors that are likely to be fixed in a moment while the developer is working.

## CA1822: Member does not access instance data and can be marked as static
Default: `error` 👎

This is a reasonable rule and should be fixed.  However, it makes no sense to have this be an error.  It is very common for a method to be implemented during a development cycle which does not use any instance data *yet* but will in the immediate future - even within the same dev cycle.  It also boxes the programmer into an API corner.  The performance benefit could be real, and I am certainly a fan of pure functional programming when possile, therefore this rule should never be higher than a suggestion.

```
dotnet_diagnostic.CA1822.severity = suggestion
```

## SA1202: Elements must be ordered by access
Default `error` 🗑️

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

## SA1505: An opening brace should not be followed by a blank line
Default `error` 🚒

This is a fine idea but it is insane to make this an error while a developer is working.

```
dotnet_diagnostic.SA1505.severity = warning
```

