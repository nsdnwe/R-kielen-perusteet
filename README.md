R-kielen perusteet 
===================

R-kieli on ensisijaisesti tilastolliseen laskentaan ja grafiikan tuottamiseen tarkoitettu skripti-/ohjelmointikieli, jota käytetään paljon esim. koneoppimisjärjestelmien (machine learning) kehityksessä.

R-kieli on avoimen lähdekoodin GNU GPL -lisenssin alainen.

R-kieli on helposti laajennettavissa ja tänä päivänä siihen on saatavilla yli 10 000 laajennuspakettia eri käyttötarkoituksiin.

Kehitysympäristö
=====

R-skriptien kehitystä voi toteuttaa mm. 

* Rstudiolla <https://www.rstudio.com/> (avointa lähdekoodia)
* Selainympäristössä, esim. Rextester <http://rextester.com> 
	* Valitse language-valinnasta R
* Visual Studiolla <https://www.visualstudio.com/downloads/> 
	* Katso lisätietoja asennuksesta <https://docs.microsoft.com/en-us/visualstudio/rtvs/installation>

Tämän dokumentin esimerkit on toteutettu Rextesterillä ja **suosittelen** käyttäämään sitä harjoituksissa.

Yleistä
=====

Kommentointi
-----

*	Kommentit alkavat `#`-merkillä.
```
# My comment here
```

Arvon määritys muuttujalle
-----

* Arvo muuttujalle määritetään `<-`-merkeillä. Tämä on siis vastaava kuin `=`-merkki useissa muissa ohjelmointikielissä.
* Muuttujan nimi voi sisältää myös pisteitä. Pisteellä ei siis viitata luokan jäseniin tms., vaan kyse on pelkästään muuttujan nimestä.
```
myvar <- 123
my.other.var <- "abc"
```

Muuttujien arvon esittäminen konsolissa
-----

* Muuttujan nimen syöttäminen näyttää sen arvon konsolissa.
```
myvar <- 123
myvar
---
123
```
*	Voit käyttää myös funktiota `print()`.
```
myvar <- 123
print(myvar)
---
123
```

Vektorit
=====

* Vektori on yksiulotteinen taulukko, eli esim. numerosarja `1, 2, 4, 6, 8`.
* Vektorin kaikki arvot ovat samaa tietotyyppiä, eli esim. kokonaislukuja (`int`).

Vektorin luonti
-----

* Uusi vektori luodaan funktiolla `c()`, jolle annetaan parametreina vektorin arvot.
```
myvector <- c(1, 2, 3)
```

Vektorien summaus, vähennys, jako- ym. operaatiot
-----

* Vektoreita voi laskea yhteen, vähentää ym. kuten tavallisia muuttujia.
```
v1 <- c(1, 2, 3)
v2 <- c(2, 4, 5)
v3 <- v1 + v2
v3
v4 <- v3 * 100
v4
---
[1] 3 6 8
[1] 300 600 800
```

Laskuoperaattorit
-----
*	Lisäys: +
*	Vähennys: -
*	Kerto: *
*	Jako: /
*	Exponentti: ^
*	Jakojäännös: %%

Vektorin elementtien nimeäminen
-----

* Usein on tarpeellista antaa vektorin elementeille nimet, jotka näkyvät tuloksissa ja johon voidaan viitata pelkän indeksinumeron sijaan.
* Nimeäminen tapahtuu funktiolla `names()`.
```
v1 <- c(1, 2, 3)
names(v1) <- c("Apples", "Carrots", "Lemons")
v1 
---
Apples Carrots  Lemons 
     1       2       3
```

Tilastofunktioita
-----

* R sisältää lukuisia tilastofunktioita ja lisämoduulien avulla kirjoa voi laajentaa.
* Yleisimpiä ovat mm. `sum()`, `min()`, `max()`, `sd()`, `median()`, `mean()`.
```
v1 <- c(1, 8, 17)
sum(v1)
mean(v1)
---
[1] 26
[1] 8.666667
```

Viittaus vektorin jäseniin
---

* Vektorin jäseniin voi viitata jäsenen indeksillä tai nimellä, mikäli nimi on määritettynä `names()`-funktiolla.
* Huomaa, että indeksit alkavat arvosta 1.
* Kaksoispisteellä on mahdollista valita tietty alue indeksejä.
* Mikäli on tarve viitata useaan vektorin jäseneen, tämä on mahdollista antamalla viitattavat jäsenet omana vektorina. Katso esimerkki alla.
```
v1 <- c(1, 20, 17, 6)
names(v1) <- c("Apples", "Carrots", "Lemons", "Grapes")
v1[3]
v1["Carrots"]
v1[c(2,4)] # items 2 and 4
v1[c(1:3)] # items 1 to 3
v1[c("Apples", "Lemons")] # named items
---
Lemons 
    17 
Carrots 
     20 
Carrots  Grapes 
     20       6 
 Apples Carrots  Lemons 
      1      20      17 
Apples Lemons 
     1     17 
  name quantity
1 Cats      123
2 Dogs      432
```

Vektorien vertailu
-----

* Vektorien arvoja voi verrata yhteen muuttujan arvoon alkioittain tai toiseen saman kokoiseen vektoriin.
```
v1 <- c(1, 20, 17, 6)
v1 > 10

v2 <- c(4, 12, 23, 13)
v1 > v2
---
[1] FALSE  TRUE  TRUE FALSE
[1] FALSE  TRUE FALSE FALSE
```

Vektorin arvojen nimien haku
-----

* Yllä kuvatussa esimerkissä vastaukseksi muodostuu totuusarvoja (`TRUE`/`FALSE`) sisältävä vektori.
* Mikäli haluat palauttaa vain ne vektorin arvot, jotka täyttävät halutun ehdon, käytä alla kuvattua mallia.
```
v1 <- c(1, 20, 17, 6)
names(v1) <- c("Apples", "Carrots", "Lemons", "Grapes")

v2 <- v1 > 10 
v1[v2]
---
Carrots  Lemons 
     20      17 
```

Matriisit
=====

* Matriisi on yleensä kaksiulotteinen taulukko, jonka elementteihin voi viitata rivi- ja sarakenumeron avulla.
* Matriisin kaikki elementit ovat samaa tietotyyppiä.

Matriisin luonti
-----

* Uusi matriisi luodaan funktiolla `matrix()`, jolle annetaan vähintään kolme argumenttia:
	* Matriisin arvot (vektori)
	* `byrow` = TRUE/FALSE (täytetäänkö matriisi "Matriisin arvot" -parametrin arvoilla rivi kerrallaan vai sarake kerrallaan)
	* `nrow` = matriisin rivien määrä

```
v1 <- c(1, 2, 3, 4, 5, 6, 7, 8, 9) # Same as v1 <- c(1:9)
m1 <- matrix(v1, byrow = TRUE, nrow = 3)
m1
---
     [,1] [,2] [,3]
[1,]    1    2    3
[2,]    4    5    6
[3,]    7    8    9
```

Usean vektorin yhdistäminen matriisiksi
-----

* Matriisi voidaan luoda useasta vektorista antamalla matriisin luonnissa matriisin arvoiksi vektori, joka sisältää useita vektoreita.
```
v1 <- c(10, 20)
v2 <- c(33, 44)
v3 <- c(55, 60)
vv <- c(v1, v2, v3)

matrix(vv, byrow = TRUE, nrow = 3)
---
     [,1] [,2]
[1,]   10   20
[2,]   33   44
[3,]   55   60
```

Matriisin rivien ja sarakkeiden nimeäminen
-----

* Matriisin riveille ja sarakkeille voi antaa nimet lähes samalla tavoin kuin vektorin sarakkeille, käyttämällä funktioita `colnames()` ja `rownames()` 

```
v1 <- c(10, 20)
v2 <- c(33, 44)
v3 <- c(55, 60)
vv <- c(v1, v2, v3)

m1 <- matrix(vv, byrow = TRUE, nrow = 3)

colnames(m1) <- c("Apples", "Carrots")
rownames(m1) <- c(2017, 2018, 2019)

m1
---
     Apples Carrots
2017     10      20
2018     33      44
2019     55      60
```

Viittaus matriisin jäseniin
---

* Matriisin jäseniin voi viitata jäsenen rivi- ja sarakenumerolla (indekseillä) tai näiden nimillä.
* Huomaa, että indeksi alkaa arvosta 1.
* Kaksoispisteellä on mahdollista valita tietty alue indeksejä.

```
m1[2,2]        # Select a single element
m1[,2]         # Select a single column (note transposed result)
m1[1:2,]       # Select rows from 1 to 2
m1[, "Apples"] # Select Apples column (note transposed result)
---
[1] 44

2017 2018 2019 
  20   44   60 

     Apples Carrots
2017     10      20
2018     33      44

2017 2018 2019 
  10   33   55 
```

Matriisin rivi- ja sarakesummat
-----

* Matriisin rivi- ja sarakkeiden summat voi laskea funktiolla `rowSums()` ja `colSums()`.

```
rowSums(m1)
colSums(m1)
---
2017 2018 2019 
  30   77  115 

 Apples Carrots 
     98     124 
```

Rivien ja sarakkeiden lisääminen matriisiin
-----

* Uusia rivejä ja sarakkeita voi lisätä olemassa olevaan matriisiin funktioilla `rBind()` ja `cBind()`.
```
v1 <- c(10, 20)
v2 <- c(33, 44)
v3 <- c(55, 60)
vv <- c(v1, v2, v3)

m1 <- matrix(vv, byrow = TRUE, nrow = 3)

colnames(m1) <- c("Apples", "Carrots")
rownames(m1) <- c(2017, 2018, 2019)

# Let's add col and row sums
m2 <- cbind(m1, rowSums(m1))
m3 <- rbind(m2, colSums(m2))

m3
---
     Apples Carrots    
2017     10      20  30
2018     33      44  77
2019     55      60 115
         98     124 222
```

Faktorit
=====

* Faktoreilla voi rajoittaa muuttujan mahdollisia arvoja.
* Esim. muuttujalle `gender` voidaan rajoittaa mahdollisiksi arvoiksi vain `Male` ja `Female`.
* Faktorit on jaettu kahteen tyyppiin
	* Nominal categorical variables
		* Ei tiettyä järjestystä
		* Esim. Red, Blue, Green jne.
	* Ordinal categorical variables
		* Jäsenillä on järjestys, jolla voidaan jaotella tuloksia
		* Esim. Low, Medium, High
			
Faktorien luonti
-----

* Uusi faktori luodaan funktiolla `factor()`.
* Faktorin arvot on mahdollista luoda analysoitavasta datasta tai antamalla ohjelmallisesti.

```
f1 <- factor(c("Apples", "Carrots", "Lemons", "Grapes")) # Nominal
f1

v2 <- c("Low", "Medium", "High") 
f2 <- factor(v2, order = TRUE, levels = v2) # Ordinal
f2
---
[1] Apples  Carrots Lemons  Grapes 
Levels: Apples Carrots Grapes Lemons

[1] Low    Medium High  
Levels: Low < Medium < High
```

Data framet eli Data setit
=====

* Data frame (Data set) on yleensä kaksiuloitteinen taulukko, jonka elementteihin voi viitata rivi- ja sarakenumeron avulla.
* Toisin kuin matriiseissa, eri sarakkeiden elementit voivat olla eri tietotyyppejä.

Data framen luonti
-----

* Uusi data frame luodaan funktiolla `data.frame()`, jolle annetaan parametreina sarakkeiden arvovektorit.

```
vegetable <- c("Carrots", "Tomatoes")
quantity <- c(123, 432)
data.frame(vegetable, quantity)
---
  vegetable quantity
1   Carrots      123
2  Tomatoes      432
```

Malli- data framet
-----

* R-kieli sisältää valmiina useita malli- data frameja, joita käytetään mm. harjoituksissa ja demoissa.
* Lista käytettävissä olevista malli- data frameista on listattavissa funktiolla `data()`

```
data()
---
Data sets in package ‘datasets’:

AirPassengers           Monthly Airline Passenger Numbers 1949-1960
BJsales                 Sales Data with Leading Indicator
BJsales.lead (BJsales)
                        Sales Data with Leading Indicator
BOD                     Biochemical Oxygen Demand
CO2                     Carbon Dioxide Uptake in Grass Plants
ChickWeight             Weight versus age of chicks on different diets
DNase                   Elisa assay of DNase 
jne ... 
```

Data framen sisällön esitys
-----

* Data framen koko sisältö voidaan esittää konsolissa samalla tavoin kuin muidenkin R-muuttujien eli syöttämällä pelkkä data framen nimi.
* Usein data framet ovat laajoja, joten on tarpeellista rajoittaa esitettävän tiedon määrää esim. käyttämällä funktiota `head()`, joka palauttaa jonkin verran ensimmäisiä rivejä data framesta.

```
head(mtcars) # mtcars is a sample data frame embedded in the R language
```

* Data framen rakenteen voi kuvailla funktiolla `str()`.

```
str(mtcars)
---
'data.frame':	32 obs. of  11 variables:
 $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
 $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
 $ disp: num  160 160 108 258 360 ...
```

* Yhteenvedon data framen sarakkeista saa funktiolla `summary()`.

```
summary(mtcars)
---
      mpg             cyl             disp             hp       
 Min.   :10.40   Min.   :4.000   Min.   : 71.1   Min.   : 52.0  
 1st Qu.:15.43   1st Qu.:4.000   1st Qu.:120.8   1st Qu.: 96.5  
 Median :19.20   Median :6.000   Median :196.3   Median :123.0  
 Mean   :20.09   Mean   :6.188   Mean   :230.7   Mean   :146.7  
 3rd Qu.:22.80   3rd Qu.:8.000   3rd Qu.:326.0   3rd Qu.:180.0  
 Max.   :33.90   Max.   :8.000   Max.   :472.0   Max.   :335.0  
      drat             wt             qsec             vs        
 Min.   :2.760   Min.   :1.513   Min.   :14.50   Min.   :0.0000 
jne...
```

Viittaus data framen jäseniin
---

* Data framen jäseniin voi viitata jäsenen rivi- ja sarakenumerolla (indekseillä) tai näiden nimillä.
* Kaksoispisteellä on mahdollista valita tietty alue indeksejä.

```
mtcars[1:3, "cyl"] # Rows 1 to 3 of column cyl
mtcars[, "cyl"] # Whole single column of data (transposed)
```

* Koko sarakkeeseen voi viitata myös $-merkillä.

```
mtcars$cyl  # Same as mtcars[, "cyl"]
```

Data framen suodattaminen (filtteröinti)
-----

* Suodattamalla data framesta voidaan luoda uusi data frame, jossa on vain osa alkuperäisen data framen tiedoista. Tämä tapahtuu funktiolla `subset()`.

```
subset(mtcars, cyl == 4 & gear == 4)
```

* Loogiset operaattorit, joita filtteröinnin ehdoissa voi käyttää ovat
	* & = ja
	* | = tai
	* ! = ei

* Suodatettuun data frameen on mahdollista valita vain osa alkuperäisen data framen sarakkeista `select =` -parametrin avulla.

```
subset(mtcars, cyl == 4 & gear == 4, select = mpg:disp) # Only columns from mpg to disp
```

Data framen järjestäminen
-----

* Data framen tiedot voi järjestää funktiolla `order()`.
* `order()` palauttaa vain indeksivektorin, joten varsinainen järjestetty data frame täytyy luoda uudelleen indeksi-vektorin avulla.

```
mtcars[order(mtcars$disp),] # Order by disp-column
```

* Käänteinen tulosjärjestys on mahdollista valita parametrilla `decreasing=TRUE`.

```
mtcars[order(mtcars$disp, decreasing=TRUE),]
```

Listat
=====

* Lista on vektori, jonka jäsenet voivat olla eri tietotyyppejä

Listan luonti
-----

* Uusi lista luodaan funktiolla `list()`, jolle annetaan parametreina listan jäsenet vastaavalla tavalla kuin vektorin luonnissa.

```
v1 = c(123, 456)
m1 <- matrix(1:9, byrow = TRUE, nrow = 3)
l1 <- list("abc", v1, m1)
l1
---
[[1]]
[1] "abc"

[[2]]
[1] 123 456

[[3]]
     [,1] [,2] [,3]
[1,]    1    2    3
[2,]    4    5    6
[3,]    7    8    9
```

Viittaus listan jäseniin
-----

* Listan jäseniin voi viitata jäsenen indeksinumerolla, muuttujan nimellä tai annetulla nimellä.

```
v1 = c(123, 456)
m1 <- matrix(1:9, byrow = TRUE, nrow = 3)
l1 <- list(my.name = "abc", my.vec = v1, my.matrix = m1)

l1[2]
l1$my.name
---
$my.vec
[1] 123 456

[1] "abc"
```

Kirjastot (kirjastopaketit)
=====

* R-kehitysympäristö sisältää yleensä useita valmiita kirjastoja.
* Listan käytettävissä olevista kirjastoista voi hakea funktiolla `library()`.
* Kirjaston voi ottaa käyttöön funktiolla `library("Kirjaston nimi")`.
* Lista niistä kirjastoista, jotka ovat jo käytössä (eli joita ei tarvitse erikseen ottaa käyttöön funktiolla `library()`) saa funktiolla `search()`
* Edellä mainittujen lisäksi R-kieleen on olemassa yli 10 000 valmista avoimen lähdekoodin kirjastoa, jotka on koottu CRAN-projektiin.
* Helppo tapa etsiä haluttua kirjastoa (pakettia) CRAN:ista on käyttää hakusivua https://mran.microsoft.com/packages/
* Kirjaston asennus tapahtuu funktiolla `install.packages()`.
* Latauksen jälkeen kirjaston käyttöönotto tapahtuu funktiolla `library()`.

```
install.packages("readxl")
library("readxl")
```

Omat funktiot
=====

* Mikäli valmiista kirjastoista ei löydy tarvittavia funktiota tai muusta syystä on tarpeen tehdä omia käsittelysääntöjä, tämä on mahdollista funktioiden avulla
* Funktiot voivat sisältää yleisimpiä ohjelmoinnin käskyjä, kuten esim. `if`/`else`, `for`, `while`, `switch`
* Funktion määrittely tapahtuu avainsanalla `function()`.

Funktion esittely
-----
```
f1 <- function(a, b) {
    if (a > b) return(TRUE) else return(FALSE)
}
        
f2 <- function(x) return(x * 2) # One line function

f3 <- function(x = 5) return(x / 2) # Parameter default value
    
f1(1,2)
f2(24)
f3()
---
[1] FALSE
[1] 48
[1] 2.5
```

Silmukat
-----

* Silmukoita voi toteuttaa avainsanoilla `for()`, `while()` ja `repeat()`.

```
v1 <- c(10, 25, 60)

# For
for(item in v1) {
  print(item)    
}

# while
counter <- 0
while (counter < 5) {
  print (counter)
  counter <- counter + 1
}
---
[1] 10
[1] 25
[1] 60
[1] 0
[1] 1
[1] 2
[1] 3
[1] 4
```

Ehtolauseet
-----

* Ehtolauseita voi toteuttaa avainsanoilla `if()`, `else`, `else if()` ja `switch()`.

```
counter <- 0
repeat {
  print (counter)
  if(counter > 2) { 
    break # Exit loop
  } else {
    counter <- counter + 1
  }
}
---
[1] 0
[1] 1
[1] 2
[1] 3
```

Tietotyypit
=====

* R-kielen perustietytyyppejä ovat:
  * Looginen (Boolean).
    `v <- TRUE` 
  * Merkkijono (Character).
    `v <-	"ABC"
  * Desimaaliluku (Numeric).
    `v <- 12.3`
  * Kokonaisluku (Integer).
    `v <- 123L`
  * Kompleksiluku (Complex).
    `v <- 1.23+2i`

Tietotyyppien muunnos
-----

* Tietotyyppejä voi muuntaa `as.`-alkuisilla funktiolla, joita ovat `as.numeric()`, `as.logical()`, `as.integer()`, `as.factor()`, `as.character()` ja `as.ordered()`.

```
as.numeric(c("3", "4abc5", "6,0", "7.0"))
---
[1] 3 NA NA  7
Warning message:
NAs introduced by coercion
```

Tietotyypin tarkastus
-----

* Muuttujan tietotyypin voi tarkastaa funktiolla `class()`.

```
v <- 123L
class(v)
---
[1] "integer"
```

Grafiikka
=====

* R-kehitysympäristössä on monia tapoja esittää tietoja graafisessa muodossa.
* Hyviä esimerkkejä löytyy esim. osoitteesta http://www.r-graph-gallery.com/

```
plot(x = pressure$temperature, y = pressure$pressure, type = "l") # Line chart. Pressure is a sample data frame embedded in R-language
lines(x = pressure$temperature, y = pressure$pressure/2, col = "red") # Add second line in the same diagram
barplot(height = BOD$demand, names.arg = BOD$Time) # Bar diagram
plot(x = mtcars$wt, y = mtcars$mpg) # Scatter plot
hist(mtcars$mpg) # Histogram
plot(density(mtcars$mpg)) # Density

library(ggplot2) 
qplot(x = mtcars$wt, y = mtcars$mpg) # Scatter plot version 2
qplot(mtcars$cyl, geom = "bar") # Bar diagram version 2
```

Tiedon haku eri lähteistä
=====

* Käsiteltävää tietoa on mahdollista hakea mm. tekstitiedostoista, Excel-tiedostoista, REST-rajapinnoista ja eri tietokannoista.
* Alla on kuvattuna muutamia esimerkkejä. Eri tietokannoista tai muista järjestelmistä tietojen hakuun kannattaa etsiä tietoa tapauskohtaisesti.

Tekstitiedostot
-----

* CSV-muotoisia (pilkuin erotellut rivit) tekstitiedostoja voi lukea data frame -muotoon funktiolla `read.csv()`.

```
Esimerkkitiedoston c:\mydata.txt sisältö

"Fruit", "Quantity"
"Apples", 123
"Cherries", 321
"Bananas", 543
```

```
mydata <- read.csv("c:\\mydata.txt", header = TRUE, sep = ",")
mydata
---
     Fruit Quantity
1   Apples      123
2 Cherries      321
3  Bananas      543
```

Excel-tiedostot
----

* Excel-tiedostoja voi lukea data frame -muotoon esim. `readxl`-kirjaston avulla.

```
install.packages("readxl")
library("readxl")
mydata <- read_excel("c:\\testing\\mydata.xlsx")
```

Rest-rajapinta
-----

* REST-rajapinnoista voi lukea JSON-muotoista tietoa esim. `jsonlite`-kirjaston avulla.

```
library(jsonlite)
mydata <- fromJSON("http://services.groupkt.com/country/search?text=un", flatten = TRUE)
head(mydata)
```

Paikallinen MySQL-tietokanta
-----

* Yhteyden muodostus MySQL-tietokantaan tapahtuu `RMySQL`-kirjaston avulla.

```
install.packages("RMySQL")
library(RMySQL)
my.conn <- dbConnect(MySQL(), user = 'root', password = 'mypassword', dbname = 'mydatabase', host = 'localhost')
result <- dbSendQuery(mysqlconnection, "SELECT * FROM MyTable")

my.data <- fetch(result, n = 5)
head(my.data)
```

Azure SQL -tietokanta
-----

Yhteyden muodostus Azure SQL tietokantaan tapahtuu `RODBC`-kirjaston avulla seuraavasti:

* Avaa Azure Portal ja valitse tietokanta, johon haluat luoda yhteyden
* Jotta kehitystyöasemasta voi ottaa yhteyden Azure SQL -tietokantaan, varmista että "Set server firewall" -kohdassa on mukana kehitystyöaseman IP-osoite
* Valitse linkki "Show database connection strings" ja kopioi ODBC-yhteyslause esim. alla näkyvän esimerkin `my.conn.string`-muuttujaan. Korjaa salasana.

```
library(RODBC) 
my.conn.string <- "Driver={ODBC Driver 13 for SQL Server};Server=tcp:oghlllivqt.database.windows.net,1433;Database=MyDatabaseName;Uid=MyUid;Pwd=MyPassword;Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;"
my.conn <- odbcDriverConnect(my.conn.string)

my.data <- sqlQuery(my.conn, "SELECT * FROM MyTable")
head(my.data)

odbcCloseAll()
```

NSD Consulting Oy
-----

**Vaativien asiakasohjelmistojen suunnittelu ja toteutus**

www.nsd.fi
