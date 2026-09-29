# Fitxa 2 — Organització del servei de directori de MusicCloud

## 1. Objectes que hem de gestionar

|Tipus d'objecte|Exemples a MusicCloud|
|---|---|
|Usuaris|Aina Ciurans, Laia Macias, Talia Costas, Pere Espinalt...|
|Grups|Direcció, Administració, Suport tècnic, Producció musical, Informàtica|
|Equips|Campanya_Estiu, Migració_Servidors|
|Servidors|Servidor de fitxers, servidor de backups|
|Comptes d'aplicacions o serveis|Compte del servei de correu, compte del servidor de la plataforma musical|

Hi afegiries algun altre tipus d'objecte?

Sí, també hi afegiria les carpetes o recursos compartits (com `comu`, `departaments`, `projectes`), ja que també s'han de gestionar dins del directori.

# 2. Organització mitjançant unitats organitzatives

|OU|Què contindrà?|Per què la crees?|
|---|---|---|
|Direccio|Aina Ciurans, Rut Tornil|Per gestionar-los amb polítiques pròpies, diferents de la resta|
|Administracio|Dídac Gassó, Laia Macias|Agrupa els usuaris d'aquest departament|
|SuportTecnic|Estel Birosta, Aina Zuriguel, Lluïsa Richart|Agrupa els usuaris d'aquest departament|
|ProduccioMusical|Roser Alberch, Guillem Adella, Meritxell Reglat, Alícia Monclús, Carles Molins, Eulàlia Galcera|Agrupa els usuaris d'aquest departament|
|Informatica|Talia Costas, Alex Soriano|Per aplicar-hi polítiques d'administrador diferents de la resta|

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

Respon breument.

### a) Per què no seria una bona idea guardar tots els usuaris, grups, equips i servidors al mateix nivell sense organitzar-los?

---

---

### b) Per què no hauríem d'utilitzar les OU per substituir els grups de permisos?

---

---

### c) Si MusicCloud passa de 14 a 500 treballadors, quina característica del disseny que has fet avui facilitarà més l'administració?

---

---

---

# Documentació final del sistema

A partir de les decisions preses durant la sessió, deixa definida la proposta que utilitzarem inicialment per a MusicCloud.

## Estructura d'unitats organitzatives

```text
MusicCloud
│
│
│
│
```

## Criteri utilitzat per organitzar els objectes

---

---

## Criteri utilitzat per diferenciar OU i grups
