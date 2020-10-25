FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY src/AspNetCoreExample/AspNetCoreExample.csproj src/AspNetCoreExample/
RUN dotnet restore src/AspNetCoreExample/AspNetCoreExample.csproj
COPY . .
WORKDIR /src/src/AspNetCoreExample
RUN dotnet build AspNetCoreExample.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish AspNetCoreExample.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspNetCoreExample.dll"]
