FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 5146

ENV ASPNETCORE_URLS=http://+:5146

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["MagicVilla_VillaAPI.csproj", "./"]
RUN dotnet restore "MagicVilla_VillaAPI.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "MagicVilla_VillaAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MagicVilla_VillaAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MagicVilla_VillaAPI.dll"]
