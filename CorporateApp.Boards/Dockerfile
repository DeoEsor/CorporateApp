FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CorporateApp.Boards/CorporateApp.Boards.csproj", "CorporateApp.Boards/"]
RUN dotnet restore "CorporateApp.Boards/CorporateApp.Boards.csproj"
COPY . .
WORKDIR "/src/CorporateApp.Boards"
RUN dotnet build "CorporateApp.Boards.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CorporateApp.Boards.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CorporateApp.Boards.dll"]
