# A-ProP
# A ProP (Analyze Peak Performance) - Infraestructura como Código (IaC)

**Autor:** Vicente Ortiz Lluch  
**Ciclo Formativo:** 2º C.F.G.S. Administración de Sistemas Informáticos en Red (ASIR)  
**Centro:** IES Conselleria (València)  

---

## 1. Descripción del Proyecto
**A ProP** es una plataforma tecnológica de *Edge Computing* e *Internet de las Cosas (IoT)* enfocada en el análisis biomecánico, prevención de lesiones y optimización del rendimiento en el baloncesto. Mediante una red local de sensores no invasivos (plantillas inteligentes, parche biomecánico en codo/tríceps y toalla de análisis), el sistema recopila e ingesta telemetría en tiempo real a pie de pista con latencia ultrabaja (<10 ms) y custodia 100% local de los datos en la Comunitat Valenciana.

---

## 2. Objetivo de la Infraestructura
Desplegar, configurar y mantener de forma automatizada, idempotente y segura un clúster *Edge* de ultra-bajo consumo (15 W TDP) capaz de operar *in-situ* sin dependencia de conexión a Internet ni nubes públicas foráneas, garantizando el cumplimiento estricto del **RGPD (Art. 9)**, el **Esquema Nacional de Seguridad (ENS)** y los principios de sostenibilidad **Green IT** ($PUE \le 1.25$).

---

## 3. Tecnologías Utilizadas
* **Virtualización:** Proxmox VE 8.x (arquitectura híbrida KVM + contenedores ligeros LXC).
* **Sistema Operativo:** Debian 12 Bookworm.
* **Automatización e IaC:** Ansible + Bash Shell Scripts + Ansible Vault (cifrado AES-256).
* **Ingesta y Base de Datos:** Broker MQTT (EMQX / Mosquitto) + PostgreSQL 16 con extensión TimescaleDB.
* **Servidor Web y Visualización:** Nginx (Proxy Inverso + TLS 1.3) + Grafana.
* **Seguridad Perimetral y VPN:** Firewall OPNsense (KVM), segmentación VLAN 802.1Q y VPN WireGuard.
* **Monitorización y Respaldo:** Prometheus + Node Exporter + Proxmox Backup Server (PBS) bajo estrategia 3-2-1.

---

## 4. Estructura del Repositorio

```text
aprop-infraestructura/
├── playbooks/              # Orquestación principal de tareas de despliegue
│   └── site.yml            # Playbook maestro que ejecuta todos los roles
├── roles/                  # Módulos reutilizables organizados por función
│   ├── seguridad/          # Bastionado SSH, usuarios, políticas ENS/RGPD
│   ├── monitorizacion/     # Despliegue de Prometheus, Node Exporter y métricas PUE
│   ├── servicios_web/      # Configuración de Nginx, TLS y paneles Grafana
│   └── firewall/           # Reglas de filtrado, segmentación VLAN y WireGuard
├── variables/              # Variables globales y secretos cifrados con Ansible Vault
├── plantillas/             # Archivos de configuración dinámicos en formato Jinja2 (.j2)
├── inventario/             # Definición de nodos, grupos e IPs por VLAN (inventory.ini)
├── documentacion/          # Memorias técnicas, diagramas de red y guías de despliegue
└── README.md               # Documentación principal del repositorio
