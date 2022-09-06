#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["team-api/team-api.csproj", "team-api/"]
RUN dotnet restore "team-api/team-api.csproj"
COPY . .
WORKDIR "/src/team-api"
RUN dotnet build "team-api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "team-api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "team-api.dll"]