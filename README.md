# (◕‿‿◕) Pwnagotchi 

<p align="center">
<img width="450" height="500" alt="WhatsApp Image 2026-05-26 at 14 00 50" src="https://github.com/user-attachments/assets/0f9e8454-3988-4073-bb91-99c27390bef7" />
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

- `¿How it works?`

   To achieve its goal, Pwnagotchi combines low-power hardware (usually a Raspberry Pi Zero W or Zero 2 W) with a very         powerful software stack:

  - ***The Engine (Bettercap)***: At the heart of its offensive and scanning capabilities is BetterCap. Pwnagotchi uses this tool's API to interact with the network interface in monitor mode, inject packets (such as for deauthentication attacks), and capture traffic.

  - ***The Brain (Artificial intelligence)***: This is where the A2C model comes in. Pwnagotchi constantly evaluates its environment and makes decisions about which channels to scan, how long to stay on each, and what kind of deauthentication packets to send to connected clients. If its decisions result in the successful capture of a handshake (its reward), the neural network adjusts its weights to favor that behavior in the future.
  
  - ***¿How handshakes are used in the WPA/WPA2?***
  
       <p align="center">
       <img width="550" height="500" alt="image (1)" src="https://github.com/user-attachments/assets/23d633b5-5210-40a5-8131-3499a48a613b" />
       </p>

  - ***Personality (UI and States)***: Its mood reflects what's happening at the network and hardware levels. If it's capturing a lot of handshakes, it will be happy. If there's little traffic or it's not capturing any, it will get bored or sad. This interface is usually displayed on an e-ink screen, giving it that characteristic cyber Tamagotchi look.
  
    👉 ***Its moods are:***


      | Mood &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | What it means | 
      | :--- | :--- | 
      | `(⇀‿‿↼) sleeping` | This is the state the unit will start from. Moreover, from time to time your Pwnagotchi will also perform naps of a few seconds while hopping among WiFi channels |
      | `(≖‿‿≖) awakening` | The unit is in the last seconds of its nap |
      | `(◕‿‿◕) awake / normal` | This face is the neutral awake status of the unit. It’ll be used to smooth the transition between other moods and in general when there’s no external cause of either positive or              negative moods. It can also be used, randomly, when another unit is encountered for the first time (each unit keeps a record of all the units it met) |
      | `( ⚆⚆), (☉☉ ) observing (neutral mood)` | Your Pwnagotchi is waiting and observing what bettercap can find on all the channels it’s hopping on |
      | `( ◕‿◕), (◕‿◕ ) observing (happy)` | When there’s one or multiple units nearby and their cumulative bond counter is greater or equal than the personality.bond_encounters_factor, this will be the unit’s face          while observing |
      | `(°▃▃°) intense` | The unit is sending an association frame to an access point in order to force it to leak the PMKID |
      | `(⌐■_■) cool` | The unit is deauthenticating a client station from an access point. This face can also be picked randomly when meeting another unit for the first time |
      | `(•‿‿•) happy` | Your Pwnagotchi is happy in one of the following cases:<ul><li>The AI just finished loading and it’s ready</li><li>Valid key material for an access point has just been captured</li><li>In MANU         mode (MANUAL MODE), if the last session was short or if any handshake has been captured during it</li><li>When another unit is met and the bond level is high enough</li></ul> |
      | `(^‿‿^) grateful` | Your Pwnagotchi is grateful in one of the following cases:<ul><li>The cumulative bond level of nearby units is at least five times the personality.bond_encounters_factor</li><li>The unit            should be bored, but there are enough friendly units nearby</li><li>The unit should be sad, but there are enough friendly units nearby</li><li>The unit should be lonely, but there are enough friendly units                 nearby</li></ul> |
      | `(ᵔ◡◡ᵔ) excited` | Your Pwnagotchi is excited in one of the following cases:<ul><li>The number of epochs with some activity is greater or equal than personality.excited_num_epochs</li><li>Randomly if a unit with        a high bond level is met</li><li>If you have unread PwnMAIL messages on that unit</li></ul> |
      | `(✜‿‿✜) smart` | Randomly if a unit with a med-high bond level is met |
      | `(♥‿‿♥) friendly` | Randomly if a unit with a high bond level is met |
      | `(☼‿‿☼) motivated` | Your Pwnagotchi just scored the best reward level in its existence or just met a unit with a high bond |
      | `(≖__≖) demotivated` | Your Pwnagotchi just scored the worst reward level in its existence |
      | `(-__-) bored` | If there are no friendly units around and the amount of consecutive inactive epochs reached personality.bored_num_epochs |
      | `(╥☁╥ ) sad` | If there are no friendly units around and the amount of consecutive inactive epochs reached personality.sad_num_epochs |
      | `(.__.) lonely` | If your Pwnagotchi just lost contact with a friendly unit that was nearby, or if the amount of missed interactions with access points or client stations (the amount of times it tried to send some       type of packet but missed the target because it isn’t in range anymore) is greater or equal than personality.max_misses_for_recon. And there are no friendly units around |
      | `(☓‿‿☓) broken` | Your unit is rebooting either as a coping strategy for the blindness bug, or after installing an update |
      | `(#__#) debugging` | Used for debug and test messages on screen |
   

