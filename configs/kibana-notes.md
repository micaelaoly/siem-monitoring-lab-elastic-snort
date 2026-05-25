# Notas de configuración de Kibana

Kibana se configuró como interfaz principal de visualización y análisis dentro del entorno SIEM del laboratorio. Su función fue permitir la consulta y monitorización de los eventos almacenados en Elasticsearch, facilitando el análisis de alertas generadas por Snort desde una interfaz gráfica mucho más cómoda y visual.

Durante la configuración se realizaron diferentes comprobaciones para asegurar la correcta comunicación entre Kibana y Elasticsearch, verificando tanto la conectividad entre servicios como la correcta indexación de eventos recibidos desde Logstash.

Una vez finalizada la configuración inicial, se crearon distintos Data Views para poder trabajar con los índices generados por los eventos del IDS. Posteriormente se realizaron pruebas desde Discover para comprobar que las alertas relacionadas con tráfico ICMP, conexiones SSH y otros eventos detectados por Snort aparecían correctamente indexadas y accesibles desde Kibana.

Además, se aplicaron filtros y búsquedas básicas para clasificar eventos según el tipo de tráfico detectado, permitiendo identificar de forma mucho más rápida la actividad generada dentro del laboratorio. Esto permitió entender mejor cómo trabaja un entorno SIEM orientado a monitorización defensiva y análisis de eventos de seguridad.

La integración entre Kibana y el resto de componentes de Elastic Stack permitió centralizar toda la información generada por el IDS y visualizarla desde una única plataforma, simulando un flujo de trabajo similar al utilizado en entornos SOC reales.

# Las principales tareas realizadas fueron:

- Verificación del estado del clúster
- Configuración en modo single-node
- Creación de índices para eventos de Snort
- Comprobación de conectividad con Kibana y Logstash
- Validación de ingestión de eventos
