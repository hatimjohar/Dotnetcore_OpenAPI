<h2> How to add Open API documentation (Swagger documentation) to your API in ASP.NET Core Web API </h2>
This article describes the way through which we can learn how to add a documentation to your webapi using Open API specification in dotnet core based webapi project

<h2>What is Open API</h2>
Open API is an description format for REST based API, it allows us to describe our api with <br/>

- [x] Endpoint definition along with request type like (GET / POST etc...)
- [x] Input and Output request format

**Swagger** is a set of open source tools built around Open API specification and provides a clean html based UI to present api specs with the ability to try it as well

<h2> Lets start enabling swagger in our dotnet core api </h2>

<h3> Pre-requisites </h3>

- [x] .Net code sdk must be installed on your machine 
- [x] Editor like Visual Studio or Visual Studio Editor
- [x] Existing api solution created in dotnet core -- refer this git repo to know how to create web api https://github.com/hatimjohar/dotnetcore_webapi 

<h3> Step 1 - Add Swashbuckle package</h3>

Add Nugut package - Swashbuckle.AspNetCore

![alt text](http://url/to/img.png)

<h3> Step 2 - Update contents in startup.cs file</h3>

Firstly confugure Swagger middle ware by adding following content to the ConfigureServices method

```c#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);

    services.AddSwaggerGen(c =>
    {
        c.SwaggerDoc("v1", new Info { Title = "Dotnet core web api", Version = "v1" });
    });
}
```

In order to use Info class, we need to add following using **using Swashbuckle.AspNetCore.Swagger;**  <br/> 

Then add swagger UI endpoint for swagger in Congure method as shown below

```c#
 public void Configure(IApplicationBuilder app, IHostingEnvironment env)
  {
      if (env.IsDevelopment())
      {
          app.UseDeveloperExceptionPage();
      }

      app.UseSwagger();
      app.UseSwaggerUI(c =>
      {
          c.SwaggerEndpoint("/swagger/v1/swagger.json", "Dotnet core web api v1");
      });

      app.UseMvc();
  }
```

<h3> Finally run our application </h3>

Once your application is started, type the url in this fashion **http://localhost:port/swagger

![alt text](http://url/to/img.png)
