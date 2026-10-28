---
style: page
title: Datu baseak
---
### 1. E/R sortu:
---
Erronka honetan, streaming-plataforma baten datu-basea diseinatu dugu, erabiltzaileak, profilak, edukiak eta harpidetzak modu antolatuan kudeatzeko. Horretarako, entitate-erlazio diagrama (ER diagrama) sortu dugu, sistemaren elementu nagusiak eta haien arteko erlazioak irudikatzeko.

Lehenik eta behin, erabiltzaileak eta perfilak definitu ditugu. Erabiltzaile bakoitzak bere datu pertsonalak ditu, hala nola NAN, helbide elektronikoa, izena, abizena eta pasahitza. Horrez gain, perfilak sortu eta kudea daitezke, perfil bakoitzak bere identifikatzailea du eta mota desberdineko izan ahal da (Pertsonala, Familiarra edo Infantila)

Bestalde, plataformak eskaintzen dituen edukiak ere definitu ditugu. Eduki bakoitzak identifikatzaile bat, izenburua, adin-sailkapena, deskribapena eta urtea ditu. Edukiak hiru motatan banatzen dira: pelikulak, dokumentalak eta serieak. Mota bakoitzak bere ezaugarri espezifikoak ditu. Adibidez, pelikulak; zuzendariaren izena eta pelikularen iraupena minututan eskatzen du, dokumentalak aldiz; iraupena minututan eta gaia (Natura eta animaliak, Kirolak, Gizartea eta kultura, Musika eta artea, Biografiak, Krimenak eta ikerketak). Serieak, berriz, denboraldietan banatzen dira, denboraldi bakoitzak zenbakietan identifikatzen da eta denboraldi bakoitzak hainbat kapitulu izan ditzake.

Horrez gain, erabiltzaileek harpidetza-plan desberdinak izan ditzakete. Bi plan mota definitu ditugu; estandarra eta premiuma. Plan bakoitzak bere ezaugarriak ditu, eta harpidetzen bidez erabiltzaileek plataformako zerbitzuetara sarbidea dute. Harpidetzek hasiera- eta amaiera-datak dituzte, eta horien bidez harpidetzaren iraupena kontrola daiteke.

Azkenik, entitateen arteko erlazioak eta kardinalitateak zehaztu ditugu, sistema osoaren funtzionamendua behar bezala irudikatzeko. Horrela, erabiltzaileen, profilen, edukien eta harpidetzen arteko loturak argi geratzen dira, eta datu-basearen egitura modu logiko eta antolatuan definitzen da.

Ondorioz, ER diagramaren helburua streaming-plataforma baten informazioa modu eraginkorrean antolatzea da, datuak behar bezala gordetzeko, erlazionatzeko eta etorkizunean kontsultatu eta kudeatu ahal izateko.

  ![digrama](img/db/1.png)

### 2. Modu erlazionala egin:
---
ER diagrama egin ondoren, zerrenda erlazionala sortu dugu, entitateak eta haien arteko erlazioak taula bihurtuz, atributuak zehaztuz eta gako primarioak (PK) eta gako arrotzak (FK) identifikatuz.
![eredu erlazioanala](img/db/1.png)


### 3. Datu basea normalizatu (1F-2F-3F):
---
Ondoren, datu-basearen normalizazioa landu dugu, hiru forma normalak aplikatuz. Lehen forma normalean (1F), atributu bakoitzak balio bakarra izatea eta datuak behar bezala antolatuta egotea ziurtatu dugu. Bigarren forma normalean (2F), menpekotasun partzialak aztertu ditugu, atributu bakoitza gako primario osoaren menpe egon dadin. Azkenik, hirugarren forma normalean (3F), menpekotasun iragankorrak aztertu ditugu, datuen errepikapenak eta eguneratze-arazoak saihesteko.


## HARPIDETZA

