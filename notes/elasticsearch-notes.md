# Notas de configuración de Elasticsearch

Elasticsearch se desplegó como componente principal de almacenamiento e indexación dentro de la infraestructura SIEM del laboratorio. Su función fue recibir, almacenar y organizar todos los eventos procesados por Logstash para posteriormente permitir su consulta desde Kibana.

La instalación se realizó sobre Ubuntu Server utilizando una configuración básica en modo single-node, suficiente para el entorno virtualizado utilizado durante las pruebas. Tras el despliegue inicial, se verificó el correcto funcionamiento del servicio comprobando el estado del clúster y la disponibilidad del puerto utilizado por Elasticsearch.

Posteriormente se realizaron diferentes pruebas de conectividad desde Kibana y Logstash para validar que los eventos generados por Snort podían almacenarse correctamente dentro de los índices creados automáticamente por el pipeline de Logstash.

Una vez configurado el flujo completo de eventos, Elasticsearch comenzó a indexar las alertas generadas por el IDS, permitiendo realizar búsquedas, filtrados y análisis desde Kibana de forma centralizada. Gracias a esto fue posible comprobar cómo se almacenaban eventos relacionados con tráfico ICMP, conexiones SSH y diferentes pruebas realizadas desde la máquina Kali del laboratorio.

El uso de Elasticsearch dentro del proyecto permitió entender mejor cómo funciona el almacenamiento y gestión de logs dentro de un entorno SIEM moderno, además de reforzar conocimientos relacionados con indexación de eventos, análisis de logs y monitorización de seguridad en infraestructuras Linux.

# Las principales tareas realizadas fueron:

- Verificación del estado del clúster
- Configuración en modo single-node
- Creación de índices para eventos de Snort
- Comprobación de conectividad con Kibana y Logstash
- Validación de ingestión de eventos
