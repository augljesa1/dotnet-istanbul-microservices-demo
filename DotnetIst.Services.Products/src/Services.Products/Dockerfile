FROM mcr.microsoft.com/dotnet/sdk:2.2.0 AS build-env
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2.0 AS build
WORKDIR /src
COPY ["DotnetIst.Services.Products/src/Services.Products/Services.Products.csproj", "DotnetIst.Services.Products/src/Services.Products"]
RUN dotnet restore "DotnetIst.Services.Products/src/Services.Products/Services.Products.csproj"
COPY . .
WORKDIR "/src/DotnetIst.Services.Products/src/Services.Products"
RUN dotnet build "Services.Products.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Services.Products.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Services.Products.dll"]
