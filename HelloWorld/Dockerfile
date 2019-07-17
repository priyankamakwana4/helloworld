#FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
#WORKDIR /src
#COPY ["HelloWorld/HelloWorld.csproj", "HelloWorld/"]
#RUN dotnet restore "HelloWorld/HelloWorld.csproj"
#COPY . .
#WORKDIR "/src/HelloWorld"
#RUN dotnet build "HelloWorld.csproj" -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish Catalog.API.csproj -c Release -o /app
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#
#


#FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-nanoserver-1803 AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443
#
#FROM mcr.microsoft.com/dotnet/core/sdk:2.2-nanoserver-1803 AS build
#WORKDIR /src
#COPY ["HelloWorld/HelloWorld.csproj", "HelloWorld/"]
#RUN dotnet restore "HelloWorld/HelloWorld.csproj"
#COPY . .
#WORKDIR "/src/HelloWorld"
#RUN dotnet build "HelloWorld.csproj" -c Release -o /app

#FROM build AS publish
#RUN dotnet publish "HelloWorld.csproj" -c Release -o /app

#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "HelloWorld.dll"]

#FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
#WORKDIR /src
## copy csproj and restore as distinct layers
#COPY *.csproj ./
#RUN dotnet restore "HelloWorld/HelloWorld.csproj"
## copy everything else and build
#COPY . .
#WORKDIR "/src/HelloWorld"
#RUN dotnet build "HelloWorld.csproj" -c Release -o /app
#
## build runtime image
#FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
#WORKDIR /app
#COPY --from=build-env /app .
#EXPOSE 80/tcp
#ENTRYPOINT ["dotnet", "HelloWorld.dll"]

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["HelloWorldWindows/HelloWorldWindows.csproj", "HelloWorldWindows/"]
RUN dotnet restore "HelloWorldWindows/HelloWorldWindows.csproj"
COPY . .
WORKDIR "/src/HelloWorldWindows"
RUN dotnet build "HelloWorldWindows.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloWorldWindows.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloWorldWindows.dll"]