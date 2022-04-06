FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Backend.WebAPI/Backend.WebAPI.csproj", "Backend.WebAPI/"]
RUN dotnet restore "Backend.WebAPI/Backend.WebAPI.csproj"
COPY . .
WORKDIR "/src/Backend.WebAPI"
RUN dotnet build "Backend.WebAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Backend.WebAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Backend.WebAPI.dll"]
