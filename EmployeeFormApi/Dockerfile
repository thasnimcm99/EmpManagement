# Use the official .NET runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

# Use the official .NET SDK image for building the application
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

# Copy the project files
COPY ["EmployeeFormApi/EmployeeFormApi.csproj", "EmployeeFormApi/"]
RUN dotnet restore "EmployeeFormApi/EmployeeFormApi.csproj"

# Copy the entire application
COPY . .
WORKDIR "/src/EmployeeFormApi"

# Build the application
RUN dotnet publish -c Release -o /app/publish

# Final image
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "EmployeeFormApi.dll"]
