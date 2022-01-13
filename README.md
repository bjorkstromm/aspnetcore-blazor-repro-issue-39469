# Repro code for https://github.com/dotnet/aspnetcore/issues/39469

This repository conitains repro code for https://github.com/dotnet/aspnetcore/issues/39469. Although Azure Front Door is not used here, we've configured YARP to work in similar manner when forwarding by adding a transformation rule on the route.

## Repro

Open up a terminal and start web.
```
cd Web
dotnet run
```
Web should start and listen on port 8888. Navigate to https://localhost:8888/web/ to verify.

In another terminal, start Proxy.
```
cd Proxy
dotnet run
```
Web should start and listen on port 8888. Navigate to https://localhost:8889/web/ to verify.

Now test the following URLs (note the casing)

- https://localhost:8888/WEB/
  This works as it works directly against Blazor web app

- https://localhost:8889/WEB/
  This doesn't works as it goes through the YARP proxy. You should see `An unhandled exception has occurred. See browser dev tools for details.` in the bottom, and console log in browser should contain `Error: The circuit failed to initialize.`.