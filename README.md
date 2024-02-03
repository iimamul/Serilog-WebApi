# Getting Started with Serilog and WebAPI
[Serilog Docs](https://serilog.net/)
- From serilog documentation first find out the [serilog documentation for AspnetCore](https://github.com/serilog/serilog-aspnetcore#serilogaspnetcore---) because that one is needed for WebApi.
- Install the *Serilog.AspNetCore* package with following cmd or from nuget package manager:
	```bash
	dotnet add package Serilog.AspNetCore
	```

- Implement the example in the documentation, then move the configuration to the *appsettings.json* file following [serilog-settings configuration](https://github.com/serilog/serilog-settings-configuration).
- After all the configuration done in *Program.cs* then just do `Log.Information()` inside the controller.
	```cs
	public IEnumerable<WeatherForecast> Get()
	{
	    var forcasts = Enumerable.Range(1, 5).Select(index => new WeatherForecast
	    {
	        Date = DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
	        TemperatureC = Random.Shared.Next(-20, 55),
	        Summary = Summaries[Random.Shared.Next(Summaries.Length)]
	    })
	    .ToArray();
			//Log forcast data
	    Log.Information("Weather Forcasts: {@forc}", forcasts);
	
	    return forcasts;
	}
	```
>The `@` operator in front of `forc` tells Serilog to serialize the object passed in, rather than convert it using `ToString()`.

