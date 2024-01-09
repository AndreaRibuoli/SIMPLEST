# SIMPLEST
L'esempio più semplice


In questo repository sono presenti due soli file rilevanti ai fini 
dell'utilizzo tramite **PASERIE/INSTALL**:

* il file *GUIDANCE.TXT*
* il file *QCLSRC/BUILD.CLLE*

L'utilità `PASERIE/INSTALL` identifica il repository mediante il nome
del proprietario del repository (come registrato su GitHub: `GitHub repository owner`) e il nome del repository stesso (`Repository`):

```
                   PASERIE Installer       V1R0M8 (INSTALL)                  
                                                                             
Type choices, press Enter.                                                   
                                                                             
GitHub repository owner  . . . .                                             
Repository . . . . . . . . . . .                 Character value             
GitHub personal access token . .                                             
                                                                             
Target library . . . . . . . . .   *REPOSITORY   Character value, *REPOSITORY
Target release . . . . . . . . .   *CURRENT      Character value, *CURRENT...
``` 

Il default per il `GitHub personal access token` è il valore speciale **\*GETPAT** che ricerca localmente il **P**ersonal **A**ccess **T**oken chiamando una exit funtion di cui può essere estratto il sorgente CL e adattato alle esigenze. Il programma di default si basa sulla DATA AREA `PASERIE/GITTOKEN`.

### GUIDANCE.TXT

Questo file contiene una lista di sorgenti: in questo caso la lista si limita a specificare il file `QCLSRC/BUILD.CLLE` che verrà creato come
`QTEMP/QCLSRC(BUILD)`

---
```
1234567890          1234567890
          1234567890          12345678901234567890123456789012345678901234567890
```

```
QCLSRC    BUILD     CLLE      Il più semplice uso di PASERIE
```
--- 

### QCLSRC/BUILD.CLLE

Questo è il file che verrà compilato in QTEMP e messo in esecuzione.
Tale fase seguirà il download di tutti i sorgenti elencati in `GUIDANCE.TXT`.
Il progettista può quindi fare affidamento sulla presenza in QTEMP di tutti 
i prerequisiti alla build della propria utilità.

---
```
PGM
CRTLIB LIB(SIMPLEST)
MONMSG MSGID(CPF0000)
ENDPGM
```
---

### Funzionalità addizionali

In realtà, all'atto della invocazione del programma BUILD, vengono passati dal programma di utilità 3 valori addizionali che possono essere impostati
al momento della sottomissione del programma `PASERIE/INSTALL`
e quindi convenientemente gestiti dalla BUILD:

```
PGM PARM(&DEVOPT_P &TGTRLS_P &TGTLIB_P)
```

```
Target library . . . . . . . . . TGTLIB         *REPOSITORY  
Target release . . . . . . . . . TGTRLS         *CURRENT     
Development option . . . . . . . DEVOPT         N  
```          

La `Target library`, qualora omessa, viene ricevuta dalla CL BUILD con il valore speciale `*PACKAGEN` (anzichè `*REPOSITORY` per omogenità con la utility `PASERIE/INSTALLOC` che sostituisce il valore speciale presente nel command `*LOCAL_PATH` sempre con `*PAKCAGEN`).

È quindi buona prassi, qualora si sviluppi lo script BUILD.CLLE a mano, 
prevedere la gestione di una libreria di installazione diversa dal nome del repository (default) e una release diversa dalla corrente.

Come vedremo lo sviluppo coerente con queste concenzioni è automatizzato dalla utilità `PASERIE/LIBCLONE`.