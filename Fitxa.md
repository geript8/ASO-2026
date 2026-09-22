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

| Persona | Departament | Funció / responsabilitat | Perfil | Necessita privilegis especials? Per què? |
|---|---|---|---|---|
| Aina Ciurans | Direcció | Usuari estàndard de Direcció | Direcció (cas especial) | Sí. Direcció té accés L/E gairebé a tots els recursos de l'empresa (comuns, propis i interdepartamentals), ja que supervisa el conjunt de l'organització. |
| Rut Tornil | Direcció | Usuari estàndard de Direcció | Direcció (cas especial) | Sí, pel mateix motiu que Aina Ciurans: Direcció necessita visió i control globals sobre la resta de departaments. |
| Dídac Gassó | Administració | Usuari estàndard | Usuari estàndard | No. Accedeix als recursos propis del departament (`compartida`, `documentacio_interna`) i als comuns de l'empresa, sense permisos addicionals. |
| Laia Macias | Administració | Cap de departament | Responsable de departament | Sí. Com a responsable, és l'única persona amb accés de lectura/escriptura a `gestio_departament` (carpeta restringida al cap). |
| Estel Birosta | Suport tècnic | Usuari estàndard | Usuari estàndard | Possiblement sí, de forma puntual. Suport tècnic pot rebre accés temporal (ATP) a `usuaris`, `logs`, `configuracions` i `inventari` per resoldre incidències concretes, sempre justificat i registrat. |
| Aina Zuriguel | Suport tècnic | Usuari estàndard | Usuari estàndard | Igual que Estel Birosta: accés ATP puntual per gestionar incidències, a més dels recursos habituals del departament. |
| Lluïsa Richart | Suport tècnic | Cap de departament | Responsable de departament | Sí. Com a responsable, té accés exclusiu de lectura/escriptura a `gestio_departament` i `scripts` del seu departament. |
| Roser Alberch | Producció musical | Usuari estàndard | Usuari estàndard | No. Treballa amb els recursos propis del departament (`compartida`, `artistes`, `cataleg`) i els comuns, sense privilegis especials. |
| Guillem Adella | Producció musical | Usuari estàndard | Usuari estàndard | No. Mateixes necessitats que la resta d'usuaris estàndard del departament. |
| Meritxell Reglat | Producció musical | Cap de departament | Responsable de departament | Sí. Accés restringit de lectura/escriptura a `gestio_departament`, a més de coordinar el contingut amb Suport tècnic (accés ATP d'aquest a `cataleg`). |
| Alícia Monclús | Producció musical | Usuari estàndard | Usuari estàndard | No. Necessitats bàsiques d'usuari del departament. |
| Carles Molins | Producció musical | Usuari estàndard | Usuari estàndard | No. Necessitats bàsiques d'usuari del departament. |
| Eulàlia Galcera | Producció musical | Usuari estàndard | Usuari estàndard | No. Necessitats bàsiques d'usuari del departament. |
| Talia Costas | Informàtica | Cap de departament / Administrador del sistema | Administrador del sistema | Sí, i de nivell alt. A més de l'accés `R: L/E` a `gestio_departament`, el departament d'Informàtica té permisos ADM sobre `administracio_sistema` (backups, logs, configuracions) i accés ADM tècnica a les carpetes personals dels usuaris. |
| Alex Soriano | Informàtica | Administrador del sistema | Administrador del sistema | Sí. Com a membre d'Informàtica, necessita permisos ADM per crear/modificar usuaris, gestionar grups, configurar serveis i revisar logs i backups. |
| Pere Espinalt | Externs | Usuari extern | Usuari extern | Sí, però limitats. Només ha d'accedir a `comu/intercanvi` per a l'intercanvi temporal de documents, sense accés a informació interna ni d'administració. |
| Neus Bages | Externs | Usuari extern | Usuari extern | Igual que Pere Espinalt: accés únicament a `comu/intercanvi`, de manera temporal i controlada. |
### 1.1. Reflexió

Quines diferències observes entre un **treballador**, un **departament** i una **funció o responsabilitat**?

Un **treballador** és una persona concreta de l'empresa (per exemple, Laia Macias). Un **departament** és el grup o àrea organitzativa a la qual pertany aquest treballador (per exemple, Administració). I la **funció o responsabilitat** és el rol concret que exerceix dins d'aquest departament (per exemple, ser cap de departament o usuari estàndard). Un mateix departament pot tenir diversos treballadors, però no tots exerceixen la mateixa funció: mentre la majoria són usuaris estàndard, n'hi ha un que assumeix la responsabilitat de cap. És precisament aquesta funció, i no el departament en si, la que determina quins privilegis d'accés necessita cada persona.

---

Hi ha persones que, pel seu càrrec o funció, necessiten accessos diferents dels altres membres del seu departament?

☑ Sí  
☐ No

Posa'n algun exemple:

- **Laia Macias** (Administració): a diferència de Dídac Gassó, com a cap de departament té accés exclusiu de lectura/escriptura a `gestio_departament`, una carpeta a la qual la resta del departament no pot accedir.
- **Talia Costas** i **Alex Soriano** (Informàtica): per la seva funció d'administradors del sistema, tenen permisos ADM sobre `administracio_sistema` (backups, logs, configuracions) i accés tècnic a les carpetes personals dels usuaris, uns privilegis que cap altre departament té.
- **Estel Birosta** i **Aina Zuriguel** (Suport tècnic): poden rebre accés temporal (ATP) a recursos com `logs` o `inventari` quan resolen una incidència concreta, un accés que no tenen de manera permanent ni la resta d'usuaris estàndard.

---

# 2. Recursos de l'empresa

Analitza l'estructura d'informació de MusicCloud.

Classifica alguns dels recursos següents segons la seva finalitat.

|Recurs|Qui creus que l'hauria d'utilitzar?|Per a què?|
|---|---|---|
|`/empresa/comu/intercanvi`|Tots els departaments i externs|Enviar i rebre documents amb gent de fora l'empresa|
|`/empresa/comu/comunicats`|Direcció (escriu) i la resta (llegeix)|Publicar avisos o comunicats per a tota l'empresa|
|`/empresa/departaments/administracio/compartida`|Treballadors d'Administració|Guardar documents habituals del departament|
|`/empresa/departaments/administracio/gestio_departament`|Només la cap d'Administració (Laia Macias)|Gestionar informació restringida del departament|
|`/empresa/projectes/campanya_estiu`|Només les persones del projecte|Treballar junts en la campanya d'estiu|
|`/empresa/administracio_sistema/backups`|Departament d'Informàtica|Guardar còpies de seguretat del sistema|

# 3. Qui ha de poder fer què?

Per a cada situació, indica quin nivell d'accés consideres adequat.

|Situació|Accés proposat|Justificació|
|---|---|---|
|Dídac accedeix a la carpeta compartida d'Administració|L/E|És del departament, hi treballa cada dia|
|Laia accedeix a la gestió del departament d'Administració|L/E|És la cap, gestiona el departament|
|Pere, treballador extern, accedeix als comunicats interns|NA|És extern, no ha de veure info interna|
|Talia accedeix als backups del sistema|ADM|És d'Informàtica, manté el sistema|
|Un membre de Producció musical accedeix a la carpeta d'Administració|NA|No és el seu departament|
|Un participant de `campanya_estiu` accedeix als fitxers del projecte|L/E|Hi treballa directament al projecte|

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

**Seria una feina molt pesada. Hauríem de configurar el permís un per un, 100 vegades, i és fàcil equivocar-se:**

---

---

### 4.2.

Què passaria cada vegada que s'incorporés una persona nova?

**Cada cop que entri algú nou, tocaria tornar a repetir tot el procés manualment per aquella persona.**

---

---

### 4.3.

Què passaria quan una persona canviés de departament?

**Caldria anar a buscar-la entre tots els permisos i canviar-los un per un, amb risc d'oblidar-ne algun.**

---

---

### 4.4.

Proposa una manera de gestionar aquestes persones conjuntament.

No cal que coneguis encara el nom tècnic de la solució.

**Es podria crear un grup amb totes les persones que necessiten el mateix accés, i donar el permís al grup sencer en lloc de a cada persona per separat. Així, quan algú entra o marxa, només s'afegeix o es treu del grup.**
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

**Hauria de perdre: accés a `compartida` i `documentacio_interna` d'Administració.**
Quins accessos hauria d'obtenir?



---

**Hauria d'obtenir: accés a `compartida`, `artistes` i `cataleg` de Producció musical.**
---

### Cas B

S'incorpora una nova treballadora al departament d'Administració.

Quins accessos caldria configurar?

---

**Hauria de obtenir accés a `compartida` i `documentacio_interna` i als recursos comuns de l'empresa.**

---

---

### Cas C

Pere Espinalt deixa de col·laborar amb MusicCloud.

Què hauríem de fer amb els seus accessos?

---

**Treure-li tots els accessos, sobretot a `comu/intercanvi`, que era l'únic recurs que tenia.**

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

**Estalvia feina: en lloc de configurar el permís persona per persona, es configura una vegada per a tot el conjunt. Si algú entra o marxa, només cal afegir-lo o treure'l del conjunt.**

---

### 6.2.

Si Dídac passa d'Administració a Producció musical, què caldria modificar?

---

**Només caldria treure'l del conjunt Administració i afegir-lo al conjunt Producció musical. No cal tocar els permisos de les carpetes.**

---

### 6.3.

Com anomenaries aquests conjunts de persones?

---

**Grups (o grups d'usuaris).**

---

# 7. Primera proposta per a MusicCloud

|Nom proposat|Qui hi pertanyeria?|Per què existeix aquest conjunt?|
|---|---|---|
|Direcció|Aina Ciurans, Rut Tornil|Necessiten accés global a gairebé tota l'empresa|
|Administració|Dídac Gassó, Laia Macias|Comparteixen els recursos del seu departament|
|Suport tècnic|Estel Birosta, Aina Zuriguel, Lluïsa Richart|Comparteixen els recursos del seu departament|
|Producció musical|Roser Alberch, Guillem Adella, Meritxell Reglat, Alícia Monclús, Carles Molins, Eulàlia Galcera|Comparteixen els recursos del seu departament|
|Informàtica|Talia Costas, Alex Soriano|Necessiten permisos ADM per gestionar el sistema|

# 8. Cas que complica el model

Laia treballa al departament d'Administració, però també és la responsable del departament.

És suficient que pertanyi només al conjunt `Administració`?

☑ Sí  
☐ No

Per què?

Perquè amb aquest conjunt ja té accés a `compartida` i `documentacio_interna`, però li falta l'accés especial a `gestio_departament`, que només és seu.

Quina possible solució proposes?

Crear un segon conjunt, per exemple `Administració_cap`, només amb en Laia, i donar-li a aquest conjunt l'accés a `gestio_departament`. Així en Laia pertanyeria als dos conjunts alhora: `Administració` i `Administració_cap`.
# 9. Un altre cas

Diverses persones de departaments diferents participen temporalment en el projecte `Campanya Estiu`.

Creus que hauríem de canviar-les de departament?

☐ Sí  
☑ No

Si no, com podríem donar-los accés als recursos del projecte?
Crear un conjunt nou només per al projecte, per exemple `Campanya_Estiu`, i afegir-hi les persones que hi participen, sense treure-les del seu departament d'origen. Així cada persona pertanyeria a dos conjunts alhora: el seu departament i el projecte.
# 10. Conclusions

### Usuari
Un usuari representa: una persona que treballa a l'empresa i necessita accedir a recursos.

### Recurs
Un recurs és: una carpeta a on hi ha informació que es pot consultar o modificar.

### Permís
Un permís determina: què pot fer un usuari amb un recurs (llegir-lo, modificar-lo o no accedir-hi).

### Grup
Un grup serveix per: reunir persones amb les mateixes necessitats d'accés i gestionar-les totes juntes.

# 11. Regla de mínim privilegi

Explica amb les teves paraules què significa.

**Significa que a cada persona només se li han de donar els permisos que realment necessita per fer la seva feina, ni un de més. Si no li cal per treballar, no hi ha d'accedir.**

Posa un exemple relacionat amb MusicCloud.

**Un membre de Producció musical no necessita accedir a la carpeta d'Administració, així que no se li dona aquest permís, encara que treballi a la mateixa empresa.**

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
