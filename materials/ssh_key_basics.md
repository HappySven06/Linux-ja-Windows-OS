# SSH võtmete juhend

SSH (Secure Shell) võtmed on turvaline viis serveritele ligipääsemiseks ilma parooli sisestamata. See juhend selgitab, kuidas luua, salvestada ja kasutada SSH võtmeid nii Linux kui Windows keskkonnas.

## Mis on SSH võtmed?

SSH autentimine kasutab **avalik-privaatne võtme paar** (public-private key pair):

- **Avalik võti (public key)**: saate seda kellelegi jagada. See paigutatakse serverisse, millele soovite ligipääsu
- **Privaatne võti (private key)**: see on salajane! Hoitakse turvalises kohas teie arvutis. Kunagi ärge jagagi seda kellegagi

Kui loote SSH ühenduse, server kontrollib, kas teie privaatne võti vastab serveris olevale avalikule võtmele. Kui jah, siis olete autenditud.

**Miks kasutada SSH võtmeid?**
- Turvalisem kui paroolid
- Paremad võimalused ligipääsukontrolliks
- Automatiseerimiseks ideaalne (skriptid ja töökonnad)
- Ajapiiratud ligipääs on võimalik

---

## SSH võtmete loomine

**Võtme loomine (Linux ja Windows):**

```bash
ssh-keygen -t ed25519 -C "teie_email@näide.ee"
```

Vajutage **Enter** vaikekoha kasutamiseks, sisestage tugev paroolifraas ja kinnitage seda.

**Võtmete asukohad:**
- **Linux:** `~/.ssh/id_ed25519` (privaatne) ja `~/.ssh/id_ed25519.pub` (avalik)
- **Windows:** `C:\Users\YourUsername\.ssh\id_ed25519` (privaatne) ja `.pub` (avalik)

---

## SSH võtmete turvalisus ja säilitamine

### Õigete failide õigused

**Linux:** Seadke õiged õigused: `chmod 700 ~/.ssh && chmod 600 ~/.ssh/id_ed25519 && chmod 644 ~/.ssh/id_ed25519.pub`

**Windows:** Faile kaitsvad Windowsi õigused automaatselt.

### Paroolifraas

Paroolifraas krüpteerib teie privaatset võtit. Kui määrasite parooli, peate selle iga kord SSH võtit kasutades sisestama.

### Kus salvestada võtmeid

- **Linux**: `~/.ssh/` (tavaliselt `/home/kasutaja/.ssh/`)
- **Windows**: `C:\Users\YourUsername\.ssh\`

**Mida ärge tehke:**
- ❌ Kunagi ärge jagake oma privaatset võtit
- ❌ Kunagi ärge säilititage privaatset võtit avalikult saadaval koodihoidlas (GitHub, GitLab jne)
- ❌ Kunagi ärge saatke privaatset võtit e-postiga

---

## SSH võtmete kasutamine

**Lihtne ühendus (kõik platvormid):** `ssh user@server.ee`

**SSH seadistamisfail:** Looge `~/.ssh/config` (Linux) või `C:\Users\YourUsername\.ssh\config` (Windows):

```
Host server1
    HostName server.ee
    User kasutaja
    IdentityFile ~/.ssh/id_ed25519
    Port 22
