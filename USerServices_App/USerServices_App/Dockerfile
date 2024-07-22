#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 2233

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["USerServices_App/USerServices_App/USerServices_App.csproj", "USerServices_App/USerServices_App/"]
COPY ["ECommerceDataModel/ECommerceDataModel.csproj", "ECommerceDataModel/"]
RUN dotnet restore "USerServices_App/USerServices_App/USerServices_App.csproj"
COPY . .
WORKDIR "/src/USerServices_App/USerServices_App"
RUN dotnet build "USerServices_App.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "USerServices_App.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "USerServices_App.dll"]