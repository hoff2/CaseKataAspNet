FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY CaseKataVersionTwo.sln ./
COPY CaseKata/CaseKata.csproj CaseKata/
RUN dotnet restore /p:RestoreUseSkipNonexistentTargets="false" -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/CaseKata
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CaseKata.dll"]
