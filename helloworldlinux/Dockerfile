FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["helloworldlinux/helloworldlinux.csproj", "helloworldlinux/"]
RUN dotnet restore "helloworldlinux/helloworldlinux.csproj"
COPY . .
WORKDIR "/src/helloworldlinux"
RUN dotnet build "helloworldlinux.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "helloworldlinux.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "helloworldlinux.dll"]