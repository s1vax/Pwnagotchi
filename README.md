# >°-°< Pwnagotchi 

<p align="center">
<img width="400" height="400" alt="WhatsApp Image 2026-04-27 at 12 16 46" src="https://github.com/user-attachments/assets/7599c37a-0f94-436d-b2f4-92932b664243" />
</p>


## ⚖️ Legal Disclaimer
The creator of this repository is not responsible for any malicious or inappropriate use of the device described. It is strictly prohibited to interfere with other Wi-Fi networks without consent or adequate security measures.

<br>
<br>

### ✅ Safe environments and measures
You can target a personal network with the pwnagotchi attack as a proof of use, or simply put it in passive mode. The repository will explain in detail how to do this.

<br>
<br>

## 🛒 Things we need
- `Raspberry Pi Zero` or `Raspberry Pi Zero 2W`
- `Ups Hat Waveshare Raspberry Pi Zero (5v) + screws`
- `1000mah Li-po Battery`
- `2,13 inches Waveshare Hat Version Electronic Ink Display`
- A `PC` for configuration
- `Micro USB cable`
- `Raspberry Pi Zero Pins`
- `OTG Adapter Micro USB to USB` [optional]
- `WIFI Antenna` [with monitor configuration available] [optional]

<br>
<br>

## 🔎 Step by step

### 🛠️ Construction & Connections 
   - En primer lugar, soldaremos todos los pines de la Raspberry Pi Zero 2 W. Tener cuidado al soldar ya que los pines se consumen/derriten. Para ello, un metodo efectivo para soldar sin quemar todo en el proceso es el del siguiente video: https://www.youtube.com/watch?v=jYKzsLmMV6o
   - Una vez hecho eso, le conectaremos al UPS Hat la bateria de LiPo. Luego, mediante los tornillos que nos vienen incluidos en el paquete de Waveshare, colocamos esta placa de alimentacion por debajo de la Raspberry Pi. Sobre el UPS Hat, 6 pines de la Raspberry Pi (del lado corto y soldado) deben hacer contacto y presion sobre los 6 pines retraibles que el UPS tiene. Con ello, pasaremos a verificar la conexion y la alimentacion para comprobar si la Raspberry Pi se encendera sin problemas.

     ¿Como realizamos la verificacion?
   
   - Concluido con lo anterior, pasamos a colocar la pantalla de tinta electronica (el conector de 8 pines, debe estar del mismo lado que los puertos de conexion de la Raspberry Pi)


<br>
<br>

### 💻 Firmware
   - Several websites offer different versions of pwnagotchi. In this repository, we will use the firmware located in the #firmware folder.

<br>

     
   - Once the `.rar` file with extension `.img` has been downloaded from the #firmware folder, we need to prepare our Micro SD card in a Micro SD card holder to insert it into our PC and flash it with the file we downloaded.

   <br>
     
   - To flash the card, it is recommended to use the applications: `balenaEtcher` o `Raspberry Imager`. Depending on which flashing tool we select, we must:
     - For `balenaEtcher` (recomended):
       - Select the corresponding `.img` file
       - Select the storage location
       - Write the file
         
     - For `Raspberry Imager`:
       - Select the board (in this case, a `Raspberry Pi Zero 2 W`)
       - Select `Use custom` in the next tab, where you will locate your `.img` file
       - Select the storage location
       - Write the file
         
<br>

   - Una vez flasheada la Micro SD, al conectar nuevamente nuestra Micro SD card holder, nos debe de salir como `Boot` o `Bootloader` en el apartado de discos de nuestra computadora (o tambien, puede que al finalizar el flasheo, se abra una ventana de este nuevo "disco", aun conectado el holder). En dicha carpeta de disco, debemos de agregar un archivo llamado `config` con extension `.toml`, en definitiva, `config.toml`. Este archivo esta relacionado con la pantalla de tinta electronica del Pwnagotchi, es necesario para que esta funcione. 
   
      ***¿Como agregamos este archivo?***
     - Para ello, vamos a crear un archivo de texto comun (colocar un nombre cualquiera)
     - Luego, debemos configurar la visualizacion de archivos en nuestra carpeta de disco de Windows 11. Iremos a `View`, luego seleccionamos en ese menu desplegable a `Show`, y por ultimo a `File name extensions`
     - Con esta configuracion, veremos todas las extensiones de nuestros archivos en esa carpeta de disco
     - Entonces, lo que haremos es, seleccionar nuestro archivo de texto creado, darle click derecho y luego en `Rename`. Aqui seleccionamos todo, incluyendo la extension y colocamos: `config.toml`
     - Nos saldra un cartel de advertencia sobre que estamos cambiando el tipo de extension, le damos en `Ok`. Hasta aqui nuestro archivo adicional ya estara creado.
     - Como es un archivo nuevo, no tiene ninguna informacion, comando o contenido alguno en el. A continuacion vamos a agregarle el codigo siguiente:

