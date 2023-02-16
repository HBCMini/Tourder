FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["tourder/tourder.csproj", "tourder/"]
RUN dotnet restore "tourder/tourder.csproj"
COPY . .
WORKDIR "/src/tourder"
RUN dotnet build "tourder.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "tourder.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "tourder.dll"]
