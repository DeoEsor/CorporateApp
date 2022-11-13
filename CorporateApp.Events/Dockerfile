FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CorporateApp.Events/CorporateApp.Events.csproj", "CorporateApp.Events/"]
RUN dotnet restore "CorporateApp.Events/CorporateApp.Events.csproj"
COPY . .
WORKDIR "/src/CorporateApp.Events"
RUN dotnet build "CorporateApp.Events.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CorporateApp.Events.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CorporateApp.Events.dll"]
