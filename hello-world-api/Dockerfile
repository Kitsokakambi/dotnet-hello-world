# Use the official .NET SDK image for building the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy the project files and restore dependencies
COPY ./hello-world-api/*.csproj ./
RUN dotnet restore

# Copy the rest of the application files
COPY ./hello-world-api/ ./
RUN dotnet publish -c Release -o /app/publish

# Use a smaller runtime image for running the application
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Copy the build output from the previous step
COPY --from=build /app/publish .

# Expose the port the application runs on
EXPOSE 8080

# Start the application
ENTRYPOINT ["dotnet", "hello-world-api.dll"]
