# syntax=docker/dockerfile:1
#phase1: Restore and build of an application
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
# Restore on the csproject
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
#copying the rest and running publish 
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/sdk:3.1
WORKDIR /app
COPY --from=build-env /app/out .
#Exposing the port
ENV ASPNETCORE_URLS http://*:80
EXPOSE 80
ENTRYPOINT ["dotnet", "WebAppgit1.dll"]
