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
kts. https://learn.microsoft.com/en-us/ef/core/cli/dotnet
Tee EF-model aiemman osan tietokannasta.
ConnectionString:n saa kopioitua Azuresta, ja voit sen jälkeen luoda mallin:
dotnet ef dbcontext scaffold komennolla.