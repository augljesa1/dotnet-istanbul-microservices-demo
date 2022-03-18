FROM mcr.microsoft.com/dotnet/sdk:2.2.0 AS build-env
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2.0 AS build
WORKDIR /src
COPY ["DotnetIst.Services.Customers/src/Services.Customers/Services.Customers.csproj", "DotnetIst.Services.Customers/src/Services.Customers"]
RUN dotnet restore "DotnetIst.Services.Customers/src/Services.Customers/Services.Customers.csproj"
COPY . .
WORKDIR "/src/DotnetIst.Services.Customers/src/Services.Customers"
RUN dotnet build "UsersService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Services.Customers.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Services.Customers.dll"]
