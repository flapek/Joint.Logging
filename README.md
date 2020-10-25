# Joint.Logging

| Branch  | Build status                                                                                                                 |
| ------- | ---------------------------------------------------------------------------------------------------------------------------- |
| master  | [![Build Status](https://travis-ci.org/flapek/Joint.Logging.svg?branch=master)](https://travis-ci.org/flapek/Joint.Logging)  |
| develop | [![Build Status](https://travis-ci.org/flapek/Joint.Logging.svg?branch=develop)](https://travis-ci.org/flapek/Joint.Logging) |

## Logging

Adds the logging capability, by default uses [Serilog](https://serilog.net/) for logging with 3 optional extensions (sinks):

- Console
- File
- [Seq](https://datalust.co/seq)

## Installation

```
dotnet add package Joint.Logging
```

## Dependencies

- [Joint](https://www.nuget.org/packages/Joint/)
- [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/)
- [Serilog](https://www.nuget.org/packages/Serilog/)
- [Serilog.AspNetCore](https://www.nuget.org/packages/Serilog.AspNetCore/)
- [Serilog.Extensions.Logging](https://www.nuget.org/packages/Serilog.Extensions.Logging/)
- [Serilog.Sinks.Console](https://www.nuget.org/packages/Serilog.Sinks.Console/)
- [Serilog.Sinks.ElasticSearch](https://www.nuget.org/packages/Serilog.Sinks.Elasticsearch/)
- [Serilog.Sinks.File](https://www.nuget.org/packages/Serilog.Sinks.File/)
- [Serilog.Sinks.Seq](https://www.nuget.org/packages/Serilog.Sinks.Seq/)

## Usage

Extend `Program.cs` -> `CreateDefaultBuilder()` with `UseLogging()` that will add the required services and configure `ILogger` available in ASP.NET Core framework.

```c#
public static IWebHostBuilder GetWebHostBuilder(string[] args)
    => WebHost.CreateDefaultBuilder(args)
        .ConfigureServices(services => services.AddJoint().Build())
        .UseLogging();
```

Then, simply inject `ILogger<T>` (being ASP.NET Core built-in abstraction) to write the logs.

```c#
public class SomeService
{
    private readonly ILogger<SomeService> _logger;

    public SomeService(ILogger<SomeService> logger)
    {
        _logger = logger;
    }

    public void Foo()
    {
        _logger.LogInformation("Foo");
    }
}
```

## Options

- applicationName - sets the optional application name property used for log enrichment.
- serviceId - sets the optional service id property used for log enrichment.
- excludePaths - optional endpoints that should be excluded from logging (e.g. while performing the health checks by other services).
- console.enabled - enables/disables console logger.
- file.enabled - enables/disables file logger.
- file.path - path to the file logs.
- file.interval - how often should the new file with logs be created.
- seq.enabled - enables/disables Seq logger.
- seq.url - URL to Seq API.
- seq.token - API key (if provided) used while sending logs to Seq.

### appsettings.json

```json
"logger": {
  "applicationName": "some-service",
  "serviceId": "instance-1",
  "excludePaths": ["/ping", "/metrics"],
  "console": {
    "enabled": true
  },
  "file": {
    "enabled": true,
    "path": "logs/logs.txt",
    "interval": "day"
  },
  "seq": {
    "enabled": true,
    "url": "http://localhost:5341",
    "token": "secret"
  }
}
```

## Table of Contents

- [Joint](https://github.com/flapek/Joint)
- [Joint.Auth](https://github.com/flapek/Joint.Auth)
- [Joint.CQRS.Commands](https://github.com/flapek/Joint.CQRS.Commands)
- [Joint.CQRS.Events](https://github.com/flapek/Joint.CQRS.Events)
- [Joint.CQRS.Queries](https://github.com/flapek/Joint.CQRS.Queries)
- [Joint.DB.Mongo](https://github.com/flapek/Joint.DB.Mongo)
- [Joint.DB.Redis](https://github.com/flapek/Joint.DB.Redis)
- [Joint.Docs.Swagger](https://github.com/flapek/Joint.Docs.Swagger)
- [Joint.Exception](https://github.com/flapek/Joint.Exception)
- [Joint.Logging](https://github.com/flapek/Joint.Logging)
- [Joint.WebApi](https://github.com/flapek/Joint.WebApi)
