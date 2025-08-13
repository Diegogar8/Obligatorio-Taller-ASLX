# Fundamentos de Ansible

1. **¿Qué es Ansible? Mencione dos actividades que se puedan hacer con Ansible.**  
   Ansible es una herramienta de automatización de TI que permite aprovisionar, configurar y orquestar sistemas mediante **playbooks declarativos** sobre SSH.  
   Actividades: (a) **Gestión de configuración** (instalar paquetes, editar configs, servicios), (b) **Despliegue de aplicaciones** y orquestación multi-servidor.

2. **¿Qué es un playbook de Ansible?**  
   Es un archivo YAML que describe **estados deseados** y **tareas** a ejecutar en hosts/grupos, reutilizando roles, variables, handlers y módulos.

3. **¿Qué información contiene un inventario de Ansible?**  
   Lista de **hosts** agrupados (por SO, rol, entorno), variables por host/grupo (p.ej. `ansible_host`, `ansible_user`) y jerarquía de grupos (children).

4. **Explique qué es un módulo de Ansible y dé un ejemplo.**  
   Un módulo es una **unidad de trabajo** reutilizable que implementa una acción (instalar paquete, gestionar servicio, editar archivo).  
   Ejemplo: `apt` (Ubuntu) para instalar paquetes; `yum`/`dnf` (RHEL/CentOS); `ufw` para firewall; `lineinfile` para editar líneas.

5. **¿Qué ventajas tiene Ansible sobre otros métodos de automatización?**  
   - **Agentless** (usa SSH, no requiere agente en el host).  
   - **Declarativo e idempotente** (aplica cambios solo si son necesarios).  
   - **YAML legible**, curva de aprendizaje moderada.  
   - **Escalable** por inventarios y reutilización de roles/vars.