**Erlazioa:** `HARPIDETZA (ID_HARPIDETZA, Hasiera_data, Amaiera_data)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Bai. Ez dago dependentzia partzialik.
- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

## PLANA

**Hasierako erlazioa:** `PLANA (ID_PLANA, ID_HARPIDETZA, Mota)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `ID_PLANA` | `Mota` |
| `ID_HARPIDETZA` | — |

Deskonposizioa:

- `PLANA (ID_PLANA, Mota)`
- `PLANA (ID_PLANA, ID_HARPIDETZA)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

## ERABILTZAILEA

**Hasierako erlazioa:** `ERABILTZAILEA (NAN, ID_PLANA, Izena, Abizena, Pasahitza)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `NAN` | `Izena`, `Abizena`, `Pasahitza` |
| `ID_PLANA` | — |

Deskonposizioa (jatorrizko testuan adierazitakoa):

- `NAN (Izena, Abizena, Pasahitza)`
- `ERABILTZAILEA (EMAILA eta ID_PLANA)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

## PERFIL

**Hasierako erlazioa:** `PERFIL (ID_IZENA, NAN, Pertsonala, Familiarra, Infantila)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `ID_IZENA` | `Pertsonala`, `Familiarra`, `Infantila` |
| `NAN` | — |

Deskonposizioa:

- `ID_IZENA (Pertsonala, Familiarra, Infantila)`
- `PERFIL (ID_IZENA eta NAN)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

## IKUSI

**Hasierako erlazioa:** `IKUSI (ID_IZENA, ID_EDUKIAK, Bistaratzea)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `ID_IZENA` | — |
| `ID_EDUKIAK` | — |
| `IKUSI` | `Bistaratzea` |

Deskonposizioa:

- `IKUSI (ID_IZENA eta ID_EDUKIAK, Bistaratzea)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

## EDUKIAK

**Erlazioa:** `EDUKIAK (ID_EDUKIAK, Adin_sailkapena, Izenburua, Urtea, Deskribapena, Izenburua, Mota)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Bai. Ez dago dependentzia partzialik.
- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

## PELIKULAK

**Erlazioa:** `PELIKULAK (Zuzendaria, Iraupena_min)`

- **IDa:** EDUKIKO FK (`id`).
- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Bai. Ez dago dependentzia partzialik.
- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik.

---

## DOKU

**Erlazioa:** `DOKU (Gaia, Iraupena_min)`

- **IDa:** EDUKIKO FK (`id`).
- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Bai. Ez dago dependentzia partzialik.
- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik.

---

## SERIEAK

- **IDa:** EDUKIKO FK (`id`).
- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Bai. Ez dago dependentzia partzialik.
- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik.

---

## DENBORALDIAK

**Hasierako erlazioa:** `DENBORALDIAK (ID_DENBORALDIA, ID_EDUKIAK, Zenbakia)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `ID_DENBORALDIA` | `Zenbakia` |
| `ID_EDUKIAK` | — |

Deskonposizioa:

- `ID_DENBORALDIAK (Zenbakia)`
- `DENBORALDIAK (ID_DENBORALDIA, ID_EDUKIAK)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

## KAPITULUAK

**Hasierako erlazioa:** `KAPITULUAK (ID_KAPITULUA, ID_DENBORALDIA, Izena)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `ID_KAPITULUA` | `Izena` |
| `ID_DENBORALDIA` | — |

Deskonposizioa:

- `ID_KAPITULUA (Izena)`
- `ID_DENBORALDIAK (ID_KAPITULUA, ID_DENBORALDIA)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).



### 4. Datu basea ACCESS-en implementatu:
---
Prozesu honen esker, datu-basearen egitura koherenteagoa eta eraginkorragoa lortu nahi izan dugu, informazioa modu egokian gordetzeko, erlazionatzeko, kontsultatzeko eta eguneratzeko. Horrela, streaming-plataformaren erabiltzaileak, profilak, edukiak, planak eta harpidetzak modu antolatuan kudeatu ahal izango dira.