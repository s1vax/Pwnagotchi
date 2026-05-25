# >°-°< Pwnagotchi 

<p align="center">
<img width="400" height="400" alt="WhatsApp Image 2026-04-27 at 12 16 46" src="https://github.com/user-attachments/assets/7599c37a-0f94-436d-b2f4-92932b664243" />
</p>


## ⚖️ Legal Disclaimer
The creator of this repository is not responsible for any malicious or inappropriate use of the device described. It is strictly prohibited to interfere with other Wi-Fi networks without consent or adequate security measures.

<br>
<br>

### ✅ Safe environments and measures
You can target a personal network with the pwnagotchi attack as a proof of use, or simply put it in passive mode (`manual mode`). The repository will explain in detail how to do this.

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
- `OTG Adapter Micro USB to USB A` [optional]
- `WIFI Antenna` [with monitor configuration available] [optional]

<br>
<br>

## ❓ ¿What is Pwnagotchi & How it works?
- `Pwnagotchi` is a virtual pet designed for cybersecurity and hardware hacking. Essentially, it's a deep reinforcement learning agent based on the A2C (Advantage Actor-Critic) architecture. Its primary function is to audit wireless networks by "eating" the handshakes and PMKIDs of WPA/WPA2 networks it encounters in its environment.

   Unlike traditional auditing tools where the user must manually configure attack parameters, Pwnagotchi learns from its radio frequency (RF) environment and dynamically adjusts its behavior to maximize the capture of       cryptographic material.
  
<br>

- ¿How it works?
To achieve its goal, Pwnagotchi combines low-power hardware (usually a Raspberry Pi Zero W or Zero 2 W) with a very powerful software stack:

  - ***The Engine (Bettercap)***: At the heart of its offensive and scanning capabilities is BetterCap. Pwnagotchi uses this tool's API to interact with the network interface in monitor mode, inject packets (such as for deauthentication attacks), and capture traffic.

  - ***The Brain (Artificial intelligence)***: This is where the A2C model comes in. Pwnagotchi constantly evaluates its environment and makes decisions about which channels to scan, how long to stay on each, and what kind of deauthentication packets to send to connected clients. If its decisions result in the successful capture of a handshake (its reward), the neural network adjusts its weights to favor that behavior in the future.

  - ***Personality (UI and States)***: Its mood reflects what's happening at the network and hardware levels. If it's capturing a lot of handshakes, it will be happy. If there's little traffic or it's not capturing any, it will get bored or sad. This interface is usually displayed on an e-ink screen, giving it that characteristic cyber Tamagotchi look.

<br>

- The life cycle of a Pwnagotchi
When you turn on your Pwnagotchi, it goes through different phases:

  - ***Recognition (Blind/Bored)***: Scan the channels looking for Access Points (APs) and active clients.
  
  - ***Asociación y Ataque***: Cuando encuentra un objetivo viable, puede esperar pasivamente a que un cliente se conecte, o forzar la reconexión enviando tramas de desautenticación para capturar el 4-way handshake.

  - ***Captura***: Al interceptar el handshake o PMKID, lo guarda en un archivo .pcap localmente. Este archivo es la "comida" que luego puedes extraer para intentar crackear la contraseña en otro equipo (usando herramientas como Hashcat).

  - ***Socialización***: Si un Pwnagotchi detecta a otro cerca (usando paquetes dot11 personalizados), pueden "hablar" entre ellos, compartir información sobre el entorno y modificar sus comportamientos mutuamente.

<br>
<br>

## 🔎 Step by step

### 🛠️ Construction & Connections 
   - En primer lugar, soldaremos todos los pines de la Raspberry Pi Zero 2 W. Tener cuidado al soldar ya que los pines se consumen/derriten. Para ello, un metodo efectivo para soldar sin quemar todo en el proceso es el del siguiente video: https://www.youtube.com/watch?v=jYKzsLmMV6o
   - Una vez hecho eso, le conectaremos al UPS Hat la bateria de LiPo. Luego, mediante los tornillos que nos vienen incluidos en el paquete de Waveshare, colocamos esta placa de alimentacion por debajo de la Raspberry Pi. Sobre el UPS Hat, 6 pines de la Raspberry Pi (del lado corto y soldado de la placa) deben hacer contacto y presion sobre los 6 pines retraibles que el UPS tiene.
   - Con ello montado, pasaremos a verificar la conexion y la alimentacion, para comprobar si la Raspberry Pi se encendera sin problemas.
   
      - ¿Como realizamos la verificacion?
      
        - Medir la tension de la bateria LiPo
          - Utilizando un multimetro, verificaremos la tension de la bateria LiPo de 3.7v.
          - Conectamos las puntas del multimetro en sus respectivos conectores del propio multimetro (cable negro en `COM`, y cable rojo en `V, Ω, Hz, °C, ...`).
          - Luego ponemos la llave selectora del multimetro en `V---` (voltaje o tension continua), y en el valor `6v`.
          - Y por ultimo medimos. Colocamos el `cable rojo` del multimetro en la parte `roja o positiva` de la bateria, y el `cable negro` del multimetro en la parte `negra o negativa` de la bateria.
        
        - Comprobar soldaduras de la Raspberry Pi Zero 2 W
        
        - Comprobar funcionamiento de la placa UPS Hat de Waveshare 
          - Conectar la bateria LiPo a la placa UPS (si no las teniamos conectadas).
          - Luego, debemos colocar el interruptor en `ON` de dicha placa.
          - Por medio de un cable `USB C` a `USB A`, conectaremos la placa UPS a nuestra PC. Cuando realicemos esto, se deberia encender un led rojo en la placa UPS, a la cual deberemos de dejar prendida unos segundos, y la             desconectamos. 
          - Finalmente, bajamos el interruptor a `OFF` y prendemos nuevamente nuestra placa UPS Hat con el interruptor en `ON` (esto con el fin de hacer un reinicio), y ya deberia ser capaz de brindar alimentacion por su              cuenta.
   
   - Concluido con lo anterior, pasamos a colocar la pantalla de tinta electronica. Para comprobar si la hemos colocado correctamente, el conector de 8 pines de esta pantalla, debe estar en paralelo o del mismo                 lado, que los puertos de conexion de la Raspberry Pi (los cuales son: `USB`, `Mini HDMI` y `PWR IN`).

