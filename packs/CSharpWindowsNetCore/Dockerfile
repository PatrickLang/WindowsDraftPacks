FROM microsoft/dotnet:2.2-sdk-nanoserver-1809 AS builder
WORKDIR /app

# caches restore result by copying csproj file separately
COPY *.csproj .
RUN dotnet restore

COPY . .
RUN dotnet publish --output /app/ --configuration Release
# TODO: if the assembly name is given in .csproj, use it
# RUN sed -n 's:.*<AssemblyName>\(.*\)</AssemblyName>.*:\1:p' *.csproj > __assemblyname
RUN if not exist "__assemblyname" ( for %i in (*.csproj) do ( echo %~ni.dll ) > __assemblyname )

# Stage 2
FROM microsoft/dotnet:2.2-aspnetcore-runtime-nanoserver-1809
WORKDIR /app
COPY --from=builder /app .

ENV PORT 80
EXPOSE 80

ENTRYPOINT for /f %i in ( __assemblyname ) do dotnet %i
