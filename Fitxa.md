# Fitxa 1 — Anàlisi inicial de MusicCloud

**Nom i cognoms:** Gerard Planas Tort________________________________________  
**Data:** _22/09/26_________________  
**Equip / parella:** _________________________________________

## Objectiu

MusicCloud necessita reorganitzar la seva infraestructura informàtica. Abans d'instal·lar o configurar cap servei, cal entendre:

- qui treballa a l'empresa;
    
- quines funcions té cada persona;
    
- quins recursos existeixen;
    
- qui necessita accedir a cada recurs;
    
- com podem gestionar aquests accessos de manera eficient.
    

---

# 1. Conèixer MusicCloud

Consulta la informació disponible sobre els departaments, treballadors i perfils d'usuari de MusicCloud.

Completa la taula següent.

|| Aina Ciurans | Direcció | Usuari estàndard de Direcció | Sí. Direcció té accés L/E gairebé a tots els recursos de l'empresa (comuns, propis i interdepartamentals), ja que supervisa el conjunt de l'organització. |
| Rut Tornil | Direcció | Usuari estàndard de Direcció | Sí, pel mateix motiu que Aina Ciurans: Direcció necessita visió i control globals sobre la resta de departaments. |
| Dídac Gassó | Administració | Usuari estàndard | No. Accedeix als recursos propis del departament (`compartida`, `documentacio_interna`) i als comuns de l'empresa, sense permisos addicionals. |
| Laia Macias | Administració | Cap de departament | Sí. Com a responsable, és l'única persona amb accés de lectura/escriptura a `gestio_departament` (carpeta restringida al cap). |
| Estel Birosta | Suport tècnic | Usuari estàndard | Possiblement sí, de forma puntual. Suport tècnic pot rebre accés temporal (ATP) a `usuaris`, `logs`, `configuracions` i `inventari` per resoldre incidències concretes, sempre justificat i registrat. |
| Aina Zuriguel | Suport tècnic | Usuari estàndard | Igual que Estel Birosta: accés ATP puntual per gestionar incidències, a més dels recursos habituals del departament. |
| Lluïsa Richart | Suport tècnic | Cap de departament | Sí. Com a responsable, té accés exclusiu de lectura/escriptura a `gestio_departament` i `scripts` del seu departament. |
| Roser Alberch | Producció musical | Usuari estàndard | No. Treballa amb els recursos propis del departament (`compartida`, `artistes`, `cataleg`) i els comuns, sense privilegis especials. |
| Guillem Adella | Producció musical | Usuari estàndard | No. Mateixes necessitats que la resta d'usuaris estàndard del departament. |
| Meritxell Reglat | Producció musical | Cap de departament | Sí. Accés restringit de lectura/escriptura a `gestio_departament`, a més de coordinar el contingut amb Suport tècnic (accés ATP d'aquest a `cataleg`). |
| Alícia Monclús | Producció musical | Usuari estàndard | No. Necessitats bàsiques d'usuari del departament. |
| Carles Molins | Producció musical | Usuari estàndard | No. Necessitats bàsiques d'usuari del departament. |
| Eulàlia Galcera | Producció musical | Usuari estàndard | No. Necessitats bàsiques d'usuari del departament. |
| Talia Costas | Informàtica | Cap de departament / Administrador del sistema | Sí, i de nivell alt. A més de l'accés `R: L/E` a `gestio_departament`, el departament d'Informàtica té permisos ADM sobre `administracio_sistema` (backups, logs, configuracions) i accés ADM tècnica a les carpetes personals dels usuaris. |
| Alex Soriano | Informàtica | Administrador del sistema | Sí. Com a membre d'Informàtica, necessita permisos ADM per crear/modificar usuaris, gestionar grups, configurar serveis i revisar logs i backups. |
| Pere Espinalt | Externs | Usuari extern | Sí, però limitats. Només ha d'accedir a `comu/intercanvi` per a l'intercanvi temporal de documents, sense accés a informació interna ni d'administració. |
| Neus Bages | Externs | Usuari extern | Igual que Pere Espinalt: accés únicament a `comu/intercanvi`, de manera temporal i controlada. |

## 2. Resum de perfils d'usuari identificats

| Perfil | Persones assignades |
|---|---|
| **Usuari estàndard** | Aina Ciurans, Rut Tornil, Dídac Gassó, Estel Birosta, Aina Zuriguel, Roser Alberch, Guillem Adella, Alícia Monclús, Carles Molins, Eulàlia Galcera |
| **Responsable de departament** | Laia Macias (Administració), Lluïsa Richart (Suport tècnic), Meritxell Reglat (Producció musical) |
| **Administrador del sistema** | Talia Costas, Alex Soriano (Informàtica) |
| **Usuari extern** | Pere Espinalt, Neus Bages |

### 1.1. Reflexió

Quines diferències observes entre un **treballador**, un **departament** i una **funció o responsabilitat**?

---

---

---

Hi ha persones que, pel seu càrrec o funció, necessiten accessos diferents dels altres membres del seu departament?

☐ Sí  
☐ No

Posa'n algun exemple:

---

---

---

# 2. Recursos de l'empresa

Analitza l'estructura d'informació de MusicCloud.

Classifica alguns dels recursos següents segons la seva finalitat.

|Recurs|Qui creus que l'hauria d'utilitzar?|Per a què?|
|---|---|---|
|`/empresa/comu/intercanvi`|||
|`/empresa/comu/comunicats`|||
|`/empresa/departaments/administracio/compartida`|||
|`/empresa/departaments/administracio/gestio_departament`|||
|`/empresa/projectes/campanya_estiu`|||
|`/empresa/administracio_sistema/backups`|||

---

# 3. Qui ha de poder fer què?

Per a cada situació, indica quin nivell d'accés consideres adequat.

Utilitza:

- **NA** → sense accés
    
- **L** → lectura
    
- **L/E** → lectura i escriptura
    
- **ADM** → administració
    

No busquis encara una solució tècnica. Pensa només en les necessitats de l'empresa.

|Situació|Accés proposat|Justificació|
|---|---|---|
|Dídac accedeix a la carpeta compartida d'Administració|||
|Laia accedeix a la gestió del departament d'Administració|||
|Pere, treballador extern, accedeix als comunicats interns|||
|Talia accedeix als backups del sistema|||
|Un membre de Producció musical accedeix a la carpeta d'Administració|||
|Un participant de `campanya_estiu` accedeix als fitxers del projecte|||

---

# 4. Primer problema: com assignem els permisos?

Imagina que MusicCloud té només quatre treballadors:

- Anna
    
- Biel
    
- Carla
    
- David
    

Tots quatre treballen al mateix departament i necessiten accedir a la mateixa carpeta.

Una possible solució seria configurar:

```text
Anna  → lectura/escriptura
Biel  → lectura/escriptura
Carla → lectura/escriptura
David → lectura/escriptura
```

### 4.1.

Què passaria si l'empresa tingués **100 treballadors** amb el mateix tipus d'accés?

---

---

### 4.2.

Què passaria cada vegada que s'incorporés una persona nova?

---

---

### 4.3.

Què passaria quan una persona canviés de departament?

---

---

### 4.4.

Proposa una manera de gestionar aquestes persones conjuntament.

No cal que coneguis encara el nom tècnic de la solució.

---

---

---

---

# 5. Canvis a MusicCloud

Ara es produeixen aquests tres canvis:

### Cas A

Dídac deixa Administració i passa a Producció musical.

Quins accessos hauria de perdre?

---

Quins accessos hauria d'obtenir?

---

---

### Cas B

S'incorpora una nova treballadora al departament d'Administració.

Quins accessos caldria configurar?

---

---

---

### Cas C

Pere Espinalt deixa de col·laborar amb MusicCloud.

Què hauríem de fer amb els seus accessos?

---

---

---

# 6. Busquem una solució millor

Suposa ara que podem crear conjunts de persones que comparteixen unes mateixes necessitats d'accés.

Per exemple:

```text
Administració
    ├── Dídac
    ├── Laia
    └── Roser
```

I podem donar permisos directament al conjunt:

```text
Administració → carpeta_administracio → L/E
```

### 6.1.

Quin avantatge té aquesta solució respecte a donar permisos persona per persona?

---

---

### 6.2.

Si Dídac passa d'Administració a Producció musical, què caldria modificar?

---

---

### 6.3.

Com anomenaries aquests conjunts de persones?

---

---

# 7. Primera proposta per a MusicCloud

A partir de l'organització de l'empresa, proposa els primers conjunts de persones que crearies.

**No cal trobar encara la solució definitiva.**

|Nom proposat|Qui hi pertanyeria?|Per què existeix aquest conjunt?|
|---|---|---|
||||
||||
||||
||||
||||

---

# 8. Cas que complica el model

Laia treballa al departament d'Administració, però també és la responsable del departament.

És suficient que pertanyi només al conjunt `Administració`?

☐ Sí  
☐ No

Per què?

---

---

Quina possible solució proposes?

---

---

---

# 9. Un altre cas

Diverses persones de departaments diferents participen temporalment en el projecte:

```text
Campanya Estiu
```

Creus que hauríem de canviar-les de departament?

☐ Sí  
☐ No

Si no, com podríem donar-los accés als recursos del projecte?

---

---

---

# 10. Conclusions

Completa les frases amb les teves paraules.

### Usuari

Un usuari representa:

---

### Recurs

Un recurs és:

---

### Permís

Un permís determina:

---

### Grup

Un grup serveix per:

---

---

# 11. Regla de mínim privilegi

Analitza aquesta afirmació:

> Un usuari només hauria de tenir els permisos estrictament necessaris per realitzar la seva feina.

Explica amb les teves paraules què significa.

---

---

Posa un exemple relacionat amb MusicCloud.

---

---

---

# 12. Pregunta final

Imagina que demà MusicCloud passa de 14 treballadors a 500.

Quina de les dues estratègies consideres més adequada?

☐ Assignar permisos individualment a cada usuari.

☐ Organitzar els usuaris segons les seves necessitats i assignar permisos a aquests conjunts.

Justifica la resposta.

---

---

---

Jo **no faria obligatori que acabessin tota la fitxa abans d'explicar res**. La utilitzaria de manera sincronitzada amb la classe:

**0–40 min:** apartats 1–3 → analitzen MusicCloud i els accessos.  
**40–65 min:** apartats 4–5 → apareix el problema de gestionar permisos individualment.  
**65–85 min:** explicació curta de **usuari, grup, recurs, permís i mínim privilegi**.  
**85–110 min:** apartats 6–9 → apliquen immediatament el concepte de grup.  
**110–120 min:** apartats 10–12 → revisió i tancament.

Hi ha una decisió pedagògica important: a l'apartat 4 **no utilitzo la paraula “grup” fins que l'alumnat ha intentat resoldre el problema**. Això encaixa molt millor amb el cicle que vols seguir: primer tenen el problema, després apareix la necessitat i només aleshores introdueixes el concepte teòric.
