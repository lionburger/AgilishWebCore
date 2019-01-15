FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 6337
EXPOSE 44327

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AgilishWebCore/AgilishWebCore.csproj", "AgilishWebCore/"]
RUN dotnet restore "AgilishWebCore/AgilishWebCore.csproj"
COPY . .
WORKDIR "/src/AgilishWebCore"
RUN dotnet build "AgilishWebCore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AgilishWebCore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AgilishWebCore.dll"]