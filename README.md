# Kuidas kasutada CLI tööriista

Tööriista saab alla laadida siit:
```bash
# bash

curl -fsSL https://tasks.homelab.ee/<course>/<script_name> | bash -s <exersice>
```
```PowerShell
# PowerShell

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
- LinuxOS
 	- lesson-1
 	- lesson-2
  - lesson-3
   
- WinOS
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
