# Dockerfile
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["DevOpsWebApplication/DevOpsWebApplication.csproj", "DevOpsWebApplication/"]
RUN dotnet restore "DevOpsWebApplication/DevOpsWebApplication.csproj"
COPY . .
WORKDIR "/src/DevOpsWebApplication"
RUN dotnet build "DevOpsWebApplication.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DevOpsWebApplication.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevOpsWebApplication.dll"]