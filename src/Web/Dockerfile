# Build Stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy the solution file and all project files
COPY *.sln . 
COPY src/Web/*.csproj ./src/Web/

# Copy the entire source code to the container
COPY . .

# Set the working directory to the Web project folder
WORKDIR /app/src/Web

# Restore dependencies
RUN dotnet restore

# Publish the application in Release mode
RUN dotnet publish -c Release -o /app/out

# Runtime Stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Copy the output from the build stage
COPY --from=build /app/out ./

# Set entrypoint for the container to run the Web.dll
ENTRYPOINT ["dotnet", "Web.dll"]
