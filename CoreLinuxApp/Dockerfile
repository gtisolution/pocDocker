FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 32928
EXPOSE 44304

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY CoreLinuxApp/CoreLinuxApp.csproj CoreLinuxApp/
RUN dotnet restore CoreLinuxApp/CoreLinuxApp.csproj
COPY . .
WORKDIR /src/CoreLinuxApp
RUN dotnet build CoreLinuxApp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish CoreLinuxApp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreLinuxApp.dll"]
