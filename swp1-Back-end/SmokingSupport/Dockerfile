FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy .csproj
COPY swp1-Back-end/SmokingSupport/WebSmokingSupport/WebSmokingSupport.csproj ./WebSmokingSupport/

# Restore
WORKDIR /src/WebSmokingSupport
RUN dotnet restore

# Copy toàn bộ mã nguồn
COPY swp1-Back-end/SmokingSupport/WebSmokingSupport/ ./WebSmokingSupport/

# Build
RUN dotnet publish -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

EXPOSE 80
ENTRYPOINT ["dotnet", "WebSmokingSupport.dll", "--urls", "http://+:80"]
