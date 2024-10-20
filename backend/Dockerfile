# Use the official .NET Core SDK image as the build environment
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Copy the app and build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["backend.csproj", "./"]
RUN dotnet restore "backend.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "backend.csproj" -c Release -o /app/build

# Publish the build
FROM build AS publish
RUN dotnet publish "backend.csproj" -c Release -o /app/publish

# Use the runtime image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "backend.dll"]
