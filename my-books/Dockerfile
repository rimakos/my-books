FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["my-books/my-books.csproj", "my-books/"]
RUN dotnet restore "my-books/my-books.csproj"
COPY . .
WORKDIR "/src/my-books"
RUN dotnet build "my-books.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "my-books.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "my-books.dll"]
