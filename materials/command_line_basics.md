# Käsurea põhitõed (Linux ja PowerShell)

## Kuidas käsud (commands) üldiselt töötavad

Käsk on juhis, mille kasutaja annab operatsioonisüsteemile käsurea (terminali) kaudu.  
Kui vajutad **Enter**, siis süsteem loeb käsu läbi ja teeb vastava tegevuse.

Üldine käsu kuju on:
```
käsk [valikud] [argumendid]
```

### 1. Käsk
Käsk on programm või sisseehitatud funktsioon, mida süsteem oskab käivitada.

Näited:
- Linuxis: `ls`, `cd`, `mkdir`
- PowerShellis: `Get-ChildItem`, `Set-Location`

---

### 2. Valikud (options / flags)
Valikud muudavad käsu käitumist.
- Linuxis algavad tavaliselt `-` või `--`
- PowerShellis algavad `-Nimi`

Näide Linuxis:
```
ls -l
```
Näitab faile detailsemas vaates.

---

### 3. Argumendid
Argumendid määravad, **millega** käsk töötab (fail, kaust, nimi jne).

Näide:
```
cd Documents
```
Liigub kausta `Documents`.

---

### 4. Käsu otsimine (PATH)
Kui kirjutad käsu, otsib süsteem seda:
- sisseehitatud käskude seast
- kaustadest, mis on määratud **PATH** keskkonnamuutujas

Kui käsku ei leita:
- Linux: `command not found`
- PowerShell: `The term '...' is not recognized`

#### Käsu lisamine PATH-i
Kui soovid lisada oma käsu, pead faili asukoha lisama PATH-i:

- **Linux** (ajutine, kehtib ainult praeguses terminalis):
```bash
export PATH="$PATH:/tee/minu/käsule"
```

- **Linux** (püsiv, lisa `.bashrc` või `.zshrc` faili):
```bash
echo 'export PATH="$PATH:/tee/minu/käsule"' >> ~/.bashrc
source ~/.bashrc
```

- **PowerShell** (ajutine, kehtib ainult praeguses sessioonis):
```powershell
$env:PATH += ";C:\tee\minu\käsule"
```

- **PowerShell** (püsiv, lisa `$PROFILE` faili):
```powershell
Add-Content $PROFILE '$env:PATH += ";C:\tee\minu\käsule"'
```

Nüüd saab oma käsu käivitada lihtsalt nime järgi, ilma kogu teed kirjutamata.

---

## Põhilised käsud: Linux vs PowerShell

| Tegevus                             | Linuxi käsk      | PowerShelli käsk               | Kirjeldus                              |
| ----------------------------------- | ---------------- | ------------------------------ | -------------------------------------- |
| Kausta sisu kuvamine                | `ls`             | `Get-ChildItem` (`ls`)         | Näitab kaustas olevaid faile ja kaustu |
| Kausta vahetamine                   | `cd`             | `Set-Location` (`cd`)          | Liigub teise kausta                    |
| Praeguse kausta näitamine           | `pwd`            | `Get-Location`                 | Kuvab hetke asukoha                    |
| Uue kausta loomine                  | `mkdir`          | `New-Item -ItemType Directory` | Loob uue kausta                        |
| Tühja faili loomine                 | `touch file.txt` | `New-Item file.txt`            | Loob uue faili                         |
| Faili sisu vaatamine                | `cat file.txt`   | `Get-Content file.txt`         | Kuvab faili sisu                       |
| Faili kopeerimine                   | `cp a.txt b.txt` | `Copy-Item a.txt b.txt`        | Kopeerib faili                         |
| Faili liigutamine / ümbernimetamine | `mv a.txt b.txt` | `Move-Item a.txt b.txt`        | Liigutab või nimetab ümber             |
| Faili kustutamine                   | `rm file.txt`    | `Remove-Item file.txt`         | Kustutab faili                         |
| Kausta kustutamine                  | `rm -r kaust`    | `Remove-Item kaust -Recurse`   | Kustutab kausta koos sisuga            |
| Käsu abi                            | `man ls`         | `Get-Help Get-ChildItem`       | Näitab käsu juhendit                   |
| Ekraani puhastamine                 | `clear`          | `Clear-Host`                   | Puhastab terminali                     |
| Käskude ajalugu                     | `history`        | `Get-History`                  | Kuvab varasemad käsud                  |

> Märkus: PowerShellis on mitmed Linuxi käsud (`ls`, `cd`, `mkdir`) **aliased**, mis kutsuvad tegelikult PowerShelli cmdlet’e.

> **Näpunäide:** Kui soovid õppida käsude kohta rohkem, saad kasutada käsurealt abi:  
> - Linuxis: `man <käsk>` (näiteks `man ls`) või `<käsk> --help`  
> - PowerShellis: `Get-Help <käsk>` (näiteks `Get-Help Get-ChildItem`)
>   
> See kuvab käsu süvendi, valikud ja näited.

---

## Olulised erinevused Linuxi ja PowerShelli vahel

- **Linux** töötab peamiselt **tekstiga**
- **PowerShell** töötab **objektidega**

Näide:
- Linuxis on `ls` väljund tavaline tekst
- PowerShellis on `Get-ChildItem` väljund objektid, mida saab edasi töödelda ja filtreerida

See teeb PowerShelli väga võimsaks automatiseerimisel ja skriptimisel.

---

## Kokkuvõte

- Käsk = programm + valikud + argumendid
- Linuxi käsud on tavaliselt lühikesed ja lihtsad
- PowerShelli käsud on pikemad, kuid loogilisemad ja objektipõhised
- Mõlemad on olulised süsteemihalduse ja arenduse jaoks
