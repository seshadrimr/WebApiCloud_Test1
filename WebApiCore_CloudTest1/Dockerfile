FROM microsoft/dotnet:2.2-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app


FROM microsoft/dotnet:2.2-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY . paservice/
RUN ls -la paservice
RUN dotnet restore paservice/WebApiCore_CloudTest1/WebApiCore_CloudTest1.csproj

COPY . . 

WORKDIR /src/paservice
RUN dotnet build WebApiCore_CloudTest1/WebApiCore_CloudTest1.csproj -c Release -o /app 

FROM build AS publish
RUN dotnet publish WebApiCore_CloudTest1/WebApiCore_CloudTest1.csproj -c Release -o /app 

FROM base AS final
WORKDIR /app
COPY --from=publish /app .

### Run Environment Variable
ENV ASPNETCORE_ENVIRONMENT="production"
### Kestrel Port Environment Variable
ENV ASPNETCORE_URLS="http://*:80"
##RUN dotnet WebApiCore_CloudTest1.dll
EXPOSE 80/tcp
ENTRYPOINT ["dotnet", "WebApiCore_CloudTest1.dll"]