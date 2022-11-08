FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["deployment-status/deployment-status.csproj", "deployment-status/"]
RUN dotnet restore "deployment-status/deployment-status.csproj"
COPY . .
WORKDIR "/src/deployment-status"
RUN dotnet build "deployment-status.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "deployment-status.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "deployment-status.dll"]
