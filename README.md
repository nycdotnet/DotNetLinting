# .NET Linting
An actionable rant on .NET linting rules

## CA1822 Member does not access instance data and can be marked as static
This is a reasonable rule and should be fixed.  However, it makes no sense to have this be an error.  It is very common for a method to be implemented during a development cycle which does not use any instance data *yet* but will in the immediate future - even within the same dev cycle.  Therefore this rule should never be higher than a warning.

```
dotnet_diagnostic.CA1822.severity = warning
```
