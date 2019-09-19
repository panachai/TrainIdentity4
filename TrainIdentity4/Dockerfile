FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["TrainIdentity4/TrainIdentity4.csproj", "TrainIdentity4/"]
RUN dotnet restore "TrainIdentity4/TrainIdentity4.csproj"
COPY . .
WORKDIR "/src/TrainIdentity4"
RUN dotnet build "TrainIdentity4.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TrainIdentity4.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TrainIdentity4.dll"]