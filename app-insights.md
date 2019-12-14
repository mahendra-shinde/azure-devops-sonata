App Insights in ASP.NET Core Web Applications

1. Add NuGet Dependency "Microsoft.AppInsights.AspNetCore"
2. Added Instrumentation key inside "appsettings.json" file
 "ApplicationInsights": {
    "InstrumentationKey": "e44945c5-14ac-4797-97e4-97d51ed2365a"
  },
3. Modify "Startup.cs" file

	  public void ConfigureServices(IServiceCollection services)
        {
            services.Configure<CookiePolicyOptions>(options =>
            {
                // This lambda determines whether user consent for non-essential cookies is needed for a given request.
                options.CheckConsentNeeded = context => true;
                options.MinimumSameSitePolicy = SameSiteMode.None;
            });
		//***Add following line ***//
            services.AddApplicationInsightsTelemetry();
		//*** thats all ***///
            services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
        }