```

**Märkus (Windows):** Kasutage `C:\Users\YourUsername\.ssh\id_ed25519` asemel `~/.ssh/id_ed25519`.

Nüüd: `ssh server1`

---

## Ajapiiratud SSH võtmete kasutamine

**See on oluline turvalisuse funktsioon!** Saate lisada oma SSH võtmeid SSH agendile ajaliselt piiratult. See tähendab, et teie võti töötab ainult määratud aja jooksul.

**Miks kasutada ajapiiratud võtmeid?**
- 🔐 Turvalisem – juurdepääs on ajaliselt piiratud
- 🔑 Paremad praktikad – iga seanss nõuab uut otsust
- ⏰ Automaatne – pole vaja käsitsi võtit eemaldada

### Linux/macOS – ajapiiratud võtmete kasutamine

```bash
eval $(ssh-agent -s)               # Käivita SSH agent
ssh-add -t 3600 ~/.ssh/id_ed25519  # Lisage võti 1 tunniks (3600 sekundit)
ssh-add -l                         # Vaata aktiivseid võtmeid
ssh-add -d ~/.ssh/id_ed25519       # Eemalda võti
```

**Ajaperioodide näited:** 30 min (`-t 1800`), 1h (`-t 3600`), 2h (`-t 7200`), 8h (`-t 28800`)

### Windows – SSH agendi kasutamine

Windows-i OpenSSH ei toeta ajapiiratud võtmeid (`ssh-add -t`). Agent käivitatakse tavaliselt automaatselt Windows 10+.

```powershell
Start-Service ssh-agent                           # Käivita SSH agent (vajadusel)
ssh-add C:\Users\YourUsername\.ssh\id_ed25519     # Lisage võti
ssh-add -l                                        # Vaata aktiivseid võtmeid
ssh-add -d C:\Users\YourUsername\.ssh\id_ed25519  # Eemalda võti
```

**Märkus:** Logige välja (`logoff`) või käivitage arvuti uuesti, et eemaldada võtmeid.

---

## SSH võtmete lisamine kaugserveritele

Nüüd peate oma **avalikku võtit** serverisse või teenusesse (näiteks GitHub, GitLab) lisama. Protsess on sama enamike platvormide puhul.

### Linux – ssh-copy-id (serverid)

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@server.ee
```

Sisestage serveri parool. Käsk kopeerib teie avalikku võtit automaatselt.

### Windows – käsitsi lisamine (serverid)

```powershell
Get-Content C:\Users\YourUsername\.ssh\id_ed25519.pub | clip  # Kopeerige avalik võti
```

Logige sisse serverisse parooli abil, seejärel serveris:

```bash
mkdir -p ~/.ssh
echo "TEIE_AVALIK_VÕTI" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
exit  # Väljuge
```

Nüüd ei küsita parooli, ainult paroolifraasi.

### GitHub – kiirseadistus (kõik platvormid)

1. Kopeerige avalik võti: `cat ~/.ssh/id_ed25519.pub` (Linux) või `Get-Content C:\Users\YourUsername\.ssh\id_ed25519.pub | clip` (Windows)
2. Minge https://github.com/settings/keys
3. Klõpsake "New SSH key" ja kleepige avalik võti
4. Testige: `ssh -T git@github.com`

---

## Turvalisuse näpunäited

**Head tava**
- Kasutada erinevaid võtmeid eri otstarvete jaoks.

**Mida mitte teha**
- Jagage privaatset võtit
- Säilitada võtit avalikudes kohtades.
- Kasutada parooliteta võtmeid kriitilistel süsteemidel.
- Ignoreerida paroolifraasi.

---

## Kasulikkad käsud

**Ühised käsud:**
- `ssh-keygen -t ed25519 -C "email@näide.ee"` – Looge võti
- `ssh user@server.ee` – SSH ühendus
- `ssh-add -l` – Näita aktiivseid võtmeid

**Linux:**
- `eval $(ssh-agent -s)` – Käivita SSH agent
- `ssh-add -t 3600 ~/.ssh/id_ed25519` – Lisage võti 1 tunniks
- `ssh-copy-id -i ~/.ssh/id_ed25519.pub user@server.ee` – Kopeerige avalik võti serverisse

**Windows:**
- `Start-Service ssh-agent` – Käivita SSH agent
- `ssh-add C:\Users\YourUsername\.ssh\id_ed25519` – Lisage võti
- `Get-Content C:\Users\YourUsername\.ssh\id_ed25519.pub | clip` – Kopeerige avalik võti
