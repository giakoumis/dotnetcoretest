FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MicroServicesTesting/MicroServicesTesting.csproj", "MicroServicesTesting/"]
RUN dotnet restore "MicroServicesTesting/MicroServicesTesting.csproj"
COPY . .
WORKDIR "/src/MicroServicesTesting"
RUN dotnet build "MicroServicesTesting.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MicroServicesTesting.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MicroServicesTesting.dll"]