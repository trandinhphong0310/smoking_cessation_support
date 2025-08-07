# Use .NET 8 SDK to build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy the .csproj file
COPY WebSmokingSupport/WebSmokingSupport.csproj ./WebSmokingSupport/

# Restore dependencies
RUN dotnet restore ./WebSmokingSupport/WebSmokingSupport.csproj

# Copy entire source code
COPY . .

# Build and publish the app
RUN dotnet publish ./WebSmokingSupport/WebSmokingSupport.csproj -c Release -o /app/publish

# Use .NET 8 runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

EXPOSE 80
ENTRYPOINT ["dotnet", "WebSmokingSupport.dll"]
