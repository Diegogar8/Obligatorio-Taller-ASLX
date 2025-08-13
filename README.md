# Taller Servidores Linux — Obligatorio

Este repositorio contiene la solución completa al obligatorio del Taller Servidores Linux.  
Incluye inventario, playbooks, evidencias y respuestas teóricas.


> **Nota**: Ajustá las IPs y el usuario en `inventory.ini` según tu entorno. Probado con **CentOS Stream 9** y **Ubuntu 24.04 LTS**.

---

## Estructura

```
.
├── Documentos/                 # Evidencias y salidas de ejecución
│   ├── 01_inventario_y_ping.txt
│   ├── 02_ad_hoc_commands.txt
│   ├── 03_nfs_setup_run.txt
│   └── 04_hardening_run.txt
├── ansible_basics.md           # Respuestas teóricas
├── IAG_prompts.md              # Prompts de IA usados (requerido por consigna)
├── inventory.ini               # Inventario con grupos linux/ubuntu/centos/webserver
├── nfs_setup.yml               # Playbook NFS para CentOS
└── hardening.yml               # Playbook de hardening para Ubuntu
```

---

## Requisitos previos

- Control node con **Ansible 2.16+**.
- Acceso SSH por clave a los hosts.
- Usuario remoto (por defecto `ansible`) con permisos de sudo sin contraseña (o usá `--ask-become-pass`).

---

## Verificación de inventario

```bash
ansible-inventory -i inventory.ini --list
ansible all -i inventory.ini -m ping
```

---

## Ejecución de playbooks

### 1) NFS en CentOS (grupo `webserver` o `centos`)

```bash
ansible-playbook -i inventory.ini nfs_setup.yml --limit webserver --become
```

### 2) Hardening en Ubuntu (grupo `ubuntu`)

```bash
ansible-playbook -i inventory.ini hardening.yml --limit ubuntu --become
```

> **Handlers**:  
> - `nfs_setup.yml` recarga `/etc/exports` cuando cambia y asegura servicios activos.  
> - `hardening.yml` reinicia `sshd` si cambia su configuración y reinicia el sistema si hubo upgrades que lo requieran.

---

## Notas de implementación

- NFS exporta `/var/nfs_shared` con permisos 0777 y propietario `nobody:nobody` como exige la consigna.
- En Ubuntu, `ufw` por defecto **deniega entrantes**, permite `OpenSSH`, deshabilita login de root y por password, y habilita `fail2ban` para proteger SSH.
- Se colocan configs en rutas estándar:
  - SSH: `/etc/ssh/sshd_config.d/99-hardening.conf`
  - Fail2ban: `/etc/fail2ban/jail.d/sshd-hardening.local`

---

## Licencia

Uso académico.