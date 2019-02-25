FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Cardcraft.API/Cardcraft.API.csproj", "Cardcraft.API/"]
RUN dotnet restore "Cardcraft.API/Cardcraft.API.csproj"
COPY . .
WORKDIR "/src/Cardcraft.API"
RUN dotnet build "Cardcraft.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Cardcraft.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Cardcraft.API.dll"]