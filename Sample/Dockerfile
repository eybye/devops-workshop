FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /build

# copy csproj and restore as distinct layers
COPY src/*.csproj .
RUN dotnet restore

# copy files from host (src) to image (/build)
COPY src/. .

# build in Release and do a deployment to /publish
run dotnet publish -c Release -o /publish

FROM microsoft/dotnet:2.1-aspnetcore-runtime AS runtime

WORKDIR /app
# copy files from image 'build:/publish' to this image's working dir
COPY --from=build /publish .

ENTRYPOINT ["dotnet", "aspnetapp.dll"]