<br>
<br>

### 💻 Firmware
   - Several websites offer different versions of pwnagotchi. In this repository, we will use the firmware located in the #firmware folder.

<br>

   - Once the `.rar` file with extension `.img` has been downloaded from the #firmware folder, we need to prepare our Micro SD card in a Micro SD card holder to insert it into our PC and flash it with the file we downloaded.
   <br>
     
   - To flash the card, it is recommended to use the applications: `balenaEtcher` o `Raspberry Imager`. Depending on which flashing tool we select, we must:
     - For `balenaEtcher` (recomended):
       - Select the corresponding `.img` file.
       - Select the storage location.
       - Write the file.
         
     - For `Raspberry Imager`:
       - Select the board (in this case, a `Raspberry Pi Zero 2 W`).
       - Select `Use custom` in the next tab, where you will locate your `.img` file.
       - Select the storage location.
       - Write the file.
<br>

   - Una vez flasheada la Micro SD, puede que al finalizar el flasheo, se abra una nueva ventana de carpeta de "disco" llamada `Boot` o `Bootloader`, en nuestra computadora. Si vemos que esto no ocurre, desconectamos y conectamos nuevamente nuestra Micro SD card holder, y ahi nos deberia de salir esa ventana emergente, o simplemente lo podemos buscar en el apartado de discos de nuestra computadora con el nombre anterior. En dicha carpeta de disco, debemos de agregar un archivo llamado `config` con extension `.toml`, en definitiva, `config.toml`. Este archivo esta relacionado con la pantalla de tinta electronica del Pwnagotchi, es necesario para que esta funcione. 
   
      - ¿Como agregamos este archivo?
        - Para ello, vamos a crear un archivo de texto comun (colocar un nombre cualquiera).
        - Luego, debemos configurar la visualizacion de archivos en nuestra carpeta de disco de Windows 11. Iremos a `View`, luego seleccionamos en ese menu desplegable a `Show`, y por ultimo a `File name extensions`.
        - Con esta configuracion, veremos todas las extensiones de nuestros archivos en esa carpeta de disco.
        - Entonces, lo que haremos es, seleccionar nuestro archivo de texto creado, darle click derecho y luego en `Rename`. Aqui seleccionamos todo, incluyendo la extension y colocamos: `config.toml`.
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

   - En adicion al archivo anterior, vamos a modificar otros dos archivos: : `config.txt` y `cmdline.txt`. Lo haremos editandolos y abriendolos con el bloc de notas (dandole click derecho al archivo a editar, y seleccionando `Open with Notepad`).
   
     - Para `config.txt`, eliminamos su codigo existente, y lo reemplazamos por:
     
          ```
           # For more options and information see
           # http://rpf.io/configtxt
           # Some settings may impact device functionality. See link above for details

           # uncomment if you get no picture on HDMI for a default "safe" mode
           #hdmi_safe=1

           # uncomment this if your display has a black border of unused pixels visible
           # and your display can output without overscan
           #disable_overscan=1

           # uncomment the following to adjust overscan. Use positive numbers if console
           # goes off screen, and negative if there is too much border
           #overscan_left=16
           #overscan_right=16
           #overscan_top=16
           #overscan_bottom=16

           # uncomment to force a console size. By default it will be display's size minus
           # overscan.
           #framebuffer_width=1280
           #framebuffer_height=720

           # uncomment if hdmi display is not detected and composite is being output
           #hdmi_force_hotplug=1

           # uncomment to force a specific HDMI mode (this will force VGA)
           #hdmi_group=1
           #hdmi_mode=1
 
           # uncomment to force a HDMI mode rather than DVI. This can make audio work in
           # DMT (computer monitor) modes
           #hdmi_drive=2

           # uncomment to increase signal to HDMI, if you have interference, blanking, or
           # no display
           #config_hdmi_boost=4

           # uncomment for composite PAL
           #sdtv_mode=2

           #uncomment to overclock the arm. 700 MHz is the default.
           #arm_freq=800

           # Uncomment some or all of these to enable the optional hardware interfaces
           #dtparam=i2c_arm=on
           #dtparam=i2s=on
           #dtparam=spi=on

           # Uncomment this to enable infrared communication.
           #dtoverlay=gpio-ir,gpio_pin=17
           #dtoverlay=gpio-ir-tx,gpio_pin=18

           # Additional overlays and parameters are documented /boot/overlays/README

           # Enable audio (loads snd_bcm2835)
           dtparam=audio=on

           [pi4]
           # Enable DRM VC4 V3D driver on top of the dispmanx display stack
           dtoverlay=vc4-fkms-v3d
           max_framebuffers=2

           [all]
           #dtoverlay=vc4-fkms-v3d
           dtoverlay=dwc2
           dtoverlay=spi1-3cs
           dtoverlay=pwm-2chan,pin=12,func=4,pin2=13,func2=4
           dtparam=spi=on
           dtparam=i2c_arm=on
           dtparam=i2c1=on
           gpu_mem=16

        ```
          
     - Para `cmdline.txt`, eliminamos su codigo existente, y lo reemplazamos por:
     
       ```
       console=serial0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 fsck.repair=yes rootwait modules-load=dwc2,g_ether
       ```

 <br>

   - Guardamos los cambios en el bloc de notas (en cada archivo).

 <br>

   - Desconectamos el SD holder de nuestra PC y colocamos la SD en nuestra Raspberry Pi.
     
   <br>

   - Seguido a ello, para realizar la primera prueba de funcionamiento, conectamos el cable Micro USB a la placa Raspberry en su puerto de `USB` (y no al puerto `PWR IN`), y el `USB A` del cable a nuestra PC. En el firmware de Pwnagotchi, el puerto `USB` de la Raspberry Pi se encuentra en un `safe mode` o mejor dicho, en un `manual mode`, esto significa que alimentando la placa por este puerto con el firmware cargado, no se ejecutara de forma automatica los procesos de desautenticacion y handshakes. Por lo que podremos corroborar si se ejecuta de forma correcta el programa, sin la necesidad de que automaticamente ataque a las redes cercanas.
   
<br>
     
   - Si no hay errores, ya podran ver el firmware de Pwnagotchi funcionando (y su carita tierna pero feroz).

<br>
   
   - En el primer inicio (tanto si conectamos por el puerto `USB` como por el puerto `PWR IN`, de la placa) el firmware va a tardar un poco debido a que esta generando las claves de configuracion y demas. Dara un aviso de esto en la pantalla. 
   
   ⚠️ ***NOTE:*** Durante esta parte de inicializacion no se debe de desconectar el dispositivo para evitar errores.

<br>

   - Luego de que se haya inicializado, cuando lo desconectemos, y volvamos a conectar, comenzara a correr normalmente y mas rapido en el inicio.

<br>

   - Por ultimo, haremos que nuestro Pwnagotchi sea portatil mediante el uso del UPS Hat de Waveshare. Simplemente ponemos el interruptor de esta placa en `ON`.


<br>

   - Y listo ✅ Ya tendremos nuestro dispositivo de hacking Pwnagotchi funcionando!
   
<br>

***⚠️ NOTE:*** Si conectamos el cable Micro USB a la Raspberry en su puerto `PWR IN`, o alimentamos la placa mediante la placa UPS Hat, el firmware de Pwnagotchi comenzara a actuar sin control alguno, es decir, entrara en su `auto mode` por defecto, capturando handshakes y desautenticando dispositivos. Para no infligir leyes, se debe proceder con una conexion y configuracion, segura y controlada.

<br>
<br>

### ⚙️ Configuration
Hasta este punto, en los pasos anteriores, cuando conectemos nuestro cable Micro USB a la Raspberry por el puerto `PWR IN` (o simplemente brindandole alimentacion a la Raspberry Pi con el UPS Hat), y con nuestro firmware cargado, el Pwnagotchi empezara a actuar sin control, resultando un dispositivo peligroso para las redes WIFI cercanas, y ademas detectable (si, se puede saber cuando alguien esta utilizando un Pwnagotchi).

Para ello, en esta seccion, vamos a configurarlo con el objetivo de que realice operaciones de pruebas controladas y seguras (sin importar por donde se alimente, garantizando seguridad).

<br>
<br>

### 🧩 Personalization and Options

<br>
<br>

### 📡 Upgrades
- ***Micro USB to USB A OTG Adapter***: Este adaptador nos permitira que la Raspberry Pi pueda tener acceso a otros dispositivos que permitan expandir sus capacidades.

<br>

- ***TP Link AC600 WIFI Antenna***: Junto al adaptador Micro USB OTG, podemos expandir el rango de ataque de nuestro dispositivo colocando una antena WIFI externa, siempre que tenga disponible la configuracion `Monitor`.

<br>
<br>

### 🧊 3D Cases (📌 in progress)

<br>

### I hope you found this helpful and enjoyable. If so, leave a star ⭐ Best wishes and much success!
