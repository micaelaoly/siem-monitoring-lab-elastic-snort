# Full Documentation - SIEM Monitoring Lab with Elastic Stack and Snort

# 1. Preparación del entorno

## 1.1 Actualización del sistema

Lo primero realizado fue actualizar completamente el sistema operativo para evitar posibles problemas de compatibilidad entre paquetes y asegurar que todas las herramientas utilizadas funcionasen sobre versiones recientes y estables.

Se ejecutaron los siguientes comandos:

```bash
sudo apt update
sudo apt upgrade -y
```

- `apt update` actualiza la lista de repositorios disponibles
- `apt upgrade -y` instala automáticamente las últimas versiones de los paquetes ya instalados

Este paso es importante antes de desplegar servicios como Elasticsearch, Kibana o Logstash, ya que muchos errores posteriores suelen venir de dependencias desactualizadas.

---

## 1.2 Instalación de dependencias

Para poder desplegar Elastic Stack correctamente fue necesario instalar Java y varias herramientas auxiliares relacionadas con descargas HTTPS y gestión de paquetes.

La instalación se realizó mediante:

```bash
sudo apt install apt-transport-https openjdk-17-jdk wget curl -y
```

Las herramientas instaladas tienen diferentes funciones dentro del laboratorio:

- `openjdk-17-jdk` proporciona el entorno Java requerido por Elasticsearch
- `wget` y `curl` permiten descargar paquetes y repositorios externos
- `apt-transport-https` habilita el uso de repositorios seguros mediante HTTPS

Una vez finalizada la instalación se comprobó que Java funcionase correctamente:

```bash
java -version
```

---

# 2. Instalación de Elasticsearch

## 2.1 Adición del repositorio oficial de Elastic

Como Elasticsearch no se encuentra incluido dentro de los repositorios estándar de Ubuntu, fue necesario añadir el repositorio oficial de Elastic para poder instalar la herramienta correctamente.

Primero se importó la clave GPG oficial del repositorio:

```bash
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elastic.gpg
```

Este paso permite verificar que los paquetes descargados pertenecen realmente al repositorio oficial y no han sido modificados.

Posteriormente se añadió el repositorio de Elastic:

```bash
echo "deb [signed-by=/usr/share/keyrings/elastic.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
```

Después se actualizó nuevamente la lista de paquetes:

```bash
sudo apt update
```

---

## 2.2 Instalación de Elasticsearch

Una vez añadido el repositorio, se instaló Elasticsearch:

```bash
sudo apt install elasticsearch -y
```

Finalizada la instalación, se habilitó el servicio para que arrancase automáticamente junto al sistema:

```bash
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
```

Para comprobar que el servicio funcionaba correctamente se verificó su estado:

```bash
sudo systemctl status elasticsearch
```

También se comprobó la conectividad local mediante:

```bash
curl localhost:9200
```

Si Elasticsearch está funcionando correctamente devuelve información relacionada con el nodo y la versión instalada.

---

# 3. Instalación de Kibana

## 3.1 Instalación del servicio

Kibana se instaló desde el mismo repositorio oficial de Elastic utilizando:

```bash
sudo apt install kibana -y
```

Posteriormente se habilitó e inició el servicio:

```bash
sudo systemctl enable kibana
sudo systemctl start kibana
```

---

## 3.2 Configuración de Kibana

El archivo principal de configuración se encuentra en:

```bash
/etc/kibana/kibana.yml
```

Se modificaron algunos parámetros básicos para permitir el acceso desde la red interna del laboratorio:

```yaml
server.host: "0.0.0.0"
elasticsearch.hosts: ["http://localhost:9200"]
```

Después de modificar la configuración, se reinició el servicio:

```bash
sudo systemctl restart kibana
```

Finalmente se accedió desde el navegador mediante:

```txt
http://192.168.56.10:5601
```

---

# 4. Instalación y configuración de Snort

## 4.1 Instalación de Snort

Snort se instaló en la máquina IDS del laboratorio mediante:

