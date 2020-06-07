#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["RepoMail.UI/RepoMail.UI.csproj", "RepoMail.UI/"]
RUN dotnet restore "RepoMail.UI/RepoMail.UI.csproj"
COPY . .
WORKDIR "/src/RepoMail.UI"
RUN dotnet build "RepoMail.UI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RepoMail.UI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RepoMail.UI.dll"]