```     
main.name = "pwnagotchi"
main.lang = "en"
main.whitelist = [
  "TuRedWifi"
]

ui.display.enabled = true
ui.display.type = "waveshare_3" # o "waveshare_4", "waveshare_213d", etc.
ui.display.color = "black"
```
<br>

   - En adicion al archivo anterior, vamos a modificar otros dos archivos: `config.txt` y `cmdline.txt`
     - Para `config.txt`, eliminamos su codigo existente, y lo reemplazamos por:
        - ```

        ```
          
     - Para `cmdline.txt`, eliminamos su codigo existente, y lo reemplazamos por:
       ```
       console=serial0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 fsck.repair=yes rootwait modules-load=dwc2,g_ether
       ```

 <br>

   - Colocamos la SD en nuestra Raspberry Pi
     
   <br>

   - Seguido a ello, para realizar la primera prueba de alimentacion, conectamos el cable Micro USB a la placa Raspberry en el puerto de `USB` (NO AL `PWR IN`), y a nuestra PC.

<br>
     
   - Si no hay errores, ya podran ver el firmware de Pwnagotchi funcionando (y su carita tierna pero feroz)

<br>
   
   - En el primer inicio (tanto si conectamos por el puerto `USB` como por el puerto `PWR IN`, de la placa) el firmware va a tardar un poco debido a que esta generando las claves de configuracion y demas. Dara un aviso de esto en la pantalla.

<br>

   - Luego de que se haya inicializado, cuando lo desconectemos, y volvamos a conectar, comenzara a correr normalmente y mas rapido en el inicio.

<br>

   - Por ultimo, pasaremos a convertir nuestro Pwnagotchi en un dispostivo portatil, haciendo funcionar el UPS Hat de Waveshare. Para ello, como ya verificamos la funcionalidad de la bateria, lo que haremos es conectarla a la placa UPS (si no la teniamos conectada), luego debemos colocar el interruptor en `ON`, y finalmente conectar, por medio de un cable USB C a USB, la placa UPS a nuestra PC. Cunado realicemos esto, se encendera un led rojo en la placa UPS, lo dejamos unos minutos y desconectamos.

<br>

   - Y listo ✅ Ya tendremos nuestro dispositivo de hacking Pwnagotchi listo!
   
<br>

***⚠️ NOTE:*** Si conectamos el cable Micro USB a la Raspberry en su puerto `PWR IN`, el firmware de Pwnagotchi comenzara a actuar sin control alguno, capturando handshakes y desautenticando dispositivos. Para no infligir ciberdelitos se debe proceder con una conexion y configuracion, segura y controlada.

<br>
<br>

### ⚙️ Configuration
Al inicio, cuando conectamos nuestro cable Micro USB a la Raspberry por el puerto `PWR IN`, con nuestro firmware cargado, como dijimos, este dispositivo empieza a actuar sin control.

Para ello, en esta seccion, vamos a configurarlo para realizar operaciones de pruebas controladas y seguras (aunque lo conectemos por este puerto de alimentacion)

<br>
<br>

### 🧩 Personalization and Options

<br>
<br>

### 📡 Upgrades
- ***Micro USB to USB OTG Adapter***: Este adaptador nos permitira que la Raspberry Pi pueda tener acceso a otros dispositivos que permitan expandir sus capacidades
- ***TP Link AC600 WIFI Antenna***: Junto al adaptador Micro USB OTG, podemos expandir el rango de ataque de nuestro dispositivo colocando una antena WIFI externa, siempre que tenga disponible la configuracion `Monitor`

<br>
<br>

### 🧊 3D Cases (📌 in progress)

<br>

### I hope you found this helpful and enjoyable. If so, leave a star ⭐ Best wishes and much success!
