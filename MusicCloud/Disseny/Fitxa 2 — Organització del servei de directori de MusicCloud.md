# Fitxa 2 — Organització del servei de directori de MusicCloud

# 1. Objectes que hem de gestionar

Indica quins tipus d'objecte consideres que ha de contenir el servei de directori.

| Tipus d'objecte | Exemples a MusicCloud |
|---|---|
| Usuaris | Aina Ciurans, Laia Macias, Talia Costas, Pere Espinalt... |
| Grups | Direcció, Administració, Suport tècnic, Producció musical, Informàtica |
| Equips (ordinadors) | PC-DIRECCIO01, PC-ADMIN01, PC-SUPORT01, PC-PRODUCCIO01, PC-INFO01 |
| Servidors | Servidor de fitxers, servidor de backups |
| Comptes d'aplicacions o serveis | Compte del servei de correu (compte de servei que envia i rep correu), compte de servei que utilitza la plataforma musical per accedir a la base de dades i al servidor de fitxers on hi ha el catàleg |

Hi afegiries algun altre tipus d'objecte?

Sí, també hi afegiria les carpetes o recursos compartits (com `comu`, `departaments`, `projectes`), ja que també s'han de gestionar dins del directori.

# 2. Organització mitjançant unitats organitzatives

| OU | Què contindrà? | Per què la crees? |
|---|---|---|
| Direccio | Aina Ciurans, Rut Tornil | Per aplicar-hi GPO i polítiques pròpies, diferents de la resta (per exemple, polítiques de seguretat més estrictes perquè treballen amb informació sensible de tota l'empresa) |
| Administracio | Dídac Gassó, Laia Macias | Per aplicar-hi les GPO específiques del departament (per exemple, mapatge automàtic de les unitats de xarxa d'Administració i restriccions d'instal·lació de programari) i poder-ne delegar l'administració de comptes (restabliment de contrasenyes) a Suport tècnic |
| SuportTecnic | Estel Birosta, Aina Zuriguel, Lluïsa Richart | Per delegar-hi permisos d'administració limitats sobre les altres OU (restablir contrasenyes, desbloquejar comptes) i aplicar-hi GPO adaptades a les seves eines de treball |
| ProduccioMusical | Roser Alberch, Guillem Adella, Meritxell Reglat, Alícia Monclús, Carles Molins, Eulàlia Galcera | Per aplicar-hi GPO adaptades al seu entorn de treball (per exemple, accés a programari de producció musical i unitats de xarxa del catàleg) i diferenciar-ne la configuració de la resta |
| Informatica | Talia Costas, Alex Soriano | Per aplicar-hi polítiques d'administrador diferents de la resta (contrasenyes més robustes, accés a eines d'administració) i ser l'OU a qui es delega l'administració del domini |

## 2.1. Organització dels usuaris

```text
MusicCloud
│
├── Direccio
│   ├── Aina Ciurans
│   └── Rut Tornil
│
├── Administracio
│   ├── Laia Macias
│   └── Dídac Gassó
│
├── SuportTecnic
│   ├── Lluïsa Richart
│   ├── Estel Birosta
│   └── Aina Zuriguel
│
├── ProduccioMusical
│   ├── Meritxell Reglat
│   ├── Roser Alberch
│   ├── Guillem Adella
│   ├── Alícia Monclús
│   ├── Carles Molins
│   └── Eulàlia Galcera
│
├── Informatica
│   ├── Talia Costas
│   └── Alex Soriano
│
└── Externs
    ├── Pere Espinalt
    └── Neus Bages
```
```

# 3. OU o grup?

|Necessitat|OU|Grup|
|---|:-:|:-:|
|Organitzar els treballadors d'Administració|☑|☐|
|Donar accés a la carpeta d'Administració|☐|☑|
|Organitzar els ordinadors clients|☑|☐|
|Identificar les persones que participen en Campanya Estiu|☐|☑|
|Organitzar els servidors|☑|☐|
|Donar privilegis als administradors del sistema|☐|☑|
|Organitzar els comptes utilitzats per aplicacions|☑|☐|

### Explica amb les teves paraules la diferència principal entre una OU i un grup.

**OU:**

Serveix per organitzar i estructurar els objectes (per exemple, per departament), i per aplicar-hi polítiques de manera automàtica.

**Grup:**

Serveix per donar permisos o accessos concrets a un conjunt de persones, encara que siguin de departaments diferents.

# 4. Un mateix usuari: ubicació i pertinença

**En quina OU ubicaries el seu compte?**

A l'OU `Administracio`, perquè és el seu departament de treball habitual.

**A quins grups podria pertànyer?**

Al grup `Administracio` i al grup `Campanya_Estiu`.

### Per què no és contradictori que estigui en una OU però pertanyi a diversos grups?

Perquè cada usuari només pot estar en **una** OU (indica on està ubicat dins l'estructura), però pot pertànyer a **diversos** grups alhora (indiquen a quins recursos té accés).

# 5. Servei de directori

Explica breument què entens per **servei de directori**.

És un sistema que centralitza la informació dels usuaris, grups i recursos d'una empresa, i controla qui hi pot accedir.

Quin problema resol a MusicCloud?

Evita haver de gestionar els usuaris i permisos un per un a cada equip o recurs per separat, i permet fer-ho tot des d'un sol lloc.

# 6. LDAP

**LDAP és:**

Un protocol per accedir i consultar informació d'un servei de directori.

**LDAP no és:**

Un programa o un producte concret; és només un estàndard que altres sistemes utilitzen.

Indica si les afirmacions són certes o falses.

|Afirmació|C|F|
|---|:-:|:-:|
|LDAP és sinònim d'Active Directory|☐|☑|
|LDAP permet accedir i consultar informació d'un directori|☑|☐|
|OpenLDAP és una implementació d'un servei de directori|☑|☐|
|Active Directory utilitza LDAP, entre altres tecnologies|☑|☐|

# 7. DIT de MusicCloud

```text
MusicCloud
│
├── Usuaris
│   ├── Direccio
│   ├── Administracio
│   ├── SuportTecnic
│   ├── ProduccioMusical
│   ├── Informatica
│   └── Externs
│
├── Grups
│   ├── Direccio
│   ├── Administracio
│   ├── SuportTecnic
│   ├── ProduccioMusical
│   ├── Informatica
│   └── CampanyaEstiu
│
├── Equips
│   ├── PC_Direccio
│   ├── PC_Administracio
│   └── PC_Informatica
│
├── Servidors
│   ├── ServidorFitxers
│   └── ServidorBackups
│
└── ComptesServei
    ├── ServeiCorreu
    └── ServeiPlataforma
