FROM mcr.microsoft.com/dotnet/aspnet:5.0 as base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /source
COPY *.sln .
COPY Review.Web/*.csproj ./Review.Web/
RUN dotnet restore
COPY Review.Web/. ./Review.Web/
WORKDIR /source/Review.Web
RUN dotnet publish -c Release -o /app --no-restore

FROM base as final
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "Review.Web.dll"]