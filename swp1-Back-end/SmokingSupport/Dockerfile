# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy .csproj
COPY WebSmokingSupport/WebSmokingSupport.csproj WebSmokingSupport/

# Restore dependencies
WORKDIR /src/WebSmokingSupport
RUN dotnet restore

# Copy toàn bộ mã nguồn
COPY WebSmokingSupport/ ./WebSmokingSupport/

# Publish
RUN dotnet publish -c Release -o /app/publish

# Stage 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

EXPOSE 80
ENTRYPOINT ["dotnet", "WebSmokingSupport.dll", "--urls", "http://+:80"]
