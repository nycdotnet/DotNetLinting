# .NET Linting
An actionable rant on .NET linting rules

## CA1822: Member does not access instance data and can be marked as static
Default: `error` 👎

This is a reasonable rule and should be fixed.  However, it makes no sense to have this be an error.  It is very common for a method to be implemented during a development cycle which does not use any instance data *yet* but will in the immediate future - even within the same dev cycle.  Therefore this rule should never be higher than a warning.

```
dotnet_diagnostic.CA1822.severity = warning
```

## SA1202: Elements must be ordered by access
Default `error` 🚒

This is a completely unreasonable rule in C#.  This is a holdover from other programming languages where there was a line which separated public from private.  This is a completely useless rule and it should be suppressed.

```
dotnet_diagnostic.SA1204.severity = none
```

## SA1204: Static elements must appear before instance elements
Default `error` 🚒

This is a completely unreasonable rule in C# and harms the ability to follow differences in a file in source control.

```
dotnet_diagnostic.SA1204.severity = suggestion
```
