#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY SampleWebAppOnDocker.csproj .
RUN dotnet restore
COPY . .
RUN dotnet publish -c Release -o /app

FROM build AS publish
RUN dotnet publish "SampleWebAppOnDocker.csproj" -c Release -o /app

FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=build /app .
ENTRYPOINT ["dotnet", "SampleWebAppOnDocker.dll"]