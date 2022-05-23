# Steg 1. Hämta basavbilden (image) för asp.net 6.0
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env

# Steg 2. Ange arbetskatalog
WORKDIR /app

# Steg 3. Kopiera all källkod till docker
# COPY <src> <dest>
COPY . ./
RUN dotnet restore

# Steg 4. Skapa ett publiceringspaket
# publish skapar ett optimerat publiceringspaket och -c anger vilken konfiguration vi ska använda
# Release anger att det är ett byggpaket som är optimerat -o anger var vi vill placera detta paket
RUN dotnet publish -c Release -o out

# Steg 5. Skapa en bggprocess av applikationen
# vi kommer att skapa en aspnet applikation
FROM mcr.microsoft.com/dotnet/aspnet:6.0 
WORKDIR /app
# COPY använder sig av build-env inställningarna
# och kopierar filer och paket från /app/out
COPY --from=build-env /app/out .

# Steg 6. Ange hur applikationen ska startas
ENTRYPOINT [ "dotnet", "westcoastcars-app.dll" ]