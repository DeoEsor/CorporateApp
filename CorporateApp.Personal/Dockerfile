FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CorporateApp.Personal/CorporateApp.Personal.csproj", "CorporateApp.Personal/"]
RUN dotnet restore "CorporateApp.Personal/CorporateApp.Personal.csproj"
COPY . .
WORKDIR "/src/CorporateApp.Personal"
RUN dotnet build "CorporateApp.Personal.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CorporateApp.Personal.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CorporateApp.Personal.dll"]
