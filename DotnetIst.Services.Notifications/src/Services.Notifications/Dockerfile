FROM mcr.microsoft.com/dotnet/sdk:2.2.0 AS build-env
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2.0 AS build
WORKDIR /src
COPY ["DotnetIst.Services.Notifications/src/Services.Notifications/Services.Notifications.csproj", "DotnetIst.Services.Notifications/src/Services.Notifications"]
RUN dotnet restore "DotnetIst.Services.Notifications/src/Services.Notifications/Services.Notifications.csproj"
COPY . .
WORKDIR "/src/DotnetIst.Services.Notifications/src/Services.Notifications"
RUN dotnet build "Services.Notifications.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Services.Notifications.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Services.Notifications.dll"]
