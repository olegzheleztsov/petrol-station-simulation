FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["PetrolStation.Worker/PetrolStation.Worker.csproj", "PetrolStation.Worker/"]
RUN dotnet restore "PetrolStation.Worker/PetrolStation.Worker.csproj"
COPY . .
WORKDIR "/src/PetrolStation.Worker"
RUN dotnet build "PetrolStation.Worker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PetrolStation.Worker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PetrolStation.Worker.dll"]
