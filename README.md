# Tour-of-Heroes-Angular-DotNet7

The goal of this project was to create an example of an implementation of a full-stack web application using Angular and C# .Net 7.

## The Web Stack

This web app uses Angular 15 for the front-end and C# .Net 7 for the back-end.

Specifically, it uses the following technologies and frameworks:

### Front-End
- Angular 15 Framework
  - HTML
  - CSS
  - TypeScript

### Back-End
- C# .Net 7
- Entity Framework
  - In-Memory Database (Default)
  - Microsoft SQL Server (Optional)
  - Docker (Optional)

## Technical Features

- A front-end Angular web app used to access the web server's API endpoints which perform CRUD (Create, Read, Update, and Delete) operations on the web server's resources.
- A back-end C# .NET 7 RESTful Web API to allow the performing of CRUD operations on web server resources.
- The ability to use an In-Memory database out-of-the-box or optionally use a Microsoft SQL Server running in a Docker container.

## The Web App

The web app is derived from the [Angular Tour of Heroes Tutorial](https://angular.io/tutorial/tour-of-heroes) which consists of a simple CRUD web application for creating, reading, updating, and deleting heroes. The Heroes are simple pieces of data consisting of an `Id` and `Name`.

I have extended the web app in that tutorial to use be a full-stack web app by adding a .NET 7 web API back-end with a database.

## Run the Web App

This section will explain how to run the web application.

### Prerequisites

The following are required to run this web application:

- NodeJS runtime environment and NPM which you can get on the [NodeJS website](https://nodejs.org/en/download/).
- The Angular CLI. See the [Angular documentation](https://angular.io/cli) for instructions.
- Visual Studio with ASP.NET and Web Development features installed. Or any other similar setup for .Net web development.

### Steps

Perform the following steps to run this web application.

1. Fork/download the files in this GitHub project.

2. Open the HeroesApi Visual Studio Solution.

    - The web api is configured to use an in memory database by default so there is no need to setup a separate database server unless you want to try it with Microsoft SQL Server.

      ### Use Microsoft SQL Server (Optional)

      Additionally, the .NET 7 back-end is configured to use a Microsoft SQL Server running in a Docker container. This is optional and only required if you want to see this web app work with a Microsoft SQL Server. Otherwise, you are free to skip to step 3.

      Note: For Windows, this will require [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and setup on your PC if you want to go this route.

      2.1. Run the following Docker command to spin up a new container running Microsoft SQL Server.

      ```
      docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=YourSTRONG!Passw0rd" -e "MSSQL_PID=Express" -p 1433:1433 -d --name heroes-sqlserver mcr.microsoft.com/mssql/server
      ```

      Note: If you use a different password, you will need to update the `DefaultConnection` string in `appsettings.json` to whatever you changed it to.

      2.2. In `Program.cs`, comment out the line which sets up the In-Memory database `builder.Services.AddDbContext<HeroContext>(options => options.UseInMemoryDatabase("Heroes"));` and uncomment the other one which uses the SqlServer and the `DefaultConnection` string. To go back to the In-Memory database, simply do the reverse.

3. In Visual Studio, start the HeroesApi. Use the `https` option, Visual Studio may ask you to trust the localhost certificate, do so.

4. Change into the `angular-tour-of-heroes` directory and perform an NPM install to install the dependencies for the front-end.

```
npm install
```

5. Use the Angular CLI to run the front-end.

```
ng serve --open
```

6. Navigate and use the web app.
    - You can add some hero names on the `/heroes` page.
    - You can create, read, update, and delete heroes as desired.
    - If you restart the .Net 7 back-end, the heroes will be removed if using the In-Memory DB.

## References
1. [Angular Tour of Heroes Tutorial](https://angular.io/tutorial/tour-of-heroes)
2. [Tutorial: Create a Web API with ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-web-api?view=aspnetcore-7.0&tabs=visual-studio)