```
# 8. Justificació del disseny

### Decisió 1

Separar els usuaris en subdivisions per departament (Direccio, Administracio, SuportTecnic...).

**Justificació:**

Així cada departament té els seus usuaris ben organitzats i es poden aplicar polítiques diferents a cada un sense afectar la resta.

### Decisió 2

Crear un grup específic `CampanyaEstiu` fora de l'estructura de departaments.

**Justificació:**

Les persones que hi participen són de departaments diferents, així que un grup a part permet donar-los accés al projecte sense haver de canviar-les de departament.

# 9. Comprovació final

### a) Per què no seria una bona idea guardar tots els usuaris, grups, equips i servidors al mateix nivell sense organitzar-los?

Seria un caos trobar res, amb tot barrejat sense cap ordre.

### b) Per què no hauríem d'utilitzar les OU per substituir els grups de permisos?

Perquè les OU serveixen per aplicar polítiques i organitzar objectes, no per controlar qui accedeix a quins recursos.

### c) Si MusicCloud passa de 14 a 500 treballadors, quina característica del disseny que has fet avui facilitarà més l'administració?

La combinació d'**OU per departament** i **grups per als permisos**. Cada eina fa una feina diferent:

- **OU:** permeten aplicar les **GPO** a tot un departament d'un sol cop (mapatge d'unitats de xarxa, restriccions, polítiques de contrasenyes) i **delegar l'administració** d'una OU concreta a una persona o equip (per exemple, que Suport tècnic pugui restablir contrasenyes només a una OU). Un treballador nou només cal col·locar-lo a l'OU corresponent i ja rep la configuració del seu departament automàticament.
- **Grups:** els permisos sobre els recursos (`compartida`, `gestio_departament`, etc.) no es donen a cada usuari ni mitjançant les OU, sinó als grups. Quan arriba un treballador, només cal afegir-lo al grup del seu departament i ja té els accessos que li toquen.

Així, amb 500 treballadors no cal configurar cada usuari un per un: l'**OU** s'encarrega de les polítiques i la delegació, i els **grups** s'encarreguen dels permisos.

# Documentació final del sistema

## Estructura d'unitats organitzatives

```text
MusicCloud
│
├── Direccio
├── Administracio
├── SuportTecnic
├── ProduccioMusical
├── Informatica
└── Externs
```

## Modificacions respecte al disseny inicial (punt 7)

L'estructura final difereix de la que vaig plantejar al punt 7. Els canvis i la seva motivació són aquests:

- **[Canvi 1, per exemple: s'ha afegit l'OU `Externs`]:** els usuaris externs (Pere Espinalt i Neus Bages) tenen unes necessitats molt diferents de la resta: només han d'accedir a `comu/intercanvi`. Tenir-los en una OU pròpia permet aplicar-hi GPO molt restrictives i delegar-ne la gestió de forma separada.
- **[Canvi 2, per exemple: s'han eliminat les OU de projecte, com `CampanyaEstiu`]:** un projecte no és una unitat d'administració, ja que agrupa persones de departaments diferents. Els permisos d'un projecte es gestionen millor amb un **grup**, i les persones continuen a l'OU del seu departament.
- **[Canvi 3, per exemple: s'han simplificat les OU a un únic nivell per departament]:** amb només 14 treballadors, crear subnivells afegia complexitat sense cap benefici. Una OU per departament és suficient per aplicar GPO i delegar l'administració.

## Criteri utilitzat per organitzar els objectes

S'ha organitzat cada usuari dins l'OU del seu departament, ja que és el lloc on treballa habitualment i on se li apliquen les polítiques (GPO) del dia a dia. A més, cada OU permet delegar-ne l'administració (per exemple, que Suport tècnic pugui restablir contrasenyes) sense donar permisos sobre tot el directori.

## Criteri utilitzat per diferenciar OU i grups

Les OU s'utilitzen per ubicar i organitzar els usuaris segons el seu departament, per aplicar-hi GPO i per delegar-ne l'administració. Els grups s'utilitzen per donar permisos d'accés a recursos concrets, encara que els membres siguin de departaments diferents (com en el cas del projecte `CampanyaEstiu`). Els permisos mai es donen directament a les OU.