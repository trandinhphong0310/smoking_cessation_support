# Giai đoạn build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy file .csproj
COPY WebSmokingSupport.csproj ./

# Chạy restore
RUN dotnet restore WebSmokingSupport.csproj

# Copy toàn bộ mã nguồn
COPY . ./

# Build & publish
RUN dotnet publish -c Release -o /app/publish

# Giai đoạn runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

# Mở cổng 80
EXPOSE 80

# Chạy ứng dụng
ENTRYPOINT ["dotnet", "WebSmokingSupport.dll", "--urls", "http://+:80"]
