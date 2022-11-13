FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CorporateApp.Task/CorporateApp.Task.csproj", "CorporateApp.Task/"]
RUN dotnet restore "CorporateApp.Task/CorporateApp.Task.csproj"
COPY . .
WORKDIR "/src/CorporateApp.Task"
RUN dotnet build "CorporateApp.Task.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CorporateApp.Task.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CorporateApp.Task.dll"]
