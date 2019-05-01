FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MySite.Web/MySite.Web.csproj", "MySite.Web/"]
RUN dotnet restore "MySite.Web/MySite.Web.csproj"
COPY . .
WORKDIR "/src/MySite.Web"
RUN dotnet build "MySite.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MySite.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MySite.Web.dll"]