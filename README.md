# Kursuse info

Siit leiad kõik kursusega seotud dokumendid ja materjalid.

## Kursuse materjalid

- [Klassi kodukord](class_docs/class_conduct.md)
- [Hindamisjuhend](class_docs/grading_guide.md)
---
- [Käsurea põhitõed (Linux ja PowerShell)](materials/command_line_basics.md)
- [TPTLab kasutus juhend](materials/tptlab_usage_guide.md)
---
- [06.04 Tunni ülesanne – Samba failiserver](materials/06.04_lesson_task.md)
- [13.04 Tunni ülesanne – Rsync ja cron](materials/13.04_lesson_task.md)

---

# Kuidas kasutada CLI tööriista

Tööriista saab alla laadida siit:
```bash
# bash

curl -fsSL https://tasks.homelab.ee/<course>/<script_name> | bash -s <exersice>
```
```PowerShell
# PowerShell

Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass

Invoke-WebRequest -Uri https://tasks.homelab.ee/<course>/<script> -OutFile install.ps1; .\install.ps1 <exersice>
```

Ülesandeid saab ainult VMs (virtuaalmasinas) jooksutada.

Olemas olevad kursused on:
- LinuxOS
- WinOS

Olemas olevad skriptid on:
- install
- install-simple
- uninstall

Olemas olevad ülesanded:
- **LinuxOS**
  - lesson-1
  - lesson-2
  - lesson-3
  - lesson-4
   
- **WinOS**
  - lesson-1
  - lesson-2 
  - lesson-3

## Tööriistale olemasolevad käsud
```bash
<program_name> start

<program_name> task start --id <task_id>
<program_name> task submit --id <task_id>

<program_name> task list
<program_name> task list --long

<program_name> task advice --id <task_id>

<program_name> finish
```
