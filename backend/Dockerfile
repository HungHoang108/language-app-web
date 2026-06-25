# FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
# WORKDIR /src

# # copy csproj and restore as distinct layers
# COPY ["backend.csproj", "./"]
# RUN dotnet restore "./backend.csproj"

# # copy everything else and publish
# COPY . .
# RUN dotnet publish "backend.csproj" -c Release -o /app/publish /p:UseAppHost=false

# FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS runtime
# WORKDIR /app
# COPY --from=build /app/publish .

# ENV ASPNETCORE_URLS=http://+:80
# EXPOSE 80

# ENTRYPOINT ["dotnet", "backend.dll"]

FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

COPY . /src

RUN dotnet restore

RUN dotnet publish -o out

FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS runtime
WORKDIR /app
COPY --from=build /src/out .

ENTRYPOINT ["dotnet", "backend.dll"]