#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["DotNetCoreAPI/DotNetCoreAPI.csproj", "DotNetCoreAPI/"]
RUN dotnet restore "DotNetCoreAPI/DotNetCoreAPI.csproj"
COPY . .
WORKDIR "/src/DotNetCoreAPI"
RUN dotnet build "DotNetCoreAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotNetCoreAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNetCoreAPI.dll"]