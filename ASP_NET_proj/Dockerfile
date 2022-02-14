FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ASP_NET_proj/ASP_NET_proj.csproj", "ASP_NET_proj/"]
RUN dotnet restore "ASP_NET_proj/ASP_NET_proj.csproj"
COPY . .
WORKDIR "/src/ASP_NET_proj"
RUN dotnet build "ASP_NET_proj.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASP_NET_proj.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASP_NET_proj.dll"]
