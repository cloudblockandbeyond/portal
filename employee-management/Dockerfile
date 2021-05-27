# Build image
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src

# Copy csproj and restore as distinct layer
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build app
COPY . ./
RUN dotnet publish --configuration release --output /app --no-restore

# Runtime image
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS runtime
WORKDIR /app

EXPOSE 80/tcp
EXPOSE 443/tcp

COPY --from=build /app ./
ENTRYPOINT ["dotnet"]
CMD ["employee-management.dll"]

ENV ASPNETCORE_ENVIRONMENT="Production"