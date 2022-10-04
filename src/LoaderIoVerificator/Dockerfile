FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/LoaderIoVerificator/LoaderIoVerificator.csproj", "src/LoaderIoVerificator/"]
RUN dotnet restore "src/LoaderIoVerificator/LoaderIoVerificator.csproj"
COPY . .
WORKDIR "/src/src/LoaderIoVerificator"
RUN dotnet build "LoaderIoVerificator.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LoaderIoVerificator.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LoaderIoVerificator.dll"]