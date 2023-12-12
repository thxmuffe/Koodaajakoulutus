# Koodaajakoulutus
Koodaajakoulutus (ASP.NET + React) esimerkit 


Azure SQL server:
- public access: käy laittamassa Networking-näkymästä public access päälle.
    (Excptions: allow azure services...)
- Tämän jälkeen Azure/Data Studio ehtottaa poikkeuksia palomuuriin automaattisesti.salli ko. IP-osoite ennen kun yrität yhdistää tietokantaan Azure Data Studiolla.
- Huom Azure Data Studiolla kytkeydytään tietokannan SQL-login tunnuksilla.


Voit tehdä "New query" napilla uuden taulun omaan tietokantaasi, esimerkkinä

CREATE TABLE Persons (
    Personid int IDENTITY(1,1) PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);

Voit lisätä rivejä esim. INSERT INTO [dbo].[Persons] (LastName,FirstName,Age)
VALUES ('Penttilä', 'Paavo', 44);

WebAPI:
Voit yksinkertaistaa launch-settings tiedostoa, jättää ainoastaan https-version, jolloin vähemmän epäselvyttää mikä profiili käytössä. Voit testata WeatherController contolleria esim: https://localhost:7183/WeatherForecast

Käyttääksesi Entity Framework:iä, sinun pitää asentaa projektiisi tarvittavat EF-nuget:t
- Voit käyttää Nuget Package Manager GUI VSC-Extensioniä
- VSC Extensio Nuget Galleri
- Tai komentoriviltä

Tarvittavat paketit:
Microsoft.EntityFrameworkCore
Microsoft.EntityFrameworkCore.SqlServer
Microsoft.EntityFrameworkCore.Design
Microsoft.EntityFrameworkCore.Tools

salasana esim. Str#ng_Passw#rd

kts. https://learn.microsoft.com/en-us/ef/core/cli/dotnet
Tee EF-model aiemman osan tietokannasta esim:
     dotnet ef dbcontext scaffolding "<connectiomString>" adapteri -o <outputkansio>
ConnectionString:n saa kopioitua Azuresta, ja voit sen jälkeen luoda mallin:
dotnet ef dbcontext scaffold komennolla.

Kun sinulla on EF-malli luoto, lisää uusi kontroller ohjelmaasi, joka tallettaa uuden henkilön persons kantaan. Tai hakee listan Persons taulussa olevista henkilöistä.

Kontrolleri kannattaa tehdä käsin, mutta voit myös aluksi tehdä sen automaattisesti komentoriviltä, jolloin näet millainen siitä pitäisi tulla. kts. https://learn.microsoft.com/en-us/aspnet/core/fundamentals/tools/dotnet-aspnet-codegenerator?view=aspnetcore-8.0

dotnet aspnet-codegenerator --project . controller -api -name YOUR_CONTROLLER_NAME -m YOUR_MODEL_NAME -dc YOUR_DB_CONTEXT_CLASS -outDir Controllers/

esim: dotnet aspnet-codegenerator --project . controller -name PersonsController -m Person -dc FreeAzureSqlContext -outDir Controllers/

Tällä tavalla teki sellaisen kontrollerin, joka olisi vaatinut jotain lisäosia. En pystynyt ratkaisemaan sitä, joten ten sen samalla tavalla kuin WeatherController, joka toimii, eli esim:
// GET: Persons
        [HttpGet(Name = "GetPersons")]
        public IEnumerable<Person> Get()
        {
              return _context.Persons.ToArray();
        }

o	Pitää laittaa kontrollerille:
	    [apicontroller] 
    	[Route("[controller]")]
o	Get-Metodille metodi-attribuutit
	    [HttpGet(Name = "GetPersons")]

Joudut myös lisäämään Program.cs:n alkuun kytkennät mm. tietokannan ja kontrollerin välille.

builder.Services.AddDbContext<FreeAzureSqlContext>();
Selitys: Kun tullaan kontrollerin esim. get-persons metodiin, ASP.NET framework kutsuu silloin db-kontekstin initialisointia ja yhdistään DbContext luokan aitoon tietokantaan (käyttäen haluttua tietokantayhteyttä / connectionString). Jos AddDbContext() kutsu puuttuu Programista, framework ei pysty yhdistämään kontrolleria oikeaan tietokantaan.


Lisäksi:
- builder.Services.AddControllers();

Ja jos käytät Razor pages / views, niin:
- optionally: builder.Services.AddControllersWithViews();


Kun luot Azuree web_appia, deployment osuuden voi määritellä joko heti luontivaiheessa, tai myöhemmin (Deployment Center)