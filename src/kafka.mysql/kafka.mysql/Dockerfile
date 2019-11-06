FROM mcr.microsoft.com/dotnet/core/runtime:3.0-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY kafka.mysql/kafka.mysql.csproj kafka.mysql/
RUN dotnet restore "kafka.mysql/kafka.mysql.csproj"
COPY . .
WORKDIR "/src/kafka.mysql"
RUN dotnet build "kafka.mysql.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "kafka.mysql.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "kafka.mysql.dll"]
