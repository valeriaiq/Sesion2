# Sesion2


Postwork Sesión 2

1. Importa los datos de soccer de las temporadas 2017/2018, 2018/2019 y 2019/2020 
de la primera divisi?n de la liga espa?ola a `R`, los datos los puedes 
encontrar en el siguiente enlace: https://www.football-data.co.uk/spainm.php

``` R
setwd("C:/Users/usuario/Documents/PostworkS2")

LE1718 <- "https://www.football-data.co.uk/mmz4281/1718/SP1.csv"
LE1819 <- "https://www.football-data.co.uk/mmz4281/1819/SP1.csv"
LE1920 <- "https://www.football-data.co.uk/mmz4281/1920/SP1.csv"

download.file(url = LE1718, destfile = "LE-1718.csv", mode = "wb")
download.file(url = LE1819, destfile = "LE-1819.csv", mode = "wb")
download.file(url = LE1920, destfile = "LE-1920.csv", mode = "wb")

dir()

```

2. Obten una mejor idea de las caracter?sticas de los data frames al usar 
las funciones: `str`, `head`, `View` y `summary`

``` R
ligaesp1 <- read.csv("LE-1718.csv")
ligaesp2 <- read.csv("LE-1819.csv")
ligaesp3 <- read.csv("LE-1920.csv")

str(ligaesp1); str(ligaesp2); str(ligaesp3)
head(ligaesp1); head(ligaesp2); head(ligaesp3)
View(ligaesp1); View(ligaesp2); View(ligaesp3)
summary(ligaesp1); summary(ligaesp2); summary(ligaesp2)

```

3. Con la funci?n `select` del paquete `dplyr` selecciona ?nicamente 
las columnas `Date`, `HomeTeam`, `AwayTeam`, `FTHG`, `FTAG` y `FTR`;
esto para cada uno de los data frames. (Hint: tambi?n puedes usar `lapply`).

``` R
library(dplyr)

LEC1 <- select(ligaesp1, Date, HomeTeam, AwayTeam,FTHG,FTAG,FTR)
LEC2 <- select(ligaesp2, Date, HomeTeam, AwayTeam,FTHG,FTAG,FTR)
LEC3 <- select(ligaesp3, Date, HomeTeam, AwayTeam,FTHG,FTAG,FTR)
# 4. Aseg?rate de que los elementos de las columnas correspondientes de
# los nuevos data frames sean del mismo tipo (Hint 1: usa `as.Date` y `mutate`
# para arreglar las fechas). 
# Con ayuda de la funci?n `rbind` forma un ?nico data frame que contenga 
# las seis columnas mencionadas en el punto 3 
# (Hint 2: la funci?n `do.call` podr?a ser utilizada).
str(LEC1);str(LEC2);str(LEC3);
LEC1$Date<- as.Date(LEC1$Date,"%d/%m/%y")
LEC2$Date<- as.Date(LEC2$Date,"%d/%m/%y")
LEC3$Date<- as.Date(LEC3$Date,"%d/%m/%y")
str(LEC1);str(LEC2);str(LEC3);

LEF <- rbind(LEC1,LEC2,LEC3)
str(LEF)
```
