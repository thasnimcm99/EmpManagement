# Use the official .NET runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

# Use the official .NET SDK image for building the application
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

# Copy the .csproj file and restore dependencies
COPY ["EmployeeForm/EmployeeForm.csproj", "EmployeeForm/"]
RUN dotnet restore "EmployeeForm/EmployeeForm.csproj"

# Copy the rest of the application code
COPY EmployeeForm/ EmployeeForm/
WORKDIR "/src/EmployeeForm"

# Build the application
RUN dotnet publish -c Release -o /app/publish

# Final image
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "EmployeeForm.dll"]
