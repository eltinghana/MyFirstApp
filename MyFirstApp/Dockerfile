FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["MyFirstApp/MyFirstApp.csproj", "MyFirstApp/"]
RUN dotnet restore "MyFirstApp/MyFirstApp.csproj"
COPY . .
WORKDIR "/src/MyFirstApp"
RUN dotnet build "MyFirstApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyFirstApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyFirstApp.dll"]
