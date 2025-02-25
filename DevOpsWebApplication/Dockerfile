# Use the official .NET SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build

# Set the working directory in the container
WORKDIR /app

# Copy the project file and restore dependencies
COPY *.csproj ./
RUN dotnet restore "DevOpsWebApplication.csproj"

# Copy the rest of the source code
COPY . ./

# Build the application with detailed verbosity
RUN dotnet build "DevOpsWebApplication.csproj" -c Release -v detailed -o /app/build

# Publish the application to the /app/publish directory
RUN dotnet publish "DevOpsWebApplication.csproj" -c Release -o /app/publish

# Use the official .NET runtime image to run the application
FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS runtime

# Set the working directory in the container
WORKDIR /app

# Copy the published application from the build stage
COPY --from=build /app/publish .

# Set the entry point to run the application
ENTRYPOINT ["dotnet", "DevOpsWebApplication.dll"]