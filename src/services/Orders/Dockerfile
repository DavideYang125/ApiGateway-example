FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/services/Orders/Orders.csproj", "src/services/Orders/"]
RUN dotnet restore "src/services/Orders/Orders.csproj"
COPY . .
WORKDIR "/src/src/services/Orders"
RUN dotnet build "Orders.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Orders.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Orders.dll"]
