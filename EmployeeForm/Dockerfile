# File: Dockerfile.frontend
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /app

# Copy csproj and restore dependencies
COPY EmployeeForm/*.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY EmployeeForm/ ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /app/out .
ENTRYPOINT ["dotnet", "EmployeeForm.dll"]
