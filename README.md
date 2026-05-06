# >°-°< Pwnagotchi 

<p align="center">
<img width="400" height="400" alt="WhatsApp Image 2026-04-27 at 12 16 46" src="https://github.com/user-attachments/assets/7599c37a-0f94-436d-b2f4-92932b664243" />
</p>


## ⚖️ Legal Disclaimer
The creator of this repository is not responsible for any malicious or inappropriate use of the device described. It is strictly prohibited to interfere with other Wi-Fi networks without consent or adequate security measures.

### ✅ Safe environments and measures
You can target a personal network with the pwnagotchi attack as a proof of use, or simply put it in passive mode. The repository will explain in detail how to do this.

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

## 🔎 Step by step

### 🛠️ Construction & Connections 
   - En primer lugar, soldaremos todos los pines de la Raspberry Pi Zero 2 W. Tener cuidado al soldar ya que los pines se consumen/derriten. Para ello, un metodo efectivo para soldar sin quemar todo en el proceso es el del siguiente video: https://www.youtube.com/watch?v=jYKzsLmMV6o
   - Una vez hecho eso, le conectaremos al UPS Hat la bateria de LiPo. Luego, mediante los tornillos que nos vienen incluidos en el paquete de Waveshare, colocamos esta placa de alimentacion por debajo de la Raspberry Pi. Sobre el UPS Hat, 6 pines de la Raspberry Pi (del lado corto y soldado) deben hacer contacto y presion sobre los 6 pines retraibles que el UPS tiene. Con ello, pasaremos a verificar la conexion y la alimentacion para comprobar si la Raspberry Pi se encendera sin problemas.

     ¿Como realizamos la verificacion?
   
   - Concluido con lo anterior, pasamos a colocar la pantalla de tinta electronica (el conector de 8 pines, debe estar del mismo lado que los puertos de conexion de la Raspberry Pi)


<br>

### 💻 Firmware
   - Several websites offer different versions of pwnagotchi. In this repository, we will use the firmware located in the #firmware folder.
     
   - Once the `.rar` file with extension `.img` has been downloaded, we need to prepare our Micro SD card in a Micro SD card holder to insert it into our PC and flash it with the file we downloaded.
     
   - To flash the card, it is recommended to use the applications: `balenaEtcher` o `Raspberry Imager`. Depending on which flashing tool we select, we must:
     - For `balenaEtcher`:
       - Select the corresponding `.img` file
       - Select the storage location
       - Write the file
         
     - For `Raspberry Imager`:
       - Select the board (in this case, a `Raspberry Pi Zero 2 W`)
       - Select `Use custom` in the next tab, where you will locate your `.img` file
       - Select the storage location
       - Write the file

<br>


### 🧩 Personalization and Options
<br>

### 📡 Upgrades
<br>

### 🧊 3D Cases
<br>

### I hope you found this helpful and enjoyable. If so, leave a star ⭐ Best wishes and much success!
