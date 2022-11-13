FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CorporateApp.Finance/CorporateApp.Finance.csproj", "CorporateApp.Finance/"]
RUN dotnet restore "CorporateApp.Finance/CorporateApp.Finance.csproj"
COPY . .
WORKDIR "/src/CorporateApp.Finance"
RUN dotnet build "CorporateApp.Finance.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CorporateApp.Finance.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CorporateApp.Finance.dll"]
