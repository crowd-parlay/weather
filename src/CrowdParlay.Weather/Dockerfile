FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["CrowdParlay.Weather/CrowdParlay.Weather.csproj", "CrowdParlay.Weather/"]
RUN dotnet restore "CrowdParlay.Weather/CrowdParlay.Weather.csproj"
COPY . .
WORKDIR "/src/CrowdParlay.Weather"
RUN dotnet build "CrowdParlay.Weather.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CrowdParlay.Weather.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CrowdParlay.Weather.dll"]
