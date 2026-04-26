# Git põhitõed

## Mis on Git?

Git on versioonihaldussüsteem, mis võimaldab:
- salvestada oma töö ajalugu
- taastada varasemaid versioone
- jagada faile teistega

---

## Mis on GitHub?

GitHub on veebiteenus, kus hoitakse Git koodihoidlat (repo).

Link: https://github.com

Seal saad:
- oma projekti üles laadida
- teistega koostööd teha
- oma tööd jagada

---

## Olulised mõisted

- **repo (repository)** – projektikaust Gitiga
- **commit** – salvestatud muudatus
- **push** – muudatuste üleslaadimine GitHubi
- **clone** – projekti allalaadimine

---

## Põhikäsud

### 1. Repo allalaadimine

```bash
git clone <repo_link>
```

---

### 2. Failide lisamine

```bash
# Lisa kõik failid
git add .

# Lisa üks kindel fail
git add file.txt
```

### 3. Commit (salvestamine)

```bash
# Lihtne
git commit -m "message"

# Salvestamine koos lisa infoga
git commit -m "title message" -m "detailed message"
```

### 4. Muudatuste üleslaadimine

```bash
git push
```

### Tavaline töövoog

```bash
git add .
git commit -m "message"
git push
```

---

## Hea commit sõnum

Commite tehes on tähtis, et sinu sõnum on selge ja konkreetne. 

Hea commit sõnum koosneb kahest osast:
- Pealkiri - Lühike kokkuvõtte commitist.
- Sisu - Detailsem ülevaade tehtud muudatustest.

Head tavad commiti kirjutades:
- Kasuta inglise keelt
- Vormista enda pealkiri niimoodi, et see sobiks sellisesse lausese `I shall <sinu pealkiri>`

**Näited:**
```bash
# Halb
git commit -m "update"

# Hea
git commit -m "Add backup script" -m "Created a backup.sh script to backup a system."
```

---

## Täiendavad teemad: .gitignore

Kui sinu repo kasvab, võid märgata, et mõned failid ei peaks Git-i jälgitavate failide hulka minema. Selleks kasutatakse `.gitignore` faili.

### Mis on .gitignore?

`.gitignore` fail ütleb Git-ile, milliseid faile ja kaustu ignoreerida – neid ei lisata commitesse ega laadita GitHubi.

### Näited IT administraatori jaoks

Tüüpilised failid, mida IT admins tahavad ignoreerida:

```
# Privaatsed võtmed ja sertifikaadid
*.key
*.pem
id_rsa

# Paroolid ja konfiguratsiooni failid koos salajaste andmetega
.env
secrets.conf
passwords.txt
config.local

# Logifailid
*.log
logs/

# Ajutised ja varufailid
*.tmp
*.bak
temp/

# Operatsioonisüsteem spetsiifilised failid
.DS_Store
Thumbs.db
```

### Kuidas rakendada

1. Loo repositooriumi juurkaustasse fail nimega `.gitignore`
2. Lisa sellesse failid/kaustad, mida soovid ignoreerida
3. Salvesta ja commit

```bash
git add .gitignore
git commit -m "Add .gitignore" -m "Exclude sensitive files and temporary files from version control"
git push
```

**Nõuanne:** Kui oled juba lisanud faili, mida tahad ignoreerida, pead selle kõigepealt eemaldama:

```bash
git rm --cached secrets.conf
git commit -m "Remove secrets.conf from tracking"
```