```bash
sudo apt install snort -y
```

Durante la instalación se configuró la red utilizada por el entorno virtualizado.

---

## 4.2 Configuración de reglas

Las reglas locales utilizadas se almacenaron dentro de:

```bash
/etc/snort/rules/local.rules
```

Se añadieron reglas simples para detectar tráfico ICMP y conexiones SSH:

```conf
alert icmp any any -> any any (msg:"ICMP Packet Detected"; sid:1000001; rev:1;)

alert tcp any any -> any 22 (msg:"SSH Connection Detected"; sid:1000002; rev:1;)
```

Estas reglas permitieron generar alertas fácilmente durante las pruebas desde la máquina Kali.

---

## 4.3 Ejecución de Snort

Para ejecutar Snort en modo IDS se utilizó:

```bash
sudo snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```

- `-A console` muestra alertas en consola
- `-q` elimina información innecesaria
- `-c` especifica el archivo de configuración
- `-i` indica la interfaz de red monitorizada

---

# 5. Instalación y configuración de Filebeat

## 5.1 Instalación de Filebeat

Filebeat se instaló en la máquina IDS para monitorizar los logs generados por Snort:

```bash
sudo apt install filebeat -y
```

---

## 5.2 Configuración de Filebeat

El archivo principal utilizado fue:

```bash
/etc/filebeat/filebeat.yml
```

Se configuró para leer las alertas de Snort:

```yaml
filebeat.inputs:
  - type: log
    enabled: true
    paths:
      - /var/log/snort/alert
```

Posteriormente se configuró la salida hacia Logstash:

```yaml
output.logstash:
  hosts: ["192.168.56.10:5044"]
```

Una vez finalizada la configuración se reinició el servicio:

```bash
sudo systemctl restart filebeat
sudo systemctl enable filebeat
```

---

# 6. Configuración de Logstash

## 6.1 Creación del pipeline

Se creó un pipeline básico para procesar eventos enviados desde Filebeat.

Archivo utilizado:

```bash
/etc/logstash/conf.d/snort.conf
```

Configuración:

```conf
input {
  beats {
    port => 5044
  }
}

filter {

  if "ICMP" in [message] {
    mutate {
      add_field => { "traffic_type" => "PING" }
    }
  }

  if "SSH" in [message] {
    mutate {
      add_field => { "traffic_type" => "SSH" }
    }
  }

}

output {
  elasticsearch {
    hosts => ["http://localhost:9200"]
    index => "snort-events"
  }
}
```

El objetivo de este filtro fue clasificar distintos tipos de tráfico para facilitar posteriormente las búsquedas y visualizaciones desde Kibana.

---

## 6.2 Inicio del servicio

```bash
sudo systemctl enable logstash
sudo systemctl start logstash
```

Comprobación:

```bash
sudo systemctl status logstash
```

---

# 7. Pruebas realizadas

Una vez configurado todo el entorno se realizaron pruebas desde la máquina Kali para generar tráfico y comprobar el flujo completo de eventos.

Pruebas realizadas:

- Ping ICMP
- Conexiones SSH
- Escaneo básico de red
- Generación de tráfico HTTP

El objetivo fue comprobar que:

1. Snort detectaba eventos
2. Filebeat recogía logs
3. Logstash procesaba eventos
4. Elasticsearch indexaba información
5. Kibana mostraba correctamente las alertas

---

# 8. Resultados obtenidos

El laboratorio permitió desplegar un entorno SIEM funcional capaz de centralizar y visualizar eventos de seguridad generados por Snort.

La integración entre Filebeat, Logstash, Elasticsearch y Kibana permitió entender de forma práctica cómo funciona el flujo completo de eventos dentro de un entorno SOC orientado a monitorización defensiva.

Además, se reforzaron conocimientos relacionados con:

- Linux
- Redes
- SIEM
- IDS
- Elastic Stack
- Gestión de logs
- Blue Team
- Monitorización de seguridad
- Procesamiento de eventos
