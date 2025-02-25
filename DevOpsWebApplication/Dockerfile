# Dockerfile

# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy project files and restore dependencies
COPY DevOpsWebApplication/ DevOpsWebApplication/
WORKDIR /src/DevOpsWebApplication
RUN dotnet restore

# Copy everything else and build application
COPY . .
RUN dotnet build -c Release --no-restore -o /app/build

# Publish stage
FROM build AS publish
RUN dotnet publish -c Release --no-restore -o /app/publish

# Final runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevOpsWebApplication.dll"]