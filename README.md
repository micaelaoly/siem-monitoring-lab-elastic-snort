```text
███████╗██╗███████╗███╗   ███╗
██╔════╝██║██╔════╝████╗ ████║
███████╗██║█████╗  ██╔████╔██║
╚════██║██║██╔══╝  ██║╚██╔╝██║
███████║██║███████╗██║ ╚═╝ ██║
╚══════╝╚═╝╚══════╝╚═╝     ╚═╝

Elastic Stack · Snort IDS · SOC Monitoring · Blue Team
```

# SIEM Monitoring Lab con Elastic Stack y Snort

![Elastic Stack](https://img.shields.io/badge/Elastic%20Stack-SIEM-blue)
![Snort](https://img.shields.io/badge/Snort-IDS-red)
![Linux](https://img.shields.io/badge/Linux-Ubuntu-orange)
![Blue Team](https://img.shields.io/badge/Blue%20Team-Monitoring-green)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)

Laboratorio SIEM orientado a monitorización defensiva y análisis de eventos utilizando Elastic Stack junto con Snort como sistema IDS dentro de un entorno virtualizado sobre Linux.

---

> [!NOTE]
> Este proyecto fue desarrollado en un entorno completamente controlado con fines educativos y orientado principalmente a conceptos relacionados con SOC, monitorización defensiva y análisis de eventos de seguridad.

---

# Descripción del proyecto

Este laboratorio consiste en la implementación de una arquitectura SIEM utilizando tecnologías de Elastic Stack junto con Snort como sistema IDS para detectar y centralizar eventos de seguridad dentro de una red virtualizada.

El objetivo principal fue simular un pequeño entorno SOC donde diferentes máquinas generan tráfico y eventos que posteriormente son detectados, procesados y visualizados desde una plataforma centralizada. Para ello se trabajó con herramientas como Elasticsearch, Kibana, Logstash, Filebeat y Snort dentro de un entorno Linux.

Durante el desarrollo del proyecto se configuró un flujo completo de eventos de seguridad, permitiendo observar cómo una alerta generada por el IDS puede ser recogida, procesada, indexada y visualizada desde Kibana para facilitar tareas de monitorización y análisis defensivo.

Además de la parte relacionada con gestión de logs y tecnologías SIEM, el laboratorio permitió reforzar conocimientos relacionados con redes, Linux, análisis de eventos, configuración de servicios y fundamentos de Blue Team.

---

# Objetivos del laboratorio

- Desplegar una arquitectura SIEM funcional utilizando Elastic Stack
- Configurar Snort como sistema IDS
- Centralizar logs de seguridad
- Procesar eventos mediante Logstash
- Visualizar eventos desde Kibana
- Comprender el flujo completo de monitorización dentro de un SIEM
- Simular un entorno básico orientado a SOC y Blue Team
- Reforzar conocimientos relacionados con análisis de eventos y monitorización defensiva

---

# Tecnologías utilizadas

| Tecnología | Función |
|---|---|
| Elasticsearch | Almacenamiento e indexación de eventos |
| Kibana | Visualización y análisis de logs |
| Logstash | Procesamiento y filtrado de eventos |
| Filebeat | Recolección y envío de logs |
| Snort IDS | Detección de tráfico sospechoso |
| Ubuntu Server | Infraestructura del SIEM |
| Kali Linux | Generación de tráfico de pruebas |
| VirtualBox | Virtualización del laboratorio |
| Linux | Administración del entorno |

---

# Arquitectura del laboratorio

El laboratorio se compone de varias máquinas virtuales conectadas mediante una red interna virtualizada.

| Máquina | Función | Dirección IP |
|---|---|---|
| SIEM-ELK | Elasticsearch + Kibana + Logstash | 192.168.56.10 |
| IDS-SNORT | Snort + Filebeat | 192.168.56.20 |
| KALI | Generación de tráfico y pruebas | 192.168.56.30 |

Cada sistema cumple una función específica dentro del flujo de eventos del laboratorio.

La máquina IDS monitoriza tráfico y genera alertas mediante Snort. Posteriormente Filebeat recoge los logs generados y los envía hacia Logstash, donde son procesados antes de almacenarse dentro de Elasticsearch. Finalmente Kibana permite consultar y visualizar todos los eventos desde una interfaz gráfica centralizada.

---

# Flujo de eventos

El funcionamiento general del laboratorio sigue el siguiente flujo:

1. Kali Linux genera tráfico de prueba dentro de la red
2. Snort detecta eventos según las reglas configuradas
3. Filebeat monitoriza continuamente los logs del IDS
4. Los eventos son enviados hacia Logstash
5. Logstash procesa y clasifica la información
6. Elasticsearch indexa los eventos procesados
7. Kibana permite visualizar y analizar las alertas generadas

Gracias a esta arquitectura fue posible simular un flujo de monitorización similar al utilizado en entornos SOC reales.

---

# Capturas del laboratorio

## Configuración de red

![Configuración IP](images/1.conf-ip-siemelk.png)

---

## Elasticsearch funcionando

![Elastic funcionando](images/5.elastic-funcionando.png)

---

## Dashboard de Kibana

![Kibana](images/7.pagina-kibana.png)

---

## Alertas detectadas por Snort

![Snort](images/15.alertas-snort.png)

---

# Resultados obtenidos

El laboratorio permitió centralizar correctamente eventos de seguridad dentro de Elastic Stack y visualizar alertas desde Kibana mediante índices personalizados en Elasticsearch.

Además, se consiguió procesar y clasificar tráfico mediante Logstash, facilitando la detección de eventos relacionados con conexiones ICMP, accesos SSH y actividad sospechosa generada desde la máquina Kali Linux.

La integración entre Snort, Filebeat, Logstash y Elasticsearch permitió comprender mejor cómo funciona el flujo completo de eventos dentro de un entorno SIEM orientado a monitorización defensiva y análisis SOC.

---

# Skills 

- SIEM deployment
- IDS configuration
- Log analysis
- Event correlation
- Security monitoring
- Elastic Stack
- Linux administration
- Blue Team fundamentals
- Network monitoring
- Security event visualization


---

# Documentación completa

La documentación técnica detallada del laboratorio se encuentra en:

[Ver documentación completa](docs/full-documentation.md)

---

> [!TIP]
> Este laboratorio está orientado principalmente a monitorización defensiva y análisis de eventos desde una perspectiva SOC y Blue Team utilizando tecnologías ampliamente utilizadas en entornos SIEM reales.

---

# Autor

Proyecto desarrollado como laboratorio práctico de ciberseguridad orientado a tecnologías SIEM, monitorización defensiva, análisis de eventos y gestión centralizada de logs utilizando Elastic Stack y Snort IDS.
