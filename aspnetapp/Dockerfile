FROM microsoft/aspnetcore-build:1.1 AS build-env
WORKDIR /app
# copy everything within the project folder
COPY . ./
# restore as distinct layers
RUN dotnet restore
# build and publish bits
RUN dotnet publish -c Release -o out


# build runtime image
FROM microsoft/aspnetcore:1.1
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "aspnetapp.dll"]