<br>

- `The life cycle of a Pwnagotchi
When you turn on your Pwnagotchi, it goes through different phases:`

  - ***Recognition (Blind/Bored)***: Scan the channels looking for Access Points (APs) and active clients.
  
  - ***Association and Attack***: When it finds a viable target, it can passively wait for a client to connect, or force reconnection by sending deauthentication frames to capture the 4-way handshake.

  - ***Capture***: By intercepting the handshake or PMKID, it saves it to a local .pcap file. This file is the "food" that you can then extract to try to crack the password on another computer (using tools like Hashcat).

  - ***Socialization***: If one Pwnagotchi detects another nearby (using custom dot11 packets), they can "talk" to each other, share information about the environment, and modify each other's behavior.
  
<br>
<br>

## 🔎 Step by step

### 🛠️ Construction & Connections 
   - First, we'll solder all the pins of the Raspberry Pi Zero 2W. Be careful when soldering, as the pins can corrode/melt. An effective method for soldering without burning everything in the process is shown in the following video: https://www.youtube.com/watch?v=jYKzsLmMV6o
     
   - As a next step, we checked the feeding system for the pwnagotchi:
   
      - ¿How do we perform the verification?
      
        - `Measure the voltage of the LiPo battery`
          - Using a multimeter we will verify the voltage of the 3.7v LiPo battery.
          - We connect the multimeter probes to their respective connectors on the multimeter itself (black wire to `COM`, and red wire to `V, Ω, Hz, °C, ...`).
          - Then we set the multimeter's selector switch to `V---` (DC voltage), and to the value `6v`.
          - And finally, we take measurements. We place the `red lead` of the multimeter on the `red or positive` side of the battery, and the `black lead` of the multimeter on the `black or negative` side of the battery.
        
        - `Check the solder joints of the Raspberry Pi Zero 2W`
        
        - `Check the operation of the Waveshare Hat UPS board` 
          - Connect the LiPo battery to the UPS board (if it wasn't already connected).
          - Next, we must turn the switch on `ON` on that board.
          - Using a `USB-C` to `USB-A` cable, connect the UPS to your PC. A red LED on the UPS should light up; leave it on for a few seconds, then disconnect it. 
          - Finally, we turn the switch to `OFF` and turn our Hat UPS board back on with the switch in `ON` (this is to perform a reset), and it should now be able to provide power on its own.

   - Once the power supply system is verified, using the screws included in the Waveshare package, place the UPS Hat underneath the Raspberry Pi. On this power supply board, 6 pins of the Raspberry Pi (on the short, soldered side of the board) must make contact and apply pressure to the 6 retractable pins on the UPS.
   
   - Having completed the above, we proceed to install the e-ink display. To verify that it has been installed correctly, the 8-pin connector of this display must be parallel to, or on the same side as, the Raspberry Pi's connection ports (which are: `USB`, `Mini HDMI`, and `PWR IN`).

   - The connection setup is complete ✅

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
   
      - ¿How do we add this file?
        - To do this, we will create a common text file (give it any name).
        - Next, we need to configure the file display in our Windows 11 disk folder. We'll go to `View`, then select `Show` from the drop-down menu, and finally `File name extensions`.
        - With this configuration, we will see all the extensions of our files in that disk folder.
        - So, what we'll do is select our created text file, right-click on it, and then click on `Rename`. Here we select everything, including the `.txt` extension, and enter: `config.toml`.
        - A warning message will appear indicating that we are changing the file extension type; click `OK`. At this point, your additional file will be created.
        - Since it's a new file, it doesn't contain any information, commands, or other content. Next, we'll add the following code:
     
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

   - In addition to the previous file, we will modify two other files: `config.txt` and `cmdline.txt`. We will do this by editing them and opening them with Notepad (right-clicking the file to be edited and selecting `Open with Notepad`).
   
     - For `config.txt`, we remove its existing code and replace it with:
     
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
          
     - For `cmdline.txt`, we removed its existing code and replaced it with:
     
       ```
       console=serial0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 fsck.repair=yes rootwait modules-load=dwc2,g_ether
       ```

 <br>

   - We save the changes in Notepad (in each file).

 <br>

   - We disconnect the SD holder from our PC and place the SD card in our Raspberry Pi.
     
   <br>

   - Next, to perform the first functionality test, we connected the Micro USB cable to the Raspberry Pi board in its `USB` port (and not to the `PWR IN` port), and the `USB A` of the cable to our PC. In Pwnagotchi's firmware, the Raspberry Pi's `USB` port is in a `safe mode` or rather, a `manual mode`. This means that powering the board through this port with the firmware loaded will not automatically execute the deauthentication and handshake processes. Therefore, we can verify if the program is running correctly, without the need for it to automatically attack nearby networks.
   
<br>
     
   - If there are no errors, you will now be able to see Pwnagotchi's firmware working (and its cute but fierce face).

<br>
   
   - On the first boot (whether connected via the `USB` port or the motherboard's `PWR IN` port), the firmware will take a little while to load because it's generating the configuration keys and other information. A notification will appear on the screen during this process.
   
   ⚠️ ***NOTE:*** During this initialization phase, the device should not be disconnected to avoid errors.

<br>

   - After it has initialized, when we disconnect it and reconnect it, it will start running normally and faster at startup.

<br>

   - Finally, we'll make our Pwnagotchi portable using the Waveshare Hat UPS. Simply turn the switch on this board to `ON`.


<br>

   - And that's it! ✅ We now have our Pwnagotchi hacking device up and running!
   
<br>

***⚠️ NOTE:*** If you connect the Micro USB cable to the Raspberry Pi's `PWR IN` port, or power the board using the Hat UPS board, the Pwnagotchi firmware will begin to operate uncontrollably, entering its default `auto mode`, capturing handshakes and deauthenticating devices. To avoid violating any laws, you must proceed with a secure and controlled connection and configuration.

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
- ***Micro USB to USB A OTG Adapter***: This adapter allows the Raspberry Pi to access other devices/peripherals, expanding its capabilities (e.g: keyboards, adapters, mouse, and more)

<br>

- ***TP Link AC600 WIFI Antenna***: Along with the Micro USB OTG adapter, we can extend our device's attack range by adding an external Wi-Fi antenna, provided the 'Monitor' configuration is available. This expands the Wi-Fi signal's range, enabling better access point identification and allowing Pwnagotchi, through its AI, to apply the learning observed in previous handshake captures to new ones.

<br>
<br>

### 🧊 3D Cases (📌 in progress)

<br>

### I hope you found this helpful and enjoyable. If so, leave a star ⭐ Best wishes and much success!
