
</p>
**Es la versión oficial de SEEKER con las plantillas modificadas al idioma español.**
El concepto detrás de Seeker es simple, ¿por qué no alojar una página falsa que solicite su ubicación como muchos sitios web basados en la ubicación? Seeker crea un sitio web falso que solicita Permiso de ubicación y, si el objetivo lo permite, podemos obtener:

* Longitud.
* Latitud.
* Precisión.
* Altitud: no siempre disponible.
* Dirección: solo disponible si el usuario se está moviendo.
* Velocidad: solo disponible si el usuario se está moviendo. 

Junto con la información de ubicación, también obtenemos **Información del dispositivo** sin ningún permiso:

* Identificación única con huellas dactilares de lienzo
* Modelo de dispositivo: no siempre disponible
* Sistema operativo
* Plataforma
* Número de núcleos de CPU: resultados aproximados
* Cantidad de RAM - Resultados aproximados
* Resolución de la pantalla
* Información de la GPU
* Nombre y versión del navegador
* Dirección IP pública
* Dirección IP local
* Puerto local

**Reconocimiento automático de direcciones IP** se realiza después de que se recibe la información anterior.

**Esta herramienta es una prueba de concepto y es solo para fines educativos, Seeker muestra qué datos puede recopilar un sitio web malicioso sobre usted y sus dispositivos y por qué no debe hacer clic en enlaces aleatorios y permitir permisos críticos como Ubicación, etc.**

## ¿En qué se diferencia de la ubicación geográfica IP?

* Otras herramientas y servicios ofrecen geolocalización de IP que NO es precisa en absoluto y no proporciona la ubicación del objetivo, sino la ubicación aproximada del ISP.

* Seeker usa la API HTML y obtiene el permiso de ubicación y luego toma la longitud y la latitud usando el hardware GPS que está presente en el dispositivo, por lo que el buscador funciona mejor con los teléfonos inteligentes, si el hardware del GPS no está presente, como en una computadora portátil, el buscador recurre a la geolocalización IP o buscará coordenadas en caché.  

* Generalmente, si un usuario acepta el permiso de ubicación, la precisión de la información recibida tiene una **precisión de aproximadamente 30 metros **

* La precisión depende de múltiples factores que usted puede controlar o no, tales como:
   * Dispositivo: no funcionará en computadoras portátiles o teléfonos que tengan el GPS roto
   * Navegador: algunos navegadores bloquean los javascripts
   * Calibración de GPS: si el GPS no está calibrado, es posible que obtenga resultados inexactos y esto es muy común.

## Plantillas

Plantillas disponibles : 

* Cerca de usted.
* Google Drive.
* WhatsApp.
* Telegrama.

## Probado en:

* Kali Linux
* BlackArch Linux
* Ubuntu
* Kali Nethunter
* Termux
* Parrot OS

## Instalación

### Kali Linux / Ubuntu / Parrot OS

```bash
git clone https://github.com/thewhiteh4t/seeker.git
cd seeker/
apt update
apt install python3 python3-pip php
pip3 install requests
```

### BlackArch Linux

```bash
pacman -S seeker
```

### Termux

```bash
git clone https://github.com/thewhiteh4t/seeker.git
cd seeker/
pkg update
pkg install python php
pip3 install requests
```
### Docker

```bash
docker pull thewhiteh4t/seeker
```

## Uso

```bash
python3 seeker.py -h

usage: seeker.py [-h] [-s SUBDOMAIN]

argumentos opcionales:
  -h, --help            show this help message and exit
  -k KML, --kml         Provide KML Filename ( Optional )
  -p PORT, --port       Port for Web Server [ Default : 8080 ]
  -t TUNNEL, --tunnel   Specify Tunnel Mode [ Available : manual ]

##################
# Ejemplos de uso #
##################

# Paso 1: en la primera terminal
$ python3 seeker.py -t manual

# Paso 2: En unaa segunda terminal, inicie un servicio de túnel como ngrok
$ ./ngrok http 8080

###########
# Opciones #
###########

# Archivo KML de salida para Google Earth
$ python3 seeker.py -t manual -k <filename>

# Usar puerto personalizado
$ python3 seeker.py -t manual -p 1337
$ ./ngrok http 1337

################
# Uso de Docker #
################

# Paso 1
$ docker network create ngroknet

# Paso 2
$ docker run --rm -it --net ngroknet --name seeker thewhiteh4t/seeker

# Paso 3
$ docker run --rm -it --net ngroknet --name ngrok wernight/ngrok ngrok http seeker:8080
```
