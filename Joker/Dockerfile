FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build-env
WORKDIR /Joker

# Copy everything
COPY . ./
# Restore as distinct layers
RUN dotnet restore
# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:3.1
WORKDIR /Joker
COPY --from=build-env /Joker/out .

ENV ASPNETCORE_URLS http://+:80

EXPOSE 80/tcp

ENTRYPOINT ["dotnet", "Joker.dll"]
