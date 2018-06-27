FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ./LinuxDockerTest.csproj ./LinuxDockerTest
RUN dotnet restore ./LinuxDockerTest.csproj
COPY . .
WORKDIR /src/LinuxDockerTest
RUN dotnet build LinuxDockerTest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish LinuxDockerTest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "LinuxDockerTest.dll"]
