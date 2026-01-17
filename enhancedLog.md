# CallerInformation enrichers
Standard Konfiguration um im Log Aufrufer und Zeilennummer angezeigt zu bekommen.
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

# Ausgabe
[12:34:56 INF] Verbindung hergestellt  
(in MyService.Connect Service.cs:42)
