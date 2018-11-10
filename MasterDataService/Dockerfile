FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["MasterDataService/MasterDataService.csproj", "MasterDataService/"]

RUN dotnet restore "$PROJECT_DIR/MasterDataService.csproj"
COPY . .
WORKDIR "/src/MasterDataService"
RUN dotnet build "MasterDataService.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MasterDataService.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MasterDataService.dll"]