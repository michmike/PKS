# Use the ASP.NET layered image. It has built-in the following:
# Windows Server Core as the base OS
# IIS 10 as Web Server
# .NET Framework (multiple versions available)
# .NET Extensibility for IIS
FROM mcr.microsoft.com/dotnet/framework/aspnet:3.5

# Open up the port for http traffic into IIS and our app
EXPOSE 80

# Copy the application binaries into the image
# Overwrite the default website on that IIS instance
COPY ./OldWebApp/Publish/ /inetpub/wwwroot/
