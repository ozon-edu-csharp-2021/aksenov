FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build

WORKDIR /src
COPY ["src/merchandiseService/merchandiseService.csproj", "src/merchandiseService/"]
RUN dotnet restore "src/merchandiseService/merchandiseService.csproj"

COPY . .

WORKDIR "/src/src/merchandiseService"

RUN dotnet build "merchandiseService.csproj" -c Release -o /app/build

FROM build as publish
RUN dotnet publish "merchandiseService.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS runtime

WORKDIR /app

EXPOSE 80
EXPOSE 443

FROM runtime AS final
WORKDIR /app

COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet", "merchandiseService.dll"]