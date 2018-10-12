FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["MyVSAKS7/MyVSAKS7.csproj", "MyVSAKS7/"]

RUN dotnet restore "$PROJECT_DIR/MyVSAKS7.csproj"
COPY . .
WORKDIR "/src/MyVSAKS7"
RUN dotnet build "MyVSAKS7.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MyVSAKS7.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MyVSAKS7.dll"]