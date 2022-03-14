#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["IdentityApi.csproj", "IdentityApi/"]
RUN dotnet restore "IdentityApi/IdentityApi.csproj"
COPY . .
WORKDIR "/src/IdentityApi"
COPY . .
RUN dotnet build "IdentityApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "IdentityApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "IdentityApi.dll"]
CMD ASPNETCORE_URLS=http://*:$PORT dotnet IdentityApi.dll

#CMD export ASPNETCORE_URLS=http://*:$PORT
#CMD ASPNETCORE_URLS=http://*:$PORT dotnet FuraFila.WebApp.dll