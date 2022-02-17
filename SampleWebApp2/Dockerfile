#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
#EXPOSE 80
#EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
#COPY ["SampleWebApp2/SampleWebApp2.csproj", "SampleWebApp2/"]
COPY ["SampleWebApp2.csproj", "SampleWebApp2/"]
RUN dotnet restore "SampleWebApp2/SampleWebApp2.csproj"
# RUN dotnet restore "SampleWebApp2.csproj"
COPY . ./SampleWebApp2
# WORKDIR "/src/SampleWebApp2"
 RUN dotnet build "./SampleWebApp2/SampleWebApp2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "./SampleWebApp2/SampleWebApp2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SampleWebApp2.dll"]