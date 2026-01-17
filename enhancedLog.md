# CallerInformation enrichers
```
dotnet add package Serilog.Enrichers.CallerInformation
```

``` csharp
using Serilog;
using Serilog.Enrichers.CallerInformation;

Log.Logger = new LoggerConfiguration()
    .Enrich.WithCallerInformation(
        includeFileInfo: true,   // nötig für Zeilennummer
        allowedAssemblies: new[] { "DeinProjekt" }
    )
    .WriteTo.Console(
        outputTemplate:
        "[{Timestamp:HH:mm:ss} {Level:u3}] {Message} " +
        "(in {CallerType}.{CallerMember} " +
        "{CallerFilePath}:{CallerLineNumber}){NewLine}{Exception}"
    )
    .CreateLogger();
```

