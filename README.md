# SIEM Monitoring Lab with Elastic Stack and Snort

Laboratorio SOC/Blue Team basado en Elastic Stack, Kibana, Logstash, Filebeat y Snort para centralizar, procesar y visualizar alertas de seguridad generadas por un IDS.

---

# Descripción del proyecto

Este proyecto consiste en el despliegue de un entorno SIEM funcional en un laboratorio virtualizado orientado a monitorización de seguridad, análisis de eventos y detección de actividad sospechosa en red.

El laboratorio fue diseñado simulando un pequeño entorno SOC donde diferentes máquinas generan tráfico y eventos que posteriormente son detectados por Snort, procesados mediante Logstash y visualizados desde Kibana utilizando Elastic Stack. El objetivo principal fue comprender el flujo completo de eventos dentro de una arquitectura defensiva moderna, desde la generación de alertas por un IDS hasta su ingestión, clasificación y análisis centralizado dentro de un SIEM.

Durante el proyecto se trabajó con conceptos relacionados con Blue Team, monitorización de red, análisis de logs, segmentación de servicios y procesamiento de eventos de seguridad en tiempo real.

---

# Tecnologías utilizadas

- Ubuntu Server
- Kali Linux
- Elastic Stack
  - Elasticsearch
  - Kibana
  - Logstash
  - Filebeat
- Snort IDS
- Linux
- Redes TCP/IP
- VirtualBox

---

# Arquitectura del laboratorio

| Máquina | Función | IP |
|---|---|---|
| SIEM-ELK | Elasticsearch + Kibana + Logstash | 192.168.56.10 |
| IDS-SNORT | Snort + Filebeat | 192.168.56.20 |
| KALI | Generación de tráfico y pruebas | 192.168.56.30 |

---

# Flujo de eventos

1. Snort detecta tráfico potencialmente sospechoso o eventos definidos mediante reglas IDS
2. Las alertas generadas son almacenadas en logs locales dentro de la máquina IDS
3. Filebeat monitoriza continuamente dichos logs y reenvía los eventos hacia Logstash
4. Logstash procesa, filtra y clasifica los eventos según el tipo de tráfico detectado
5. Elasticsearch indexa la información para facilitar búsquedas y correlación de eventos
6. Kibana permite visualizar logs, aplicar filtros y analizar actividad de red desde una interfaz gráfica


---

# Implementación

## Configuración de red

Se configuró una red interna virtualizada para permitir la comunicación entre las diferentes máquinas del laboratorio.

### Capturas recomendadas

- Configuración IP
- Conectividad entre máquinas
- Esquema de red

---

## Instalación de Elasticsearch

Se desplegó Elasticsearch como motor principal de almacenamiento e indexación de eventos de seguridad.

### Capturas recomendadas

- Servicio funcionando
- curl localhost:9200
- Estado del clúster

---

## Instalación de Kibana

Kibana se configuró para conectarse a Elasticsearch y facilitar la visualización gráfica y análisis de eventos generados dentro del laboratorio.

### Capturas recomendadas

- Página principal de Kibana
- Discover
- Data Views

---

## Configuración de Filebeat

Filebeat se instaló en la máquina IDS para monitorizar continuamente los logs generados por Snort y enviarlos hacia Logstash para su procesamiento.

### Capturas recomendadas

- filebeat.yml
- Servicio activo
- Logs enviados correctamente

---

## Configuración de Logstash

Logstash se utilizó para procesar eventos y añadir campos personalizados según el tipo de tráfico detectado, permitiendo clasificar y organizar mejor la información almacenada.

### Capturas recomendadas

- Pipeline de Logstash
- Puerto 5044 escuchando
- Procesamiento de eventos

---

## Configuración de Snort

Snort se configuró como sistema IDS para detectar diferentes tipos de tráfico y generar alertas relacionadas con ICMP, SSH y otros eventos definidos mediante reglas personalizadas.

### Capturas recomendadas

- Reglas Snort
- Alertas generadas
- Logs del IDS

---

# Resultados obtenidos

El laboratorio permitió centralizar correctamente eventos de seguridad dentro de Elastic Stack y visualizar alertas desde Kibana mediante índices personalizados en Elasticsearch.

Además, se consiguió procesar y clasificar tráfico mediante filtros de Logstash, facilitando la detección de eventos relacionados con conexiones ICMP, accesos SSH y actividad sospechosa generada desde la máquina de pruebas.

La integración entre Snort, Filebeat, Logstash y Elasticsearch permitió simular un flujo realista de monitorización de seguridad orientado a entornos SOC y Blue Team.

---

# Conocimientos aplicados

- Monitorización de seguridad
- SIEM
- Blue Team
- IDS
- Gestión de logs
- Elastic Stack
- Redes
- Linux
- Análisis de eventos
- Seguridad defensiva

---

# Estructura del repositorio

```bash
siem-monitoring-lab-elastic-snort/
│
├── README.md
├── docs/
├── images/
├── configs/
└── notes/
```

---

# Autor

Proyecto desarrollado como laboratorio práctico de ciberseguridad orientado a tecnologías SIEM, monitorización defensiva, análisis de eventos y gestión centralizada de logs en entornos Linux.
