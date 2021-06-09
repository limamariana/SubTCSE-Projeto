#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Av.SubTCSE.Projeto.API/Av.SubTCSE.Projeto.API.csproj", "Av.SubTCSE.Projeto.API/"]
RUN dotnet restore "Av.SubTCSE.Projeto.API/Av.SubTCSE.Projeto.API.csproj"
COPY . .
WORKDIR "/src/Av.SubTCSE.Projeto.API"
RUN dotnet build "Av.SubTCSE.Projeto.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Av.SubTCSE.Projeto.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Av.SubTCSE.Projeto.API.dll"]