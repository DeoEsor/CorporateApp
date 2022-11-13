FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CorporateApp.Resources/CorporateApp.Resources.csproj", "CorporateApp.Resources/"]
RUN dotnet restore "CorporateApp.Resources/CorporateApp.Resources.csproj"
COPY . .
WORKDIR "/src/CorporateApp.Resources"
RUN dotnet build "CorporateApp.Resources.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CorporateApp.Resources.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CorporateApp.Resources.dll"]
