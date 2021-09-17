#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["DotNetCore5WebAppPrjDevOpsKubernets/DotNetCore5WebAppPrjDevOpsKubernets.csproj", "DotNetCore5WebAppPrjDevOpsKubernets/"]
RUN dotnet restore "DotNetCore5WebAppPrjDevOpsKubernets/DotNetCore5WebAppPrjDevOpsKubernets.csproj"
COPY . .
WORKDIR "/src/DotNetCore5WebAppPrjDevOpsKubernets"
RUN dotnet build "DotNetCore5WebAppPrjDevOpsKubernets.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotNetCore5WebAppPrjDevOpsKubernets.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNetCore5WebAppPrjDevOpsKubernets.dll"]