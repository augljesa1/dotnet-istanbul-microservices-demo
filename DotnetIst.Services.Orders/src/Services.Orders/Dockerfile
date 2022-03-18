FROM mcr.microsoft.com/dotnet/sdk:2.2.0 AS build-env
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2.0 AS build
WORKDIR /src
COPY ["DotnetIst.Services.Orders/src/Services.Orders/Services.Orders.csproj", "DotnetIst.Services.Orders/src/Services.Orders"]
RUN dotnet restore "DotnetIst.Services.Orders/src/Services.Orders/Services.Orders.csproj"
COPY . .
WORKDIR "/src/DotnetIst.Services.Orders/src/Services.Orders"
RUN dotnet build "Services.Orders.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Services.Orders.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Services.Orders.dll"]
