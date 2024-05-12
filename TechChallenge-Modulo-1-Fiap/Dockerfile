#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["TechChallenge-Modulo-1-Fiap/TechChallenge-Modulo-1-Fiap.csproj", "TechChallenge-Modulo-1-Fiap/"]
RUN dotnet restore "./TechChallenge-Modulo-1-Fiap/./TechChallenge-Modulo-1-Fiap.csproj"
COPY . .
WORKDIR "/src/TechChallenge-Modulo-1-Fiap"
RUN dotnet build "./TechChallenge-Modulo-1-Fiap.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./TechChallenge-Modulo-1-Fiap.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TechChallenge-Modulo-1-Fiap.dll"]