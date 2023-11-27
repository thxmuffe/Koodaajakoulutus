# Koodaajakoulutus
Koodaajakoulutus (ASP.NET + React) esimerkit 


Azure SQL server:
- kun valmis, sinun pitää tehdä poikkeus palomuuriin. salli oman koneesi IP-osoite ennen kun yrität yhdistää tietokantaan Azure Data Studiolla.
- Huom Azure Data Studiolla kytkeydytään tietokannan SQL-login tunnuksilla.


Voit tehdä "New query" napilla uuden taulun omaan tietokantaasi, esimerkkinä

CREATE TABLE Persons (
    Personid int IDENTITY(1,1) PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);



WebAPI:
Voit yksinkertaistaa launch-settings tiedostoa, jättää ainoastaan https-version, jolloin vähemmän epäselvyttää mikä profiili käytössä. Voit testata WeatherController contolleria esim: https://localhost:7183/WeatherForecast

kts. https://learn.microsoft.com/en-us/ef/core/cli/dotnet
Tee EF-model aiemman osan tietokannasta.
ConnectionString:n saa kopioitua Azuresta, ja voit sen jälkeen luoda mallin:
dotnet ef dbcontext scaffold komennolla.

Kun sinulla on EF-malli luoto, lisää uusi kontroller ohjelmaasi, joka tallettaa uuden henkilön persons kantaan. Tai hakee listan Persons taulussa olevista henkilöistä.

Kontrolleri kannattaa tehdä käsin, mutta voit myös aluksi tehdä sen automaattisesti komentoriviltä, jolloin näet millainen siitä pitäisi tulla. kts. https://learn.microsoft.com/en-us/aspnet/core/fundamentals/tools/dotnet-aspnet-codegenerator?view=aspnetcore-8.0

dotnet aspnet-codegenerator --project . controller -name YOUR_CONTROLLER_NAME -m YOUR_MODEL_NAME -dc YOUR_DB_CONTEXT_CLASS -outDir Controllers/

esim: dotnet aspnet-codegenerator --project . controller -name PersonsController -m Person -dc FreeAzureSqlContext -outDir Controllers/
