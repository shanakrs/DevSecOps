FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
#EXPOSE 5000

#ENV ASPNETCORE_URLS=http://+:5000

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src

RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs

COPY ["dotnetcoreangular.csproj", "./"]
RUN dotnet restore "dotnetcoreangular.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "dotnetcoreangular.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnetcoreangular.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnetcoreangular.dll"]