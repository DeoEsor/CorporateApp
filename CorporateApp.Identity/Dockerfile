FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CorporateApp.Identity/CorporateApp.Identity.csproj", "CorporateApp.Identity/"]
RUN dotnet restore "CorporateApp.Identity/CorporateApp.Identity.csproj"
COPY . .
WORKDIR "/src/CorporateApp.Identity"
RUN dotnet build "CorporateApp.Identity.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CorporateApp.Identity.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CorporateApp.Identity.dll"]
