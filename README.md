<p align="center">
<img src="https://user-images.githubusercontent.com/51358498/152991504-005a1daa-2900-4f48-8bec-d163d6336ed2.png" width="400">
</p>

# OpenWeedLocator

Welcome to the OpenWeedLocator (OWL) project, an opensource hardware and software weed detector that uses
entirely off-the-shelf componentry, very simple green-detection algorithms (with capacity to upgrade to
in-crop detection) and 3D printable parts. OWL integrates weed detection on a Raspberry Pi with a relay
control board or custom driver board, in a custom designed case so you can attach any 12V solenoid, relay, lightbulb or 
device for low-cost, simple and open-source site-specific weed control. Projects to date have seen OWL mounted on robots,
vehicles and bicycles for spot spraying. For the latest ideas and news, check out the [Discussion](https://github.com/geezacoleman/OpenWeedLocator/discussions) tab.

### News
**08-05-2024** - Check out the latest Compact OWL enclosures!

|                                           | Front                                                                                                                    | Back                                                                                                                    |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Official OWL extruded aluminium enclosure | ![front_enclosure](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/c5d8c4d7-21d0-4987-9691-cd9a8615b65a) | ![enclosure_back](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/4ddf0538-265e-4e6b-aebd-040336d1562b) |
| 3D printable enclosure                    |  ![20240502_214051_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/beb40fca-723d-4f2b-9555-46bc0587cd8d)                                                                                                                        |        ![3d-printed_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/aa4898ff-5481-4d89-98ba-656302ac70b1)                                                                                                                 |

Find all the 3D printable files [on the OWL repository](#3d-printing) or download them from 
[Printables](https://www.printables.com/model/875853-raspberry-pi-rugged-imaging-enclosure).

**13-04-2024** - OpenWeedLocator now supports Raspberry Pi 5 and picamera2! Improvements include:
* support for both picamera and picamera2
* implementation of a `config/config.ini` approach to setting detection parameters
* cleaner, more consistent code

**10-04-2024** - v2.1 of the [OWL driver board released](https://github.com/geezacoleman/owl-driver-board).
* simplifies assembly
* more robust and improved performance

### OWLs in Action

|                                                                OWL on a vehicle                                                                 |                                            OWL on the AgroIntelli Robotti                                             | OWL on the Agerris Digital Farmhand | OWL on a bicycle |
|:-----------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------:|-------------------------------------|------------------|
| ![Fitted module - spot spraying vehicle](https://user-images.githubusercontent.com/51358498/130522810-bb19e6ca-5019-4de4-83cc-858eca358ef8.jpg) | ![robotti_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/99df0188-a850-4753-ac48-ab743c46d563) |                   ![OWL - on robot agerris](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/9cb73514-dffc-4c53-969e-c1c816610f1b)                  |          ![bike_owl_cropped](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/17ad4ead-429e-4384-9e74-b050a536897f)        |

### Official Publications

#### OpenWeedLocator (OWL): An open-source, low-cost device for fallow weed detection

This is the original OWL publication, released
in [Scientific Reports (open access)](https://www.nature.com/articles/s41598-021-03858-9). A range of green detection
algorithms were tested including ExG (excess green 2g - r - b, developed by Woebbecke et al. 1995), a hue, saturation
and value (HSV) threshold and a combined ExG + HSV algorithm. If you use the OWL in your research please consider citing
this publication.

#### Investigating image-based fallow weed detection performance on Raphanus sativus and Avena sativa at speeds up to 30 km/h

The performance of the OWL from 5 - 30 km/h with different cameras and on broadleaf and grass 'weeds' was tested and
published
in [Computers and Electronics in Agriculture](https://www.sciencedirect.com/science/article/pii/S0168169923008074). The
current Raspberry Pi HQ Camera + latest software combination provided a recall of 74.8% at 5 km/h and 50.5 % at 30 km/h.
Recall of up to 95.7% at 5 km/h was achieved by the global shutter Arducam AR0234.

Repository DOI: [![DOI](https://zenodo.org/badge/399194159.svg)](https://zenodo.org/badge/latestdoi/399194159)

# Overview

* [OWL Use Cases](#owl-use-cases)
* [Community Development](#community-development-and-contribution)
* [Hardware Requirements](#hardware-requirements)
    - [Hardware Assembly](#hardware-assembly)
    - [Single Board Computer (SBC) Options](#sbc-options)
* [Software Installation](#software)
    - [Quick Method](#quick-method)
    - [Detailed Method](#detailed-method)
    - [Changing Detection Settings](#changing-detection-settings)
    - [Green-on-Green (available NOW) :eyes::dart::seedling:](#green-on-green)
    - [Installing on non-Raspberry Pi Computers](#non-raspberry-pi-installation)
* [3D Printing](#3d-printing)
* [Updating OWL](#updating-owl)
    - [Version History](#version-history)
* [Troubleshooting](#troubleshooting)
* [Citing OWL](#citing-owl)
* [Acknowledgements](#acknowledgements)
* [References](#references)

### Manuals

If you prefer a hardcopy version of these instructions, you can view and download the PDF using one of the links below.
These will be updated as major changes are made. All older versions will be retained within the `docs` folder.

**Current**

* [2024-05-28 - Download OWL manual](docs/20240528_owl_readme.pdf)

[View all versions](docs)

# OWL Use Cases

## Vehicle-mounted spot spraying

The first, and most clear use case for the OWL is for the site-specific application of herbicide in fallow. As part of
the development and testing of the unit, the OWL team designed and assembled a 2 m spot spraying boom, using two OWLs to
control four 12 V solenoids each. The boom was mounted on the back of a ute/utility vehicle with the spray tank located
in the tray and powered by a 12V car battery. Indicator lights for each nozzle were used to highlight more clearly when
each solenoid had been activated for demonstration and testing purposes.

<p align="center">
<img src="https://user-images.githubusercontent.com/51358498/152991630-fe343f37-5a45-43b0-900c-bb3cad4f1b80.JPG" width="600">
</p>

Parameter | Details | Notes 
:-------------------------:|:-------------------------: |:-------------------------:
Mounting gap | 0 cm | Mounted directly to same bar as nozzles, just 32cm higher.
Forward Speed | 6 - 8 km/h | Image blur/activation time limiting forward speed. Moving the OWL unit forward would be a quick improvement for travel speed and large green weeds.
Solenoids | Goyen solenoid 3QH/3662 with Teejet body | Many alternatives exist as outlined in [#2](https://github.com/geezacoleman/OpenWeedLocator/issues/2)
Spray tips | Teejet TP4003E-SS | 40 degree, flat fan nozzles, stainless steel
Strainer | TeeJet 50 mesh strainer | Protect spray tip from clogging/damage
Pump/tank | Northstar 12V 60L ATV Sprayer | 8.3 LPM 12V pump, 60L capacity, tray mounted

## Robot-mounted spot spraying

A second system, identical to the first, was developed for the University of Sydney's Digifarm robot, the Agerris
Digital Farm Hand. The system is in frequent use for the site-specific control of weeds in trial areas. It is powered by
the 24V system on the robot, using a 24 - 12V DC/DC converter.

<p align="center">
<img src="https://user-images.githubusercontent.com/51358498/152990627-0f89bf92-87bc-4808-a748-33f0742068e4.jpg" width="500">
</p>

## Image data collection

The OWL can act as a high quality image data collection tool for developing image data training sets in realistic 
agricultural environments, attached to agricultural equipment. The approach allows whole-image, cropped-to-bounding-box 
and square images saved on a set frequency to a thumb drive.

Settings are updated in the `config.ini` file.

| **Method**  | **Code** | **Example** |
| ------------- | ------------- | ------------- |
| Whole image  | 'whole' | ![20220714-145951__frame_420](https://user-images.githubusercontent.com/51358498/178902742-45952737-ee3e-4a36-b9b3-216a19e78eb7.png) |
| Crop to bounding box  | 'bbox'  | ![20220714-145757__frame_420_n_4](https://user-images.githubusercontent.com/51358498/178902795-96bb8068-cf58-4f5a-8819-8ca538add384.png) |
| Crop to square around weed centre | 'square' | ![20220714-150328__frame_420_n_4](https://user-images.githubusercontent.com/51358498/178903171-af7f8f1b-9caf-435e-96d0-4f01e76c53fb.png) |
| Deactivated (DEFAULT)  | None |  |

## Community development and contribution

As more OWLs are built and fallow weed control systems developed, we would love to share the end results here. Please
get in contact and we can upload images of the finished systems on this page.

Check out the OWL [Discussion](https://github.com/geezacoleman/OpenWeedLocator/discussions) page for any questions, suggestions ideas or feedback. If there's a bug or improvement,
please raise an issue.

Please review the [contribution page](CONTRIBUTING.md) for all the details on how to contribute and follow community
guidelines.

# Hardware Requirements

The specific hardware requirements and details for each OWL format are provided below. There are two designs developed 
to ensure improved performance without compromising on the original simplicity of the OWL:
1. Education layout (original OWL)
2. Compact OWL
   * extruded aluminium enclosure
   * 3D printed enclosure

| Original OWL | Compact OWL - Extruded Aluminium Enclosure                                                                            | Compact OWL - 3D Printed Enclosure                                                                                    |
|--------------|-----------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
|        ![Finished OWL - small](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/accae1b1-b00d-40f9-ab95-743b732df2a0)      | ![3D Printed OWL](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/a9771aa2-355d-40db-ac15-f6da037b63ed) | ![Extruded OWL](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/d153db2d-624b-427e-832e-599a3a841623) |

All 3D models and hardware assembly guides are provided in subsequent sections. The quantities of each item below are for 
one OWL detection unit for each respective design.

*Please note links provided in tables below to an example online retailer of each component for convenience only. There are
certainly many other retailers that may be better suited and priced to your purposes and we encourage you to find local
suppliers. Other types of connector, layout and design are also possible, which may change the parts required.*

## Official OWL Hardware
We now have a range of official OWL hardware available to build or purchase.

#### OWL Enclosure
The Official OWL Enclosure is an extruded aluminium enclosure with rubber seals and a glued with 2mm thick glass lens.
It provides a more production friendly, durable and water/chemical resisant option over 3D printed plastic.

#### OWL Driver Board
The [Official OWL driver board](https://github.com/geezacoleman/owl-driver-board) combines the relay control board, power supply and wiring. It will be available for
purchase soon, or you can use the files provided to order/make your own.

## Hardware Lists
<details>
<summary>Original OWL - Hardware List</summary>
<br>

### Original OWL
The original OWL lays out all components in a flat design. It makes the connections and interactions within the system
clear. It's a great educational tool to learn the parts required for a weed detection system and has served in the field 
as a functional weed detection system for a number of years.

| **Component**                                                         | **Quantity**      | **Link**                                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Enclosure**                                                         |                   |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Main Case (single Bulgin connector)                                   | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Enclosure%20-%20single%20connector.stl)                                                                                                                                                                                                                                                                           |
| *Main Case (cable glands)*                                            | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Enclosure%20-%20cable%20gland.stl)                                                                                                                                                                                                                                                                                |
| Main Cover                                                            | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Enclosure%20-%20cover.stl)                                                                                                                                                                                                                                                                                        |
| Raspberry Pi Mount                                                    | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Raspberry%20Pi%20mount.stl)                                                                                                                                                                                                                                                                                       |
| Relay Control Board Mount                                             | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Relay%20control%20board%20mount.stl)                                                                                                                                                                                                                                                                              |
| Voltage Regulator Mount                                               | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Voltage%20regulator%20mount.stl)                                                                                                                                                                                                                                                                                  |
| Camera Mount                                                          | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Camera%20mount.stl)                                                                                                                                                                                                                                                                                               |
| Enclosure Plug                                                        | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Enclosure%20plug.stl)                                                                                                                                                                                                                                                                                             |
| **Computing**                                                         |                   |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Raspberry Pi 5 4GB (or Pi 4 or 3B+)                                   | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-5-model-b-4gb.html)                                                                                                                                                                                                                                                                                                                                           |
| *Green-on-Green ONLY - Google Coral USB Accelerator                   | 1                 | [Link](https://coral.ai/products/accelerator)                                                                                                                                                                                                                                                                                                                                                                     |
| 64GB SD Card (min. 16 GB)                                             | 1                 | [Link](https://core-electronics.com.au/extreme-sd-microsd-memory-card-64gb-class-10-adapter-included.html)                                                                                                                                                                                                                                                                                                        |
| **Camera** (choose one)                                               |                   |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| RECOMMENDED: Raspberry Pi Global Shutter Camera                       | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-global-shutter-camera.html)                                                                                                                                                                                                                                                                                                                                   |
| CCTV 6mm Wide Angle Lens                                              | 1 (GS or HQ only) | [Link](https://core-electronics.com.au/raspberry-pi-6mm-wide-angle-lens.html)                                                                                                                                                                                                                                                                                                                                     |
| SUPPORTED: Raspberry Pi 12MP HQ Camera                                | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-hq-camera.html)                                                                                                                                                                                                                                                                                                                                               |
| SUPPORTED: Raspberry Pi Camera Module 3                               | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-camera-3.html)                                                                                                                                                                                                                                                                                                                                                |
| SUPPORTED: Raspberry Pi V2 Camera (NOT RECOMMENDED)                   | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-camera-board-v2-8-megapixels-38552.html)                                                                                                                                                                                                                                                                                                                      |
| NOTE: If you use the RPi 5, make sure you have the right camera cable | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-camera-fpc-adapter-cable-200mm.html)                                                                                                                                                                                                                                                                                                                          |
| **Power**                                                             |                   |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 5V 5A Step Down Voltage Regulator                                     | 1                 | [Link](https://core-electronics.com.au/pololu-5v-5a-step-down-voltage-regulator-d24v50f5.html)                                                                                                                                                                                                                                                                                                                    |
| 4 Channel, 12V Relay Control Board                                    | 1                 | [Link](https://www.jaycar.com.au/arduino-compatible-4-channel-12v-relay-module/p/XC4440?gclid=Cj0KCQjwvYSEBhDjARIsAJMn0ljQf_l5tRY0D4UyDRlaNBFV6-XAj_UGQzC029d-wiwoCyD6Rzy7x2MaAinhEALw_wcB)                                                                                                                                                                                                                       |
| M205 Panel Mount Fuse Holder                                          | 1                 | [Link](https://www.jaycar.com.au/round-10a-240v-m205-panel-mount-fuse-holder/p/SZ2028?pos=17&queryId=11c21fd77c75a11725bd0f093a0fc862&sort=relevance)                                                                                                                                                                                                                                                             |
| Jumper Wire                                                           | 1                 | [Link](https://core-electronics.com.au/solderless-breadboard-jumper-cable-wires-female-female-40-pieces.html)                                                                                                                                                                                                                                                                                                     |
| WAGO 2-way Terminal Block                                             | 2                 | [Link](https://au.rs-online.com/web/p/splice-connectors/8837544/)                                                                                                                                                                                                                                                                                                                                                 |
| Bulgin Connector - Panel Mount                                        | 1                 | [Link](https://au.rs-online.com/web/p/industrial-circular-connectors/8068625/)                                                                                                                                                                                                                                                                                                                                    |
| Bulgin Connector - Plug                                               | 1                 | [Link](https://au.rs-online.com/web/p/industrial-circular-connectors/8068565/)                                                                                                                                                                                                                                                                                                                                    |
| Micro USB to USB-C adaptor                                            | 1                 | [Link](https://core-electronics.com.au/usb-micro-b-to-usb-c-adapter-black.html)                                                                                                                                                                                                                                                                                                                                   |
| Micro USB Cable                                                       | 1                 | [Link](https://core-electronics.com.au/micro-usb-cable.html)                                                                                                                                                                                                                                                                                                                                                      |
| **Miscellaneous**                                                     |                   |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 12V Chrome LED                                                        | 2                 | [Link](https://www.jaycar.com.au/12v-mini-chrome-bezel-red/p/SL2644)                                                                                                                                                                                                                                                                                                                                              |
| 3 - 16V Piezo Buzzer                                                  | 1                 | [Link](https://www.jaycar.com.au/mini-piezo-buzzer-3-16v/p/AB3462?pos=8&queryId=404751ef55b1d6b8adef8b031d16576f&sort=relevance)                                                                                                                                                                                                                                                                                  |
| Brass Standoffs - M2/3/4                                              | Kit               | [Link](https://www.amazon.com/Hilitchi-360pcs-Female-Standoff-Assortment/dp/B013ZWM1F6/ref=sr_1_5?dchild=1&keywords=standoff+kit&qid=1623697572&sr=8-5)                                                                                                                                                                                                                                                           |
| M3 Bolts/Nuts                                                         | 4 each or Kit     | [Link](https://www.amazon.com/DYWISHKEY-Pieces-Stainless-Socket-Assortment/dp/B07VNDFYNQ/ref=sr_1_4?crid=2X7QROKBF9F4D&dchild=1&keywords=m3+hex+bolt&qid=1623697718&sprefix=M3+hex%2Caps%2C193&sr=8-4)                                                                                                                                                                                                            |
| Wire - 20AWG (red/black/green/blue/yellow/white)                      | 1 roll each       | [Link](https://www.amazon.com/Electronics-different-Insulated-Temperature-Resistance/dp/B07G2GLKMP/ref=sr_1_1_sspa?dchild=1&keywords=20+awg+wire&qid=1623697639&sr=8-1-spons&psc=1&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUEyMUNVM1BBQUNKSFNBJmVuY3J5cHRlZElkPUEwNjQ4MTQ5M0dRTE9ZR0MzUFE5VyZlbmNyeXB0ZWRBZElkPUExMDMwNTIwODM5OVVBOTFNRjdSJndpZGdldE5hbWU9c3BfYXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ==) |
| *Optional*                                                            |                   |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Real-time clock module                                                | 1                 | [Link](https://core-electronics.com.au/adafruit-pirtc-pcf8523-real-time-clock-for-raspberry-pi.html)                                                                                                                                                                                                                                                                                                              |

</details>

<details>
<summary> Compact OWL - Hardware List</summary>
<br>

### Compact OWL
The new OWL design is more compact, inside either an extruded aluminium enclosure or 3D printed housing. It offers
improved water and dust resistance, plus ease of assembly and longevity. This design is recommended for production use.

The parts list is substantially reduced:

| **Component**                                                         | **Quantity**      | **Link**                                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Enclosure**                                                         |                   |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **OFFICIAL OWL ENCLOSURE** - aluminium                                | 1                 | TBD                                                                                                                                                                                                                                                                                                                                                                                                               |
| Extrusion - 3D printed                                                | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Compact%20OWL/Main%20Body.stl)                                                                                                                                                                                                                                                                                                   |
| Front plate                                                           | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Compact%20OWL/Frontplate.stl)                                                                                                                                                                                                                                                                                                    |
| Tray                                                                  | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/picamera2/3D%20Models/Compact%20OWL/Tray.stl)                                                                                                                                                                                                                                                                                                     |
| Back plate - Amphenol, Adafruit RJ45                                  | 1*                | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Compact%20OWL/Backplate%20-%20Receptacle%20and%20Ethernet.stl)                                                                                                                                                                                                                                                                   |
| Back plate - Amphenol only                                            | 1*                | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Compact%20OWL/Backplate%20-%20Receptacle%20Only.stl)                                                                                                                                                                                                                                                                             |
| Back plate - 16 mm cable gland                                        | 1*                | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Compact%20OWL/Backplate%20-%20Gland.stl)                                                                                                                                                                                                                                                                                         |
| Lens mount                                                            | 1                 | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Compact%20OWL/Lens%20Mount.stl)                                                                                                                                                                                                                                                                                                  |
| Camera mount                                                          | 1*                | [STL File](https://github.com/geezacoleman/OpenWeedLocator/blob/picamera2/3D%20Models/Compact%20OWL/Camera%20Mount.stl)                                                                                                                                                                                                                                                                                           |
| **Computing**                                                         |                   |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Raspberry Pi 5 4GB (or Pi 4 or 3B+)                                   | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-5-model-b-4gb.html)                                                                                                                                                                                                                                                                                                                                           |
| *Green-on-Green ONLY - Google Coral USB Accelerator                   | 1                 | [Link](https://coral.ai/products/accelerator)                                                                                                                                                                                                                                                                                                                                                                     |
| 64GB SD Card (min. 16 GB)                                             | 1                 | [Link](https://core-electronics.com.au/extreme-sd-microsd-memory-card-64gb-class-10-adapter-included.html)                                                                                                                                                                                                                                                                                                        |
| **Camera** (choose one)                                               |                   |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| RECOMMENDED: Raspberry Pi Global Shutter Camera                       | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-global-shutter-camera.html)                                                                                                                                                                                                                                                                                                                                   |
| CCTV 6mm Wide Angle Lens                                              | 1 (GS or HQ only) | [Link](https://core-electronics.com.au/raspberry-pi-6mm-wide-angle-lens.html)                                                                                                                                                                                                                                                                                                                                     |
| SUPPORTED: Raspberry Pi 12MP HQ Camera                                | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-hq-camera.html)                                                                                                                                                                                                                                                                                                                                               |
| SUPPORTED: Raspberry Pi Camera Module 3                               | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-camera-3.html)                                                                                                                                                                                                                                                                                                                                                |
| SUPPORTED: Raspberry Pi V2 Camera (NOT RECOMMENDED)                   | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-camera-board-v2-8-megapixels-38552.html)                                                                                                                                                                                                                                                                                                                      |
| NOTE: If you use the RPi 5, make sure you have the right camera cable | 1                 | [Link](https://core-electronics.com.au/raspberry-pi-camera-fpc-adapter-cable-200mm.html)                                                                                                                                                                                                                                                                                                                          |
| **Power Management** * items only needed in place of OWL driver board | 1                 |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **OFFICIAL OWL DRIVER BOARD** (incl. power mgmt, relay control)       | 1                 | TBD                                                                                                                                                                                                                                                                                                                                                                                                               |
| * 5V 5A Step Down Voltage Regulator                                   | 1                 | [Link](https://core-electronics.com.au/pololu-5v-5a-step-down-voltage-regulator-d24v50f5.html)                                                                                                                                                                                                                                                                                                                    |
| * 4 Channel, Relay Control Board HAT                                  | 1                 | [Link](https://core-electronics.com.au/pirelay-v2-relay-board-for-raspberry-pi-1.html?gad_source=1&gclid=Cj0KCQjw_qexBhCoARIsAFgBlev42xD_VLsmZHCLmIPB-NCCMRCGtKRPbH7WV2ddw4oucobn-XOUpLkaArl5EALw_wcB)                                                                                                                                                                                                            |
| * Jumper Wire                                                         | 1                 | [Link](https://core-electronics.com.au/solderless-breadboard-jumper-cable-wires-female-female-40-pieces.html)                                                                                                                                                                                                                                                                                                     |
| Amphenol Fathomlock Connector - 6 pin connector (FLS6BS10N3W3P03)     | 1                 | [Link](https://au.mouser.com/ProductDetail/Amphenol-SINE-Systems/FLS6BS10N3W3P03?qs=ulEaXIWI0c%2FMtNeYzYmViA%3D%3D)                                                                                                                                                                                                                                                                                               |
| Amphenol Fathomlock Connector - 6 pin plug (FLS710N3W3S03)            | 1                 | [Link](https://au.mouser.com/ProductDetail/Amphenol-SINE-Systems/FLS710N3W3S03?qs=ulEaXIWI0c8tWp%252BkBCr3Ag%3D%3D)                                                                                                                                                                                                                                                                                               |
| Adafruit RJ45 Cable Gland                                             | 1                 | [Link](https://au.mouser.com/ProductDetail/Adafruit/827?qs=GURawfaeGuA%2FhbkGNTwr3g%3D%3D)                                                                                                                                                                                                                                                                                                                        |
| 16mm Cable Gland                                                      | 1                 | [Link](https://au.mouser.com/ProductDetail/Davies-Molding/GC1000-B?qs=xhbEVWpZdWd7C8HYv4mDiQ%3D%3D)                                                                                                                                                                                                                                                                                                               |
| **Miscellaneous**                                                     |                   |                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 3 - 16V Piezo Buzzer (optional)                                       | 1                 | [Link](https://www.jaycar.com.au/mini-piezo-buzzer-3-16v/p/AB3462?pos=8&queryId=404751ef55b1d6b8adef8b031d16576f&sort=relevance)                                                                                                                                                                                                                                                                                  |
| Brass Standoffs - M2/3/4 (required for HAT/driver board)              | Kit               | [Link](https://www.amazon.com/Hilitchi-360pcs-Female-Standoff-Assortment/dp/B013ZWM1F6/ref=sr_1_5?dchild=1&keywords=standoff+kit&qid=1623697572&sr=8-5)                                                                                                                                                                                                                                                           |
| Wire - 20AWG (red/black/green/blue/yellow/white)                      | 1 roll each       | [Link](https://www.amazon.com/Electronics-different-Insulated-Temperature-Resistance/dp/B07G2GLKMP/ref=sr_1_1_sspa?dchild=1&keywords=20+awg+wire&qid=1623697639&sr=8-1-spons&psc=1&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUEyMUNVM1BBQUNKSFNBJmVuY3J5cHRlZElkPUEwNjQ4MTQ5M0dRTE9ZR0MzUFE5VyZlbmNyeXB0ZWRBZElkPUExMDMwNTIwODM5OVVBOTFNRjdSJndpZGdldE5hbWU9c3BfYXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ==) |

</details>

## Hardware Assembly
Separate guides are provided for the Original OWL assembly and the Compact OWL.

### Required tools
* Wire strippers
* Wire cutters
* Pliers
* Soldering iron/solder (only for Original OWL)

<details>
<summary> Original OWL - Hardware Assembly</summary>
<br>

**NOTE:** All components listed above are relatively "plug and play" with minimal soldering or complex electronics required.
Follow these instructions carefully and triple check your connections before powering anything on to avoid losing
the [magic smoke](https://en.wikipedia.org/wiki/Magic_smoke) and potentially a few hundred dollars. Never make changes
to the wiring on the detection unit while it is connected to 12V and always remain within the safe operating voltages of
any component.

## Original OWL - Hardware Assembly

A [video guide](https://www.youtube.com/watch?v=vZqNKogzz8k) is available for the Original OWL assembly.

Before starting, have a look at the complete wiring diagram below to see how everything fits together. The LEDs, fuse and Bulgin connector are all mounted on the rear of the OWL unit, rather than where they are located in the diagram. If you prefer not to use or can't access a Bulgin connector, there is a separate 3D model design that uses cable glands instead.

![wiring diagram-01](https://user-images.githubusercontent.com/40649348/156698009-a58ed01b-258f-462a-9524-ba3f8d7ec246.png)

### Step 1 - enclosure and mounts

Assembling the components for an OWL unit requires the enclosure and mounts as a minimum. These can be 3D printed on
your own printer or printed and delivered from one of the many online stores that offer a 3D printing service.
Alternatively, you could create your own enclosure using a plastic electrical box and cutting holes in it, if that's
easier. We'll be assuming you have printed out the enclosure and associated parts for the rest of the guide, but please
share your finished designs however they turn out!

The first few steps don't require the enclosure so you can make a start right away, but while you're working on getting
that assembled, make sure you have the pieces printing, they'll be used from Step 4. For a complete device, you'll need:
1 x base, 1 x cover, 1 x RPi mount, 1 x relay mount, 1 x regulator mount, 1 x camera mount and 1 x plug.

### Step 2 - soldering

There are only a few components that need soldering, including the fuse and voltage regulator:

* Soldering of voltage regulator pins
* Soldering of 12V input wires to voltage regulator pins
* Soldering of 5V output wires to voltage regulator pins (micro USB cable)
* Soldering of red wire to both fuse terminals

Carefully check which pins on the voltage regulator correspond to 12V in, GND in, 5V out and GND out prior to soldering.

To solder the Micro USB cable to the voltage regulator output, you'll need to cut off the USB A end so you are left with
approximately 10cm of cable. Using the wire strippers or a sharp box cutter/knife, remove the rubber sheath around the
wires. If you have a data + charging cable you should see red, green, white and black wires. The charging only cables
will likely only have the red and black wires. Isolate the red (+5V) and black (GND) wires and strip approximately 5mm
off the end. Solder the red wire to the positive output on the voltage regulator and black wire to the GND pin. Once you
have finished, it should look like the first panel in the figure below.

**NOTE**: Soldering can burn you and generates potentially hazardous smoke! Use appropriate care, fume extractors and
PPE to avoid any injury. If you're new to soldering, read
through [this guide](https://www.makerspaces.com/how-to-solder/), which explains in more detail how to perfect your
skills and solder safely.

**NOTE**: When soldering, it's best to cover the exposed terminals with glue lined heat shrink to reduce the risk of
electrical short circuits.

Voltage regulator | Voltage regulator pins | Fuse
:-------------: | :-------------: | :-------------: 
![Vreg](https://media.github.sydney.edu.au/user/5402/files/12c53200-ce9e-11eb-812b-52c51a0c6263) | ![Vregpins](https://media.github.sydney.edu.au/user/5402/files/85abe580-d023-11eb-87ee-c3cad42406fe)| ![Fuse](https://media.github.sydney.edu.au/user/5402/files/240e3e80-ce9e-11eb-8c0f-25e296720072)

Once the two red wires are soldered to the fuse, the fuse can be mounted on the rear panel of the OWL base. One wire
will be connected to the Bulgin plug (next step) and the other to the Wago 2-way block.

For neater wiring you can also solder jumpers between all the normally open (NO) pins on the base of the relay board,
but this is optional. If you don't solder these connections, make sure you connect wire using the screw terminals
instead. Photos of both are provided below.

Soldered | Screw terminals
:-------------: | :-------------: 
![Relayboardunderside](https://media.github.sydney.edu.au/user/5402/files/e5938500-cf6c-11eb-91a2-75685a6d948d) | ![Relayboardalternative](https://media.github.sydney.edu.au/user/5402/files/e88e7580-cf6c-11eb-8e26-7bbce2fb3f71)

The other wires requiring soldering are joins between the buzzer and jumper wires for easy connection to the GPIO pins
and from the LEDs to the power in/jumper wires.

### Step 3 - wiring up Bulgin connector

Next we'll need to wire the output relay control and input 12V wires to the Bulgin panel mount connector. Fortunately
all pins are labelled, so follow the wire number table below. This will need to be repeated for the Bulgin plug as well,
which will connect your solenoids or other devices to the relay control board.

The process is:

1. Connect all wires to Bulgin connector using the screw terminals
2. Mount the connector to the rear panel
3. Leave at least 10cm of wire so it can be connected to the relay board and other connections later.

Bulgin terminal number | Wire connection
:-------------: | :-------------: 
1 | Blue wire - connects to centre terminal (common) on relay 1
2 | Green wire - connects to centre terminal (common) on relay 2
3 | Orange wire - connects to centre terminal (common) on relay 3
4 | White wire - connects to centre terminal (common) on relay 4
5 | Red 12VDC - connects to fuse wire already soldered. Make sure wire is the right length when mounted. 
6 | Black GND - connects to Wago 2-way terminal

**NOTE**: Skip this step if you're using cable glands.

Once all the wires have been connected you can now mount the Bulgin connector to the OWL base.

### Step 4 - mounting the relay control board and voltage regulator

Attach the relay control board to the 3D printed relay control board mount using 2.5 mm standoffs. Attach the voltage
regulator to the 3D printed voltage regulator mount with 2 mm standoffs. The mounted voltage regulator can then be
mounted to one corner of the relay control board. The relay board and voltage regulator can then be installed in the
raised slots in the OWL base.

**NOTE**: Use **2.5 mm** standoffs for mounting the relay control board to its base. Use **2 mm** standoffs to mount the
voltage regulator to its base.

![Relaymount](https://media.github.sydney.edu.au/user/5402/files/964c5500-cf6a-11eb-8d2f-e1282b6411c3)

### Step 5 - wiring the relay control board, voltage regulator, Wago 2-way blocks and Bulgin connector

Connect the relay control board to the Bulgin connector using the table in step 3 as a guide.

**NOTE**: Some relay control boards such
as [this](https://www.amazon.com/ELEGOO-Channel-Optocoupler-Arduino-Raspberry/dp/B01HEQF5HU/ref=asc_df_B01HEQF5HU/?tag=hyprod-20&linkCode=df0&hvadid=198076677096&hvpos=&hvnetw=g&hvrand=5997956897740931812&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9027902&hvtargid=pla-350609711896&psc=1)
on Amazon are ACTIVE on LOW. This means that the signal provided by the Raspberry Pi (a higher voltage) to activate a
relay will instead turn the relay off. While this can be changed in the code, please consider purchasing HIGH level
trigger (
e.g [the board specified in the parts list](https://www.jaycar.com.au/arduino-compatible-4-channel-12v-relay-module/p/XC4440))
or adjustable trigger (
e.g. [this board](https://www.amazon.com/DZS-Elec-Optocoupler-Isolation-Triggered/dp/B07BDJJTLZ/ref=asc_df_B07BDJJTLZ/?tag=hyprod-20&linkCode=df0&hvadid=241912880102&hvpos=&hvnetw=g&hvrand=5997956897740931812&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9027902&hvtargid=pla-438273746158&psc=1)).

Next, connect red and black jumper wires to the VCC and GND header pins on the relay control board. Now choose one Wago
block to be a 12V positive block and the second to be the negative or ground. To the positive block, connect the 12 V
wire from the fuse (12V input from source), the 12 V input to the voltage regulator, the 12 V solenoid line from the
relay board and the VCC line from the relay board to one of the two WAGO terminal blocks, twisting the wires together if
necessary. Repeat with the second, negative WAGO terminal block, connecting the input ground line from the Bulgin
connector, ground line from the voltage regulator and the GND black wire from the relay board.

Installed relay board | Relay board wiring diagram | Relay board wiring
:-------------: | :-------------: | :-------------: 
![Relayboardinstalled](https://media.github.sydney.edu.au/user/5402/files/54c7a400-cf82-11eb-9fb3-250199227384) | ![OWL - relay board diagram](https://media.github.sydney.edu.au/user/3859/files/431ed600-cf5b-11eb-94df-87f01e0a41a4) | ![relayinputs](https://media.github.sydney.edu.au/user/5402/files/cad01780-d023-11eb-98e0-bfcc1c2c03e0) |

### Step 6 - mounting Raspberry Pi and connecting power

Attach the Raspberry Pi to the 3D printed mount using 2.5 mm standoffs. Install in the raised slots in the OWL base.
Connect to micro USB power from the voltage regulator, using a micro USB to USB-C adaptor. Alternatively, the Raspberry
Pi can be powered over the GPIO, however, this has not yet been implemented.

|                                          Raspberry Pi mount                                          |                                              Raspberry Pi in OWL base                                               |
|:----------------------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------------------------:|
| ![RPimount](https://media.github.sydney.edu.au/user/5402/files/263dcf00-cf6a-11eb-9781-1c2d79c9b96d) | ![1T7A9540](https://user-images.githubusercontent.com/40649348/156697656-df60257b-773a-425c-9c56-33f6e48013b5.jpeg) |

### Step 7 - connecting GPIO pins

Connect the Raspberry Pi GPIO to the relay control board header pins, using the table below and the wiring diagram above
as a guide:

The GPIO pins on the Raspberry Pi are not clearly labelled, so use this guide to help. Be careful when connecting these
pins as incorrect wiring can shortcircuit/damage your Pi.
![image](https://user-images.githubusercontent.com/51358498/152514046-37d5bcf5-348b-4e39-8810-c877acfed852.png)

| RPi GPIO pin | Relay header pin |
|:------------:|:----------------:|
|      13      |       IN1        |
|      14      |       COM        |
|      15      |       IN2        |
|      16      |       IN3        |
|      18      |       IN4        |

|                                         Raspberry Pi GPIO pins                                          |                                       Relay control board header pins                                       |
|:-------------------------------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------:|
| ![GPIOtorelay](https://media.github.sydney.edu.au/user/5402/files/6adb7000-d027-11eb-81b9-5fecfe0c2c4e) | ![relayheaderpins](https://media.github.sydney.edu.au/user/5402/files/2bf8ea80-d026-11eb-8c5c-685563db7691) |

![1T7A9541](https://user-images.githubusercontent.com/40649348/156697725-9a99ba10-b79c-4963-ab15-b07bb95c7d3a.jpeg)

### Step 8 - mounting and connecting camera

Connect one end of the CSI ribbon cable to the camera. We provide a mounting plate that can be used with both the HQ, Global Shutter or
V2 cameras, however, we recommend the use of the HQ camera for improved image clarity. Attach the HQ camera to the 3D
printed mount using 2.5 mm standoffs (or 2 mm standoffs if using the V2 camera). Ensuring that the CSI cable port on the
camera is directed towards the Raspberry Pi, mount the camera inside the OWL case using four M3 standoffs (50 mm long
for HQ camera; 20 mm long for V2 camera). Connect the other end of the CSI cable to the Raspberry Pi CSI camera port.

Before connecting the lens, please be aware the HQ camera comes with fitted a C-CS mount adapter which needs to be
removed before fitting the 6mm lens. The image won't focus unless the adapter is removed. More information is available
below and in the [HQ Camera Datasheet](https://datasheets.raspberrypi.com/hq-camera/cs-mount-lens-guide.pdf)

How to remove the C-CS mount adapter:

HQ camera C-CS mount adapter | Camera and adapter separated | Lens fitted without adapter
:-------------: | :-------------: | :-------------:
![adapter1](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/3ab35c57-77c1-4ce0-b627-410a3598db93)|![adapter2](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/7f50e5c8-9dd7-4e29-94d7-8bf8e907e011)|![adapter3](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/322d6409-8509-4895-8896-5959a5f529bc)

Mounting the HQ camera to the 3D printed mount:
HQ camera and mount | HQ camera mounted in case
:-------------: | :-------------:
![1T7A9544](https://user-images.githubusercontent.com/40649348/156695569-ded4679b-f94f-433a-a81f-08a5c409e61c.jpeg) | ![1T7A9545](https://user-images.githubusercontent.com/40649348/156695635-9fd58bb7-303c-4aa8-b5c7-c16b818a51f0.jpeg)

Mounting the V2 camera to the 3D printed mount:
V2 camera and mount | V2 camera mounted in case | Raspberry Pi camera port
:-------------: | :-------------: | :-------------:
![1T7A9558](https://user-images.githubusercontent.com/40649348/156695701-49598e62-fdba-4416-88d1-fbf158fe99ef.jpeg) | ![1T7A9559](https://user-images.githubusercontent.com/40649348/156695786-c34f84e3-26db-4198-80e3-96a5da4b52d3.jpeg) | ![Cameracable](https://media.github.sydney.edu.au/user/5402/files/7ed2a200-d026-11eb-93cb-26a91d727094)

The HQ lens will need to be focused, details below, once the software is correctly set up.

### Step 9 - adding buzzer and LEDs

Mount the buzzer inside the OWL base using double sided mounting tape and connect the 5 V and ground wires to Raspberry
Pi GPIO pins 7 and 9, respectively.

For simplicity we have used two 12V LEDs (which are just normal LEDs with a current limiting resistor included) for both
the 5V TX/GND connection for Raspberry Pi status indication and also the 12V power connection. While 12 V will work fine
on both, the 5 V connection will be dimmer. If you want to use a non-prepackaged, 3 mm LED for the 5V connection, you
should solder a current limiting resistor to the LED to prevent damage to either the LED or the Rasperry Pi as
described [here](https://howchoo.com/g/ytzjyzy4m2e/build-a-simple-raspberry-pi-led-power-status-indicator). Install the
5 V LED inside the OWL base and connect the 5V and ground wire to GPIO pins 8 (TX pin) and 20 (GND pin), respectively.
Install the 12 V LED inside the OWL base and connect the 12 V and GND wires to their respective WAGO terminal blocks.

Buzzer location | LEDs in OWL base | GPIO pins
:-------------: | :-------------: | :-------------:
![1T7A9546](https://user-images.githubusercontent.com/40649348/156696065-177d675e-a0c1-45f8-8e17-acf90ef13314.jpeg) | ![LEDs](https://media.github.sydney.edu.au/user/5402/files/79bc1700-cf82-11eb-80b2-646f2c74fcc9) | ![GPIOpins](https://media.github.sydney.edu.au/user/5402/files/e0474080-d027-11eb-93fd-8c7b7c783eea)

### OPTIONAL STEP - adding real time clock module

Although optional, we recommend that you use a real time clock (RTC) module with the OWL system. This will enable the
Raspberry Pi to hold the correct time when disconnected from power and the internet, and will be useful for debugging
errors if they arise. The RTC uses a CR1220 button cell battery and sits on top of the Raspberry Pi using GPIO pins 1-6.

PiRTC module | RTC installed on Raspberry Pi
:-------------: | :-------------: 
![RTC](https://media.github.sydney.edu.au/user/5402/files/a59bd300-d03c-11eb-847a-d0813f44fcb2) | ![1T7A9550](https://user-images.githubusercontent.com/40649348/156696142-8dd8aaa7-756a-4ff2-a638-7ebfb68165e6.jpeg)

### Step 10 - connecting mounting hardware and OWL cover

There are four 6.5 mm holes on the OWL base for mounting to a boom. Prior to installing the OWL cover, decide on a
mounting solution suitable to your needs. In the photo below, we used 4 x M6 bolts. The cover of the OWL unit is secured
with 4 x M3 nuts and bolts. Place M3 nuts into the slots in the OWL base. This can be fiddly and we suggest using
tweezers, as shown below. Place the cover onto the base and secure using M3 bolts.

Mounting hardware | Cover nuts | Completed OWL unit
:-------------: | :-------------: | :-------------:
![1T7A9551](https://user-images.githubusercontent.com/40649348/156698150-f23571cd-867e-42c7-96ea-125304551d8a.jpeg) | ![1T7A9553](https://user-images.githubusercontent.com/40649348/156698184-464bbded-8e53-4ebc-b6aa-242d8c96ae6e.jpeg) | ![1T7A9554](https://user-images.githubusercontent.com/40649348/156698342-4b3ebba5-337e-469c-bd0e-c34985d57b83.jpeg)

</details>

<details>
<summary> Compact OWL - Hardware Assembly</summary>
<br>

One major benefit of the Compact OWL (with the OWL driver board) is that no soldering is required. The design removes 
much of the wiring, improving ease of assembly and reliability. If you choose a Raspberry Pi Relay HAT instead of the 
OWL driver board, you'll just need to add a voltage regulator and solder that in to provide the 5V @ 5A required for 
the Raspberry Pi 5 or up to 3A required for the older models.

There are two options for the enclosure. The 3D printed enclosure and the official OWL extruded aluminium enclosure. Both share
a 3D printed tray and the same components. The 3D printed version allows you to make a start without needing to buy bespoke
components if you have access to a 3D printer.

The 3D model files for the printed enclosure can be downloaded [here]().

The Official OWL Enclosure will be available for purchase through the OWL store soon.

| Compact OWL - Extruded Aluminium Enclosure                                                                            | Compact OWL - 3D Printed Enclosure                                                                                    |
|-----------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| ![3D Printed OWL](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/a9771aa2-355d-40db-ac15-f6da037b63ed) | ![Extruded OWL](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/d153db2d-624b-427e-832e-599a3a841623) |

**NOTE**: The 3D printed version requires the additional purchase of:
1. [1.6mm](https://au.rs-online.com/web/p/o-ring-cords/1591478) and [3mm](https://au.rs-online.com/web/p/o-ring-cords/1591490) nitrile rubber o-ring cord
2. [M2, M3 and M4 threaded inserts](https://www.amazon.com.au/WEZCHUGHAOL-Threaded-Embedment-Printing-Components/dp/B0CN39ZSC2/ref=sr_1_21_sspa?crid=2R258Z1R9XYJQ&dib=eyJ2IjoiMSJ9.YV_8e4yZB5Up2sxjc6yADA7Nnr7U_kpewviCOxQiUAiT6HPGv5rLlXY1PVeDUBAfmO5LAuekzE8VmOU_0V6pDgL1lOmLjEqU8cGrC2bBxPeu3bDe1ZAScHdT6FLAoWi8i-J9F7nz0hj0S_zyow4N92_ZBdySI1CdG651qgCoF7hC5Av5xYcZBqJ41agRh0WjTmNiIGDV9LRODEPy9hAwFm7tM8XzQpL7jXGtycJNoqOVEEck64araKnzphdkqWC0wKWFVRQOyTKw7LM3TBAsXJPsq83qrBvGJ0vNIgayg2Y.gVKTvrTwcC1PdIZc9g_UckOD3B8z063oPKo9M3o9-Sg&dib_tag=se&keywords=embedded+nuts+threaded&qid=1715135215&sprefix=embedded+nuts+threadd%2Caps%2C385&sr=8-21-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9tdGY&psc=1) + M2, M3 and M4 hex head screws
3. [K&F Concept 37 mm UV lens filter](https://www.amazon.com.au/Concept-18-Layer-Protection-Nanotech-Ultra-Slim/dp/B07NYPCPD5/ref=sr_1_4_sspa?crid=7B57R6GYCCC3&dib=eyJ2IjoiMSJ9.WLMO784g_HVvxPY8RxBi3DdjOJlAw_RRc543yR2qlin4vGGdFusrTxn-OxNr4IQHY_EKtKFwLx9ti6e-ALuUeVuEPGkmCZS7yYe_uisRUN6iDpCOagXAL06Q0aOmh6lWsjS1evk7QMSITdwViuI32n7Ow8KUD6r4Lwm8aun0tsPdBgr3D5Mzo02aGihHL0BmXnmzfR2qbmxQlxaYH-v-IKB2FeQFeMQWt8vFQSe__lSOo3g9ZlSra5mTliSksZh7TLDxBywpR6vOkLD8b1Lxf7ZO__iZLLj9-fmmRJeWQ38.RnnA1gpAajKrN8o4tZgGclc3GRE1tvm50y234Ah4mVE&dib_tag=se&keywords=37mm%2Buv%2Blens%2Bfilter&qid=1715135313&sprefix=37%2Bmm%2BUV%2Bl%2Caps%2C316&sr=8-4-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1)

### Step 1 - enclosure, camera and mounts
The internal tray is the same for both the extruded aluminium or 3D printed enclosures. The 3D printed tray suits the
Raspberry Pi HQ Camera and the Global Shutter Camera. A separate mount is available for the Camera Module 3. Details are
provided below.

Begin camera installation by removing the adapter ring and fitting the lens. The camera will not focus with this 
ring.

| Global Shutter camera with adapter ring atached                                                                                 | Adapter ring removed                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| ![camera_adapter_removal](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/8bd43460-e3de-4978-9eb7-641602024ab9) | ![camera_install](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/f3972dbc-c41a-4d86-83a4-ea237f0fa267) |


Mount the camera to the front of the tray using M2.5 standoffs. The Global Shutter camera requires slightly longer
standoffs to get past the plastic backing cover. Run the ribbon cable over the top of the tray (as pictured)

| Internal tray                                                                                                                 | Mounting the camera                                                                                                           | Mounting the camera                                                                                                           |
|-------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| ![20240502_125849_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/ba347b54-3e51-402a-a9c6-91eb178ac642) | ![20240502_125728_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/7298fc98-96b9-4bf0-8a27-7d74a925298f) | ![20240502_125716_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/730ef3dc-40b8-403a-8045-7b8600478413) |

Once the camera is secured, mount the Raspberry Pi using 4 x M2.5 x 5mm long standoffs. To secure the Pi, use 4 x 15mm 
standoffs. These will be used to mount the HAT.

| Raspberry Pi 4B mounted on tray                                                                                               |
|-------------------------------------------------------------------------------------------------------------------------------|
| ![20240502_125635_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/6605aeaf-174b-4120-beeb-ad40ec189f3f) |

#### 3D printed enclosure
The 37 mm UV lens filter is installed on the faceplate with 8 M2 heat-set threaded inserts and M2 hex head screws. Add
the 1.6mm nitrile rubber o-ring cord to the internal channel on the lens mount. Firmly press the 37 mm UV lens filter into the 
channel on the faceplate.

Tighten down the 8 M2 screws in a cross pattern (similar to how a car tyre is installed), to avoid cracking the 3D printed
mount.

| Faceplate                                                                                                                     | Lens mount                                                                                                              | Lens fitted with o-ring                                                                                                     |
|-------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| ![faceplate_clean_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/43e4d33f-5649-48d7-bdcd-cb4fe766fbe0) | ![lens_cover_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/e32c8b5a-5c4f-4b3d-8206-9665de723f81) | ![faceplate_lens](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/e355db9b-1bdb-4009-afe2-2a6f7ce35461) |

The 3D printed enclosure also supports the mounting of the Camera Module 3 with an extra 3D printed part. Using M2 threaded 
inserts in the faceplate, mount the plate with approx. 5mm long M2 standoffs. Route the camera ribbon cable over the top.

| Camera mounted on backplate                                                                                                   | Faceplate with standoffs and backplate                                                                                        | Assembled                                                                                                                     |
|-------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| ![20240507_095647_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/13deaca2-0e49-4296-a52f-d3de9e280630) | ![20240507_095748_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/828289af-f351-4be2-90f9-46fa3341ffbb) | ![20240507_100004_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/d1852882-f98a-4a28-8431-22f9bcb09bd1) |


### Step 2 - connecting the Official OWL HAT
The OWL Hat simply fits over the GPIO pins and is mounted using the 4 x 15 mm standoffs installed in the previous step.
Secure the HAT with 4 x 2.5mm screws and tighten down.

PWM or GPIO control is selected with four jumper pins (in blue below). 

| Fitted Official OWL HAT                                                                                                  | OWL Hat jumpers                                                                                                               | GPIO pin assignment                                                                                                           |
|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| ![mounted owl hat](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/d080805a-507f-4d9a-a363-25124c52c101) | ![20240502_123112_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/ad1e522f-316b-4bc3-90c7-4415e5608205) | ![20240502_123121_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/8a567873-0c5e-4c46-ba97-c6dbc0a2d352) |

The default option is for GPIO control as pictured. By default the OWL HAT is wired as shown above:

```ini
[Relays]
# defines the relay ID (left) that matches to a boardpin (right) on the Pi.
# Only change if you rewire/change the relay connections.
0 = 13
1 = 15
2 = 16
3 = 18
```
The final jumper pin `Pi Power Supply Enable` connects the Raspberry Pi to the 5V provided by the HAT. Only connect this jumper once you want the 
Pi to start.

#### Step 2a - connecting a generic relay HAT

Instead of the Official OWL HAT, a relay control HAT (such as [this from PiHut](https://core-electronics.com.au/pirelay-v2-relay-board-for-raspberry-pi-1.html?))
can be used, with some minor changes to the OWL software. There are many different relay HATs available, so check which
is most suitable for your purposes. Be sure to choose one with accessible GPIO pins.

Fit the HAT as recommended by the manufacturer, similar to the below images (source: The PiHut).

| HAT | Installed HAT |
|-----|---------------|
| ![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/bf16cf89-0955-4822-8a8a-c3bd7c295c7f)   |    ![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/4c0987a7-936f-4338-ac72-6ee352bc2636)           |

In its default configuration, this specific relay HAT assigns GPIO boardpins 29, 31, 33, and 35 to relays 4 - 1
respectively. This differs to the default OWL configuration, so the `[Relays]` section of the config file would need to
be updated. Using this board as the example:

```ini
[Relays]
# defines the relay ID (left) that matches to a boardpin (right) on the Pi.
# Only change if you rewire/change the relay connections.
0 = 35
1 = 33
2 = 31
3 = 29
```
 However, if you use another relay HAT check the assignment/configuration of relays to boardpins. For reference, use this
 GPIO guide to help.

<p align="center">
<img src="https://user-images.githubusercontent.com/51358498/152514046-37d5bcf5-348b-4e39-8810-c877acfed852.png" width="400">
</p>

#### Step 2b - connecting the voltage regulator
Without the OWL HAT, 5V power to Pi needs to be supplied separately. We recommend the [Pololu 5V 5.5A step down voltage
regulator](https://core-electronics.com.au/pololu-5v-5-5a-step-down-voltage-regulator-d36v50f5.html), however, 
there are many options available.

Solder wires to the input and output of the voltage regulator. Using WAGO connector blocks, connect the input to the 12V
from the Amphenol connector. Mount the regulator to the underside of the internal tray using M2 standoffs.

<p align="center">
<img src="https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/b939e26f-1785-4d4e-8476-ec5721526724" width="400">
</p>

##### Raspberry Pi 3B+ or 4B
The earlier models of the Raspberry Pi consumer less power (3A @ 5V) than the Raspberry Pi 5 and can be powered over single 5V and GND
pins on the GPIO. Use high quality connectors here or consider soldering directly to the GPIO pins on the HAT. A good
connection without risk of coming loose, is critical.

You'll need to solder to pins 2 (5V) and 6 (GND) on the relay HAT. More details provided 
[here](https://thepihut.com/blogs/raspberry-pi-tutorials/how-do-i-power-my-raspberry-pi) from The PiHut (image source).

<p align="center">
<img src="https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/c8eeacde-0e6c-4de2-8120-a343cdcbc756" width="400">
</p>

##### Raspberry Pi 5
The Raspberry Pi 5 consumes up to 5A @ 5V, so it's suggested to use 2 x 5V and 2 x GND pins on the Raspberry Pi.
Some good information on the topic is provided [here](https://forums.raspberrypi.com/viewtopic.php?t=367896).

Using the two 5V outputs from the voltage regulator, solder one +5V wire to pin 2 and another to pin 4 on the GPIO on 
the HAT relay. Similarly, connect two GND wires from the voltage regulator output to pins 30 and 34. Ensure there is a 
good solder connection, without any short circuits to neighbouring pins.

The images below are from a Raspberry Pi 5, however, the setup is the same for the 4B and 3B+ models just with one 5V/GND
wire.

| HAT installation - GPIO                                                                                                      | HAT installation - soldering the 2 x 5V, 2x GND                                                                           | HAT Installation - voltage regulator                                                                                              |
|---------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| ![relay_hat_1_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/dc678435-e59a-44ae-a2d8-4eab43c7797c) | ![relay_hat_2_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/a87a34c6-148e-41c7-b092-e429aa5cb3fd) | ![relay_hat_3_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/e3bb13fa-26f3-42d6-ac21-3862ccfcd701) |

### Step 3 - wiring the connector and HAT
Begin by wiring the [Amphenol EcoMate Aquarius receptacle](https://au.mouser.com/ProductDetail/Amphenol-SINE-Systems/FLS710N3W3S03?qs=ulEaXIWI0c8tWp%252BkBCr3Ag%3D%3D). The connector has 3 x 16 guage connections rated to 13A and 3 x 20 
guage rated up to 7.5A (machined) or 5A (stamped). Use the appropriate crimp connections for the 16 and 20 guage connections. 

<p align="center">
<img src="https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/e6ae15b0-cec5-4295-aa66-dbe5f731cc4b" height="300">
</p>

Connections are labeled A - F on the receptacle and should be made in the following order:

1. +12V (red) - A
2. GND (black) - E
3. relay 1 (blue) - B
4. relay 2 (green) - C
5. relay 3 (orange) - D
6. relay 4 (white) - F

Unlike the relay HATs and relay board in the Original OWL, the common ground for the OWL driver board is routed through 
the board itself, reducing the wiring required. Connect the wires from the back of the connector to each relay, 
using the above list as a guide. The finished result should appear similar to the images below. Add heat shrink at 
the end of each wire for neater and more reliable connections.

| Connector with wires                                                                                                          | Completed HAT                                                                                                                     | Completed HAT mounted on the Pi                                                                                        |
|-------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| ![20240507_160726_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/e225496d-f08b-4304-8239-bcee196a5524) | ![owl_driver_board_install](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/8735a833-f157-456a-a6cd-3dd037ed6e5d) | ![finished_tray](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/50ea79c5-ee7c-4e95-9a46-5f57d773de1b) |

**OPTIONAL** Add a 5V buzzer inside the OWL by mounting it to the corner of the HAT with a screw. Connect the 5 V and ground wires 
to Raspberry Pi GPIO pins 7 and 9, respectively. The buzzer is useful for identifying when the OWL has started successfully.
It isn't essential to operation.

**OPTIONAL** Add Kapton tape to the camera cable and internal wiring. Kapton tape is a god insulator and resistant to high
temperatures, improving the robustness of the device.

| Tray with Kapton tape                                                                                                         |
|-------------------------------------------------------------------------------------------------------------------------------|
| ![finished_tray_kapton](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/3c206482-1d8a-4a78-9963-11f1e4401bf7) |


### Step 4 - inserting the tray and closing the device
**NOTE**: For software installation, you'll need access to the Raspberry Pi display, and USB ports. We recommend you
set up the software prior to completing the build and inserting the tray. Alternatively, flash the SD card with one of 
the provided owl disk images.

To improve the resistance to dust and water ingression on the 3D printed version, you'll need to add a 3mm nitrile rubber 
o-ring around the face- and backplates of the enclosure.

| Faceplate with o-ring                                                                                                    | Backplate with o-ring                                                                                                   |
|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| ![frontplate_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/512e020e-0482-4542-a3a4-25ea811a988d) | ![backplate_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/879c68b3-d379-44b0-8254-3137922bfb5c) |

Fix the faceplate to the enclosure with the 4 x M4 screws. The 3D printed enclosure will need 4 x M4 threaded inserts set
into the plastic on the back and front of the enclosure body. Carefully push the tray into the enclosure on the second row,
making sure wires are not caught up on the side.

<p align="center">
<img src="https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/ddf1d660-feac-4e7c-b4d5-f3a36d464192" width="400">
</p>

For the single Amphenol EcoMate Aquarius receptacle, push it through the backplate and tighten down. Fix the backplate
to the enclosure.

| Front                                                                                                                   | Back                                                                                                                    |
|-------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| ![fron_enclosure](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/c5d8c4d7-21d0-4987-9691-cd9a8615b65a) | ![enclosure_back](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/4ddf0538-265e-4e6b-aebd-040336d1562b) |


There is a choice of three different backplates, depending on your hardware requirements. They include:
1. 1 x hole for the Amphenol EcoMate Aquarius
2. 2 x holes for the Amphenol EcoMate Aquarius and Adafruit waterproof RJ45 (ethernet) connector
3. 1 x 16mm hole for a 16mm cable gland.

If you would prefer a different arrangement, just get in touch or raise an issue and we can sort it out for you!

| Backplate options (aluminium)                                                                                                 | Backplate options (3D printed)                                                                                                |
|-------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| ![20240502_122757_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/07ff7316-0af2-413c-b7ff-a94f678fe8e6) | ![20240503_123813_crop](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/189d9ad1-7734-429e-9ce5-f1c4fdb74ef5) |

And you're all done! Congratulations on building your OWL.

</details>

<details>
<summary> Connecting Solenoids for Spot Spraying</summary>
<br>

### Optional Step - connecting 12V solenoids

Once you have completed the setup, you now have the opportunity to wire up your own solenoids for spot spraying,
targeted tillage, spot flaming or any other targeted weed control you can dream up. To do this, wire the GND wire of
your device (it can be any wire if it's a solenoid) to the ground pin on the Bulgin plug (the same wire used for the GND
from the 12V power source) and wire the other to one of the blue, green, orange or white wires on pins 1 - 4. A wiring
diagram is provided below. The easiest way to wire them together to the same GND wire is to create a six-way harness,
where one end is connected to the plug, one of the five other wires to the source power GND and the remaining four to
the solenoids or whatever devices you are driving.

![solenoid wiring-01](https://user-images.githubusercontent.com/40649348/156698481-3d4fec4e-567a-4a18-b72e-b26d35c8d1c7.png)

Bulgin plug | Ground wiring harness
:-------------: | :-------------:
![Bulginplug](https://media.github.sydney.edu.au/user/5402/files/7f753380-d03a-11eb-8d9b-658db73d3408) | ![Groundharness](https://media.github.sydney.edu.au/user/5402/files/7e440680-d03a-11eb-9af1-67132f4cc36f)

</details>

### SBC Options

A single board computer or SBC is the brains behind the OWL. It can do all the image processing and logic within a
single, roughly credit card sized board without moving parts. These SBCs are the backbone of embedded computing or 'edge
computing'. While the Raspberry Pi is arguably one of the most widely used and well supported SBCs there are many
different options out there. Each has their strengths and weaknesses and may or may not be good fits with the OWL. We've
providing a summary of some SBCs below, but this isn't an exhaustive list.

Currently, only Raspberry Pi 5, 4 and 3B+ work with the OWL and have been tested in full. Early tests (alpha) have been
made with the LibreComputer LePotato. We will update the 'Works with OWL' column as more boards are tested in the
community.

<details>
<summary> A summary of possible single board computers (SBCs) to use with the OWL</summary>
<br>

| Name                                                                                                      | CPU                                                            | RAM   | MIPI | USB          | GPU               | Pros                                                                                                         | Cons                                         | Dimensions        | OWL?                                                                                                 | Image                                                                    |
|-----------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|-------|------|--------------|-------------------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------|-------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| [Raspberry Pi 5](https://datasheets.raspberrypi.com/rpi5/raspberry-pi-5-product-brief.pdf)                | Broadcom BCM2712, quad-core 64-bit ARM Cortex-A76              | 1-8GB | 2    | 2x3.0, 2x2.0 | VideoCore VII     | Large community, affordable, PCIe 2.0 lane for externals (including Google Coral and solid state harddrives) | Limited GPU performance, no eMMC storage     | 88 x 58 x 19.5mm  | :heavy_check_mark:                                                                                   | Manual install only (disk image coming soon)                             |
| [Raspberry Pi 4B](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/)            | Broadcom BCM2711, quad-core Cortex-A72                         | 1-8GB | 2    | 2x3.0, 2x2.0 | VideoCore VI      | Large community, affordable                                                                                  | Limited GPU performance, no eMMC storage     | 88 x 58 x 19.5mm  | :heavy_check_mark:                                                                                   | [OWL v1.0.0](https://www.dropbox.com/s/ad6uieyk3awav9k/owl.img.zip?dl=0) |
| [Raspberry Pi 3B+](https://www.raspberrypi.com/products/raspberry-pi-3-model-b-plus/)                     | Broadcom BCM2837B0, quad-core Cortex-A53                       | 1GB   | 1    | 4x2.0        | VideoCore IV      | Large community, affordable                                                                                  | Limited GPU performance, no eMMC storage     | 85 x 56 x 17mm    | :heavy_check_mark:                                                                                   | [OWL v1.0.0](https://www.dropbox.com/s/ad6uieyk3awav9k/owl.img.zip?dl=0) |
| [Raspberry Pi CM4](https://www.raspberrypi.com/products/compute-module-4/?variant=raspberry-pi-cm4001000) | Broadcom BCM2711 quad-core Cortex-A72                          | 1-8GB | 0    | 0            | VideoCore IV      | Integration into custom carrier boards, EMMC                                                                 | Needs carrier board                          | 55 x 40 x 4.7mm   | -                                                                                                    | -                                                                        |
| [Libre Computer LePotato](https://libre.computer/products/aml-s905x-cc/)                                  | Amlogic S905X                                                  | 1/2GB | 0    | 4x2.0        | Mali-450 @ 750MHz | Affordable                                                                                                   | Limited community support, no onboard Wi-Fi  | 85 x 56mm         | :warning: alpha ([full report here](https://github.com/geezacoleman/OpenWeedLocator/discussions/70)) | TBA                                                                      |
| [Libre Computer Renegade](https://libre.computer/products/roc-rk3328-cc/)                                 | Rockchip RK3328, 4 Core Cortex-A53                             | 1-4GB | 0    | 1x3.0, 2x2.0 | Mali-450 @ 500MHz | 4K HDR support                                                                                               | Limited community support, no onboard Wi-Fi  | 85 x 56mm         | -                                                                                                    | -                                                                        |
| [Libre Computer Renegade Elite](https://libre.computer/products/roc-rk3399-pc/)                           | Rockchip RK3399, 2 Core Cortex-A72 + 4 Core Cortex-A53         | 4GB   | 2    | 4x3.0        | 4 Core Mali-T860  | PCIe, highest performance Libre Computer                                                                     | Higher cost compared to other options        | 128 x 64mm        | -                                                                                                    | -                                                                        |
| [Rock Pi 4B](https://rockpi.org/rockpi4)                                                                  | Rockchip RK3399, 2 Core Cortex-A72 + 4 Core Cortex-A53         | 4GB   | 1    | 2x2.0 2x3.0  | 4 Core Mali-T860  | PCIe, M.2 slot                                                                                               | Limited community support, no onboard Wi-Fi  | 85 x 54mm         | -                                                                                                    | -                                                                        |
| [ODROID-XU4](https://wiki.odroid.com/odroid-xu4/odroid-xu4)                                               | Samsung Exynos5422 ARM Cortex-A15 Quad 2Ghz and Cortex-A7 Octa | 2GB   | 0    | 2x3.0, 1x2.0 | Mali-T628 MP6     | eMMC module support                                                                                          | Higher cost compared to Raspberry Pi options | 83 x 58 x 20mm    | -                                                                                                    | -                                                                        |
| [NVIDIA Jetson Nano](https://developer.nvidia.com/embedded/jetson-nano-developer-kit)                     | 4 Core ARM Cortex-A57                                          | 2/4GB | 2    | 4x3.0        | 128-core Maxwell  | Powerful GPU, CSI camera                                                                                     | Higher cost compared to Raspberry Pi options | 100 x 79 x 30.2mm | -                                                                                                    | -                                                                        |

Only the Raspberry Pi 5 is currently capable of operating on larger image sizes. Frame rates of up to 120 FPS were recorded at the
default 416 x 320 resolution. We recommend increasing resolution to 640 x 480 for the Raspberry Pi 5.

Want to help fill in this table? Find one of the untested platforms and give the OWL a go!

NVIDIA has released numerous powerful, [embedded computers](https://www.nvidia.com/en-us/autonomous-machines/) such as
the Jetson Orin series (and previously the Jetson Xavier NX). These would likely be good options for the OWL, but are
substantially more expensive than the options listed above.

</details>

# Software

The project will eventually support the use of the two major embedded computing devices, the Raspberry Pi (models 3B+, 4 and 5)
and the Jetson Nano/Jetson Xavier NX for possible green-on-green detection with deep learning algorithms. At
present, just the details on setting up the Raspberry Pi 3B+/4/5 are provided below. There are two options for
installation. 

For the first, all you'll need to do is download the disk image file (vX.X.X-owl.img) and flash it to an
SD card. The second method is more in depth, but takes you through the entire process from beginning to end. If you're
looking to learn about how everything works, take some time to work through this process.

**NOTE**: 08/05/2024 - OWL transitioned from `picamera` to `picamera2` support. The v1.0.0 disk image below (Buster) does not
support `picamera2` and will not work on the Raspberry Pi 5 nor with the recent camera releases. We strongly recommend
using the most up to date version of Raspbian with the latest OWL software.

**NOTE**: 17/03/2023 - running of the OWL changed from using `greenonbrown.py` to `owl.py`. This
ensures better cross compatibility with GoG algorithms. It improves the modularity of the system.

## Quick Method
**IMPORTANT**: v1.0.0-owl.img DOES NOT WORK WITH RASPBERRY PI 5.

For this method you'll need access to:

* Desktop/laptop computer
* Micro SD card reader
* Internet with large data capacity and high speed (WARNING: the image file is large, and downloading will take time and
  use up a substantial quantity of your data allowance if you have are on a limited plan)

<details>
<summary><b>Quick method for software installation</b></summary>
<br>

### Step 1 - download the disk image file

Download the entire disk image file (v1.0.0-owl.img)
here: [OWL disk image](https://www.dropbox.com/s/ad6uieyk3awav9k/owl.img.zip?dl=0) (NOT COMPATIBLE WITH RASPBERRY PI 5)

**NOTE** The v1.0.0-owl.img file contains the original software and we strongly recommend updating using the process
below. It also includes the deprecated naming of `greenonbrown.py` instead of `owl.py`. If you do not update the
software, be aware that you will need to run `greenonbrown.py` instead.

The latest, stable version will be linked above, however, all other older versions or versions with features being
tested are available [here](#version-history).

### Step 2 - flash owl.img to SD card

The easiest way to flash (add the vX.X.X-owl.img file to the SD card so it can boot) the SD card is to use Balena Etcher
or any other card flashing software. Instructions for Balena Etcher are provided here. Navigate to
the [website](https://www.balena.io/etcher/) and download the relevant version/operating system. Install Balena Etcher
and fire it up.

![OWL - etcher](https://media.github.sydney.edu.au/user/3859/files/e184ea00-d5a0-11eb-9560-4842758686d0)

* Insert the SD card using your SD card reader.
* Select `Flash from file` on the Balena Etcher window and navigate to where you downloaded the vXX-XX-XX-owl.dmg file.
  This can be a zip file (compressed) too.
* Select the target, the SD card you just inserted.
* Click `Flash`

If this completes successfully, you're ready to move to the next step. If it fails, use Balena Etcher documentation to
diagnose the issue.

### Step 3 - power up

Once the SD card is inserted into the slot of the Raspberry Pi, power everything up and wait for the beep. If you hear
the beep, you're ready to go and start focusing the camera.

### Step 4 - updating the disk image

The disk image that you downloaded is likely to be a few versions behind the most recent. We only provide images of the
most major updates. So to update the OWL software, just run the follow these steps.

1. Have the OWL powered on with screen, keyboard and mouse connected. You should see a desktop with the OWL logo.
2. Press CTRL + ALT + T to open a Terminal window or click the black icon with blue line and >_ symbol.
3. Once the Terminal window is open, make sure you are working in the `owl` virtual environment by running:

```
owl@raspberrypi:~ $ workon owl
(owl) owl@raspberrypi:~ $
```

Notice that (owl) now appears before the line in the Terminal window. This indicates you are in the `owl` virtual
environment. This is **critical** to make sure you install everything in the `requirements.txt` file into the right
spot.

4. Once you are in the `owl` environment, enter these commands on each new line:

```
(owl) owl@raspberrypi:~ $ cd ~
(owl) owl@raspberrypi:~ $ mv owl owl-old      # this renames the old 'owl' folder to 'owl-old'
(owl) owl@raspberrypi:~ $ git clone https://github.com/geezacoleman/OpenWeedLocator        # download the new software
(owl) owl@raspberrypi:~ $ mv OpenWeedLocator owl      # rename the download to 'owl'
(owl) owl@raspberrypi:~ $ cd ~/owl
(owl) owl@raspberrypi:~/owl $ pip install -r requirements.txt                # installs the necessary software into the (owl) environment 
(owl) owl@raspberrypi:~/owl $ chmod a+x owl.py                  # changes owl.py to be executable
(owl) owl@raspberrypi:~/owl $ chmod a+x owl_boot.sh                     # changes owl_boot.sh to be executable
```

Once this is complete your software will be up to date and you can move on to focusing the camera.

### Step 5 - focusing the camera

The final step in the process is to make sure the camera is correctly focused for the mounting height. With the latest
software, when you run `owl.py --focus` a sharpness (i.e. least blurry) estimation is provided on the video feed. The
algorithm determines how sharp an image is, so the higher the value the better. A single script is provided to make
focusing as easy as possible. Simply run:

 ```
(owl) owl@raspberrypi:~ $ cd ~/owl
(owl) owl@raspberrypi:~/owl $ bash focus_owl.sh 
 ```

This will automate all the steps below. If this doesn't work, follow the steps below. If you would like to focus the OWL
again, you can always run `./owl.py --focus`.

| Blurry Image | Clear Image |
|--------------|-------------|
|![blurry owl](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/34ae71f2-8507-4892-b49a-195e515e56dd) | ![clear owl](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/20db536b-edaf-4085-a613-6ea786747998) |

#### Legacy focusing

With the older versions of the software, you need to stop all `owl.py` or `greenonbrown.py` background processes before
you can restart the software with the video feed viewable on the screen. Enter the following into the terminal:

```
(owl) owl@raspberrypi:~ $ ps -C owl.py # or ps -C greenonbrown.py if you still have the older version.
```

After pressing ENTER, you should receive the following output:

```
(owl) owl@raspberrypi:~ $ ps -C owl.py
PID TTY              TIME CMD
515 ?            00:00:00 owl.py
```

The PID is the important part, it's the ID number for the `owl.py` program. In this case it is `515`, but it is likely
to be different on your OWL.

IMPORTANT: If the headings `PID TTY              TIME CMD` appear but a PID/line for owl.py doesn't appear it could mean
two things. Firstly make sure you've typed `owl.py` correctly. If it doesn't have the right program to look for, it
won't find it. The other option is that `owl.py` isn't running, which may also be the case. If you're certain it's not
running in the background, skip the stop program step below, and move straight to launching `owl.py`.

If a PID appears, you'll need to stop it operating. To stop the program, enter the following command:

```
(owl) owl@raspberrypi:~ $ sudo kill enter_your_PID_number_here
```

The program should now be stopped

Now you'll need to launch `owl.py` manually with the video feed visible. To do this use the Terminal window and type the
following commands:

```
(owl) owl@raspberrypi:~ $ ~/owl/./owl.py --show-display
```

This will bring up a video feed you can use to visualise the OWL detector and also use it to focus the camera. Once
you're happy with the focus, press Esc to exit.

### OPTIONAL Step 6 - enabling UART for status LED

This is just the cherry on top and non-essential to correct operation of the OWL but to make sure the status LED you
connected earlier blinks correctly the GPIO UART needs to be enabled.

Open up a terminal console by pressing `Ctrl + T`. Type:

```
(owl) owl@raspberrypi :-$ sudo nano /boot/config.txt
```

This will open up the config.txt file. Scroll down to the bottom by holding the down arrow key and add the following
line to the very last line of the file:

```
enable_uart=1
```

Press `ctrl + x` to exit, then type `y` to save and then `enter`.

You're now ready to run!

### OPTIONAL Step 7 - running original `greenonbrown.py`

If you are using the v1.0.0-owl.img file and don't update the OWL software as above, you will be using the
original `greenonbrown.py` Python script. Running it from the command line will require slightly different commands.
Please follow this guide if this is you.

In the `greenonbrown.py` file there is a parameter `headless` which determines if a video is shown. If set to `True` a
video feed is NOT displayed and the system will operate whenever it is powered on. If it is set to `False` a video feed
will be displayed. To change this parameter, scroll to the bottom of `greenonbrown.py` and find the
line `headless=True`. Change as desired.

**NOTE** `headless` must be set to `True` for operation without a screen. If a screen is not attached
but `headless=False` the Raspberry Pi will not boot correctly and the OWL software will not run.

To run the software from the command line (assuming it is not currently running), follow these steps:

```
owl@raspberrypi:~ $ workon owl
(owl) owl@raspberrypi:~ $ cd owl 
(owl) owl@raspberrypi:~ /owl $ ./greenonbrown.py  
```

**BUG ALERT** There is a known bug with this version where the script will not run if you are running it outside of
the `owl` directory. If you enocunter this error, `cd` into the `owl` directory and run the code again.


</details>  

## Detailed Method
**IMPORTANT**: *Suitable for the Raspberry Pi 5 and Bookworm Raspberry Pi OS.*

This setup approach may take a little longer (aproximately 1 hour total) than the quick method, but you'll be much better
trained in the ways of OWL and more prepared for any problem solving, upgrades or changes in the future. You'll also
download and use the latest software that hasn't been saved in the .img file yet. In the process you'll learn about
Python environments, install Python packages and set it all up to run on startup. To get this working you'll need access
to:

* Raspberry Pi
* Empty SD Card (SanDisk 32GB SDXC ideally)
* Your own computer with SD card reader
* Power supply (if not using the OWL unit)
* Screen and keyboard
* WiFi/Ethernet cable

<details>
<summary><b>Detailed OWL installation procedure</b></summary>
<br>

### Step 1 - Raspberry Pi setup

#### Step 1a - Rasperry Pi OS
Before powering up the Raspberry Pi, you'll need to install the Raspian operating system (just like Windows/MacOSX for
laptops) on the new SD card. This is done using the same process as the quick method used to flash the premade owl.img
file, except you'll be doing it with a completely new and untouched version of Raspbian. 

From your own computer, download and flash the latest **64-bit** version of Raspian from the official 
[Raspberry Pi website](https://www.raspberrypi.com/software/operating-systems/#raspberry-pi-os-64-bit) to the empty SD card. 
The official [Raspberry Pi Imager](https://www.raspberrypi.com/software/) is a good piece of software to use.

Leave the hostname as default. To simplify setup, you can specify the wifi network settings. Set the username to 'owl'
and choose a password.

| Raspberry Pi Imager                                                                                                    | Configuring the OWL                                                                                             |
|-----------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| ![Raspberry Pi Imager](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/a86a6358-3a8c-4f40-94df-9eeba9c17e4d) | ![Imager](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/5f0756e0-52f5-4eb4-8e38-e3ee323cc468) |

#### Step 1b - Setting up the OWL environment
Once the Raspian OS has been flashed to the SD Card (may take 5 - 10 minutes), remove the SD card and insert it into the
Raspberry Pi. Connect the screen, keyboard and mouse and then power up the Pi. 

##### First boot
On the first boot you may be asked to set country, timezone, keyboard, connect to wifi and look for updates among other
things. If you haven't already set the username, set it to 'owl' and choose a password. Uninstall the unused browser - 
this will save space on the Pi. Finally, you will be asked to restart the pi.

##### Opening terminal
After the restart, open up Terminal. You can press CTRL + ALT + T, or click the icon in the top left with the `>_` 
symbol. The instructions that follow are a blend of those available from 
[PyImageSearch](https://pyimagesearch.com/2019/09/16/install-opencv-4-on-raspberry-pi-4-and-raspbian-buster/) 
and [QEngineering](https://qengineering.eu/bookworm.html)

**NOTE:** We recommend naming the device `owl` when asked if you didn't set it during the flashing process. 

##### Free up space
The Raspberry Pi comes pre-installed with a range of software. To free up space it can be removed from the OWL. 
Depending on your install, these may or may not be present. At the command line (it should look like `owl@raspberrypi:~ $`), 
run the following:
```commandline
$ sudo apt-get purge wolfram-engine
$ sudo apt-get purge libreoffice*
$ sudo apt-get clean
$ sudo apt-get autoremove
```
##### Set up the virtual environment
A virtual environment contains all the necessary packages in one neat spot. We'll be using `virtualenv` and 
`virtualenvwrapper` on the Pi to create a virtual environment called `owl`.

To start with, update the system. The update may take a few minutes depending on your internet connection and how many
packages need updating. It's good practice to do this regularly. Then you'll add the following two lines to the `bashrc`
file.

**WARNING** using `rpi-update` will update to the latest kernel and drivers. This is to fix an issue with image component
order. The problem should eventually be merged into normal `apt-get update && upgrade`. This notice will be removed then.

```commandline
$ sudo apt-get update && sudo apt-get upgrade
# update to the latest firmware version
$ sudo rpi-update
$ echo # virtualenv and virtualenvwraper >> ~/.bashrc
# add the following line to the bashrc file
$ echo "export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python" >> ~/.bashrc
# reload the profile
$ source ~/.bashrc
```

Once that is complete, you can install `virtualenv` and `virtualenvwrapper` and add a few more lines to the same `bashrc`
file.
```commandline
$ sudo apt-get install python3-virtualenv
$ sudo apt-get install python3-virtualenvwrapper
$ echo "export WORKON_HOME=$HOME/.virtualenvs" >> ~/.bashrc
$ echo "source /usr/share/virtualenvwrapper/virtualenvwrapper.sh" >> ~/.bashrc
$ source ~/.bashrc
```
With the virtual environment software successfully installed, it's now time to create the `owl` environment. Importantly,
we need to inherit the site-packages (i.e. everything currently on the Pi) because they contain `picamera2` pre-installed.

To make the `owl` environment, run the following:
```commandline
$ mkvirtualenv --system-site-packages -p python owl
```
The command line should now look like `(owl) owl@raspberrypi:~ $`. The '(owl)' at the start of the line means you're currently within
that virtual environment. To turn it off you can run `deactivate` and to turn it run `workon owl`.

**IMPORTANT**: The next steps must be run within the `owl` virtual environment. We're installing packages specific to the OWL.

### Step 2 - Installing packages
We now need to install the Python libraries that let the OWL work. The most import is OpenCV, which we'll do first before
downloading the OWL repository and installing the remainder from the `requirements.txt` file.

```commandline
owl@raspberrypi:~ $ workon owl
(owl) owl@raspberrypi:~ $ pip3 install opencv-contrib-python
```
This should have successfully installed OpenCV into the `owl` virtual environment. You can double check by quickly starting a
Python session at the command line.
```commandline
(owl) owl@raspberrypi:~ $ python
>>> import cv2
>>> import picamera2
>>> exit()
(owl) owl@raspberrypi:~ $
```
If both of these complete without error, then you've successfully set up the virtual environment and installed OpenCV.

### Step 3 - Downloading the 'owl' repository

Now you should have:

* A virtual environment called 'owl'
* A working version of OpenCV installed into that environment
* a Terminal window open with the 'owl' environment activated.

The next step is to download the entire OpenWeedLocator repository into your *home* directory on the Raspberry Pi.

```commandline
(owl) owl@raspberrypi:~ $ cd ~
(owl) owl@raspberrypi:~ $ git clone https://github.com/geezacoleman/OpenWeedLocator owl
```
This will download the repository into a folder called `owl`. Double check it is there by typing `(owl) owl@raspberrypi:~ $ ls` 
and reading through the results, alternatively open up the Home folder using a mouse. If that was successful, you can 
now move on to Step 4.

### Step 4 - Installing the OWL Python dependencies
Dependencies are Python packages on which the code relies to function correctly. With a range of versions and possible
comptibility issues, this is the step where issues might come up. There aren't too many packages, but please make sure
each and every module in the requirements.txt file has been installed correctly. These include:

* OpenCV (should already be in 'owl' virtual environment from Step 1)
* numpy
* imutils
* gpiozero
* pandas
* RPi.GPIO
* tqdm
* blessed (for command line visualisation)
* threading, multiprocessing, collections, queue, time, os (though these are included as standard Python modules).

**IMPORTANT**: Before continuing make sure you are in the `owl` virtual environment. Check that `(owl)` appears at the start
of each command line, e.g. `(owl) owl@raspberrypi:~ $`. Run `workon owl` if you are unsure. If you are not in the `owl`
environment, you will run into errors when starting `owl.py`.

To install all the requirements.txt, simply run:

```commandline
(owl) owl@raspberrypi:~ $ cd ~/owl
(owl) owl@raspberrypi:~/owl $ pip install -r requirements.txt
```
Now to double-check this has worked, we can open up another Python session and try importing the packages.

```commandline
(owl) owl@raspberrypi :~ $ python
```
Python should start up an interactive session; type each of these in and make sure you don't get any errors.

```commandline
>>> import cv2
>>> import numpy
>>> import gpiozero
>>> import pandas
```
Version numbers can be checked with:

```commandline
>>> print(package_name_here.__version__) ## this is a generic example - add the package where it says package_name_here
>>> print(cv2.__version__)
>>> exit()
```
If any errors appear, you'll need to go back and check that the modules above have (1) been installed into the owl
virtual environment, (2) that Python was started in the owl environment, and/or (3) they all installed correctly. Once
that is complete, exit Python and continue with the installation process.

### Step 5 - starting OWL on boot

Now that these dependencies have been installed into the owl virtual environment, it's time to make sure the software 
runs on startup. The first step is to make both the Python file `owl.py` and the boot files `owl_boot.sh` and `owl_boot_wrapper.sh`
executable. Then move both `owl_boot.sh` and `owl_boot_wrapper.sh` into the `/usr/local/bin` directory.

```commandline
(owl) owl@raspberrypi:~/owl $ chmod a+x owl.py
(owl) owl@raspberrypi:~/owl $ chmod a+x owl_boot.sh
(owl) owl@raspberrypi:~/owl $ chmod a+x owl_boot_wrapper.sh
(owl) owl@raspberrypi:~/owl $ sudo mv owl_boot.sh /usr/local/bin/owl_boot.sh
(owl) owl@raspberrypi:~/owl $ sudo mv owl_boot_wrapper.sh /usr/local/bin/owl_boot_wrapper.sh
```

After they have been made executable, the `owl.py` needs to be launched on startup so each time the Raspberry Pi is
powered on, the detection systems starts. The easiest way to do this is by using cron, a scheduler for starting code. 
We need to add the `owl_boot.sh` file to the schedule so that it launches on boot. The `owl_boot.sh` file is 
fairly straightforward. It's what's known as a [bash script](https://ryanstutorials.net/bash-scripting-tutorial/bash-script.php) which is just a text file that
contains commands we would normally enter on the command line in Terminal.

This is the `owl_boot.sh` file:
```commandline
#!/bin/bash

# automatically determine the home directory, to avoid issues with username
source $HOME/.bashrc

# activate the 'owl' virtual environment
source $HOME/.virtualenvs/owl/bin/activate

# change directory to the owl folder
cd $HOME/owl

# run owl.py in the background and save the log output
LOG_DATE=$(date -u +"%Y-%m-%dT%H-%M-%SZ")
./owl.py > $HOME_DIR/owl/logs/owl_$LOG_DATE.log 2>&1 &
```

In the file, the first two commands launch our `owl` virtual environment, then we change directory `cd` into the owl 
folder and run the python program. The `owl_boot_wrapper.sh` file figures out which user is running the file, and then
uses that user to run `owl_boot.sh`. This makes the system more resilient to changes in Pi username.

To add this to the list of cron jobs, you'll need to edit it as a root user:

```
(owl) owl@raspberrypi:~/owl $ sudo crontab -e
```

Select `1. /bin/nano editor`, which should bring up the crontab file. At the base of the file add this text:

```
@reboot /usr/local/bin/owl_boot_wrapper.sh > /home/launch.log 2>&1 
```

Once you've added that line, you'll just need to save the file and exit. In the nano editor just press Ctrl + X, then Y
and finally press Enter to agree to save and exit.

If you get stuck, [this guide](https://www.makeuseof.com/how-to-run-a-raspberry-pi-program-script-at-startup/) or [this guide](https://www.tomshardware.com/how-to/run-script-at-boot-raspberry-pi) both have a bit more detail on cron and some other methods too.

Now you'll just need to reboot the system. Once it reboots, `owl.py` will launch and run in the background.

### Step 6 - focusing the camera

**NOTE**: *Cameras with automatic focus such as the Raspberry Pi Camera Module 3 will be automatically focused to 1.2m 
distance. The following guide is useful for the HQ and Global Shutter cameras which require manual focusing.*

The final step in the process is to make sure the camera is correctly focused for the mounting height. With the latest
software, when you run `owl.py --focus` a sharpness (i.e. least blurry) estimation is provided on the video feed. The
algorithm determines how sharp an image is, so the higher the value the better. A single script is provided to make
focusing as easy as possible. Simply run:

 ```
(owl) owl@raspberrypi:~ $ cd ~/owl
(owl) owl@raspberrypi:~/owl $ bash focus_owl.sh 
 ```

This will automate all the steps below. If this doesn't work, follow the steps below. If you would like to focus the OWL
again, you can always run `./owl.py --focus`.

| Blurry Image | Clear Image |
|--------------|-------------|
|![blurry owl](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/34ae71f2-8507-4892-b49a-195e515e56dd) | ![clear owl](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/20db536b-edaf-4085-a613-6ea786747998) |

#### Legacy focusing

With the older versions of the software, you need to stop all `owl.py` or `greenonbrown.py` background processes before
you can restart the software with the video feed viewable on the screen. Enter the following into the terminal:

```
(owl) owl@raspberrypi:~ $ ps -C owl.py # or ps -C greenonbrown.py if you still have the older version.
```

After pressing ENTER, you should receive the following output:

```
(owl) owl@raspberrypi:~ $ ps -C owl.py
PID TTY              TIME CMD
515 ?            00:00:00 owl.py
```

The PID is the important part, it's the ID number for the `owl.py` program. In this case it is `515`, but it is likely
to be different on your OWL.

IMPORTANT: If the headings `PID TTY              TIME CMD` appear but a PID/line for owl.py doesn't appear it could mean
two things. Firstly make sure you've typed `owl.py` correctly. If it doesn't have the right program to look for, it
won't find it. The other option is that `owl.py` isn't running, which may also be the case. If you're certain it's not
running in the background, skip the stop program step below, and move straight to launching `owl.py`.

If a PID appears, you'll need to stop it operating. To stop the program, enter the following command:

```
(owl) owl@raspberrypi:~ $ sudo kill enter_your_PID_number_here
```

The program should now be stopped

Now you'll need to launch `owl.py` manually with the video feed visible. To do this use the Terminal window and type the
following commands:

```
(owl) owl@raspberrypi:~ $ ~/owl/./owl.py --show-display
```

This will bring up a video feed you can use to visualise the OWL detector and also use it to focus the camera. Once
you're happy with the focus, press Esc to exit.

### Step 8 - reboot

The moment of truth. Shut the Raspberry Pi down and unplug the power. This is where you'll need to reconnect the camera
and all the GPIO pins/power in the OWL unit if they have been disconnected. Once everything is connected again (double
check the camera cable is inserted or this won't work), reconnect the power and wait for a beep!

If you hear a beep, grab something green and move it under the camera. If the relays start clicking (the Official OWL 
HAT uses transistors and will not click - look for the lights) and lights come on, congratulations, you've successfully 
set the OWL up! If not, check the troubleshooting chart below and see if you can get it fixed. Raise an issue and get in touch
if you're not sure how to proceed.

**NOTE** The unit does not perform well under office/artificial lighting. The thresholds have been set for outdoor
conditions.
</details>

<details>
<summary><b>Optional Step - installing RTC and setting the time</b></summary>
<br>
The optional real time clock module can be set up by following the [detailed instructions](https://learn.adafruit.com/adding-a-real-time-clock-to-raspberry-pi/set-up-and-test-i2c) provided by Adafruit. This is a quick process that should take less than 10 minutes. Note that an internet connection is required to set the time initially, however after this the time will be held on the clock module.
</details>

## Changing detection settings
<details>
<summary>Instructions for changing detection settings</summary>
<br>
Changing detection settings is now easier by using a specific config file. 

You can use command line flags to toggle display, data source and setting focus. Use the `config.ini` file in the 
config folder to set other parameters as described below.

The default config file is `DAY_SENSITIVITY_2.ini` (details provided below). If you change any settings here, make sure
to save the file before restarting `owl.py`. 

While we recommend tuning detection parameters to your specific environment, we have provided three sensitivity levels to 
get you started.

| Config File Name      | Description                                                                                                                                          |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| DAY_SENSITIVITY_1.ini | The least sensitive parameters, designed to minimise false positive detections to just get the big weeds. Minimum detection size has been increased. |
| DAY_SENSITIVITY_2.ini | OWL detection parameters were tuned to this file.                                                                                                    |
| DAY_SENSITIVITY_3.ini | The most sensitive parameters. Reduce missed detections with lower minimum detection size and wider detection ranges.                                |


### Command line flags
Command line flags are let you specify options on the command line within the Terminal window. It means you don't have
to open up the code and make changes directly. OWL now supports the use of flags for some parameters. To read a
description of all flags available type `--help`:

```commandline
usage: owl.py [-h] [--input] [--show-display] [--focus]
  --input               path to image directory, single image or video file
  --show-display        show display windows
  --focus               focus the camera
```

### Creating your own config files
Feel free to create your own config files to meet your specific conditions. In `owl.py` just update the path to the
config file. Follow the same layout and format as the default.

To open `owl.py`, you'll need to open it and not execute the file. 

Navigate to the `owl` directory  | Open the `owl.py` file
:-------------------------:|:-------------------------:
![owl_dir](https://user-images.githubusercontent.com/51358498/221152779-46c78fe2-92e6-4e65-9ebd-234ae02c33f6.png) | ![open_greenonbrown_py](https://user-images.githubusercontent.com/51358498/221153072-922d9ed6-8120-4c2d-9bd2-a999030b4723.png)

Then scroll down to the very bottom until you find the line below. Update the `config_file=` path to your own config file path.

```python
owl = Owl(config_file='config/ENTER_YOUR_CONFIG_FILE_HERE.ini')
```

These are the various system, data collection and detection settings that can be changed. They are defined further below.
```ini
[System]
algorithm = exhsv
# operate on a directory, single image or video
input_file_or_directory =
relay_num = 4
actuation_duration = 0.15
delay = 0

[Visualisation]
show_display = False
focus = False
image_loop_time = 5

[Camera]
resolution_width = 416
resolution_height = 320
exp_compensation = -2

[GreenOnGreen]
# parameters related to green-on-green detection
model_path = models
confidence = 0.5
class_filter_id = None

[GreenOnBrown]
# parameters related to green-on-brown detection
exgMin = 25
exgMax = 200
hueMin = 39
hueMax = 83
saturationMin = 50
saturationMax = 220
brightnessMin = 60
brightnessMax = 190
min_detection_area = 10
invert_hue = False

[DataCollection]
# all data collection related parameters
# image collection, sample method include: 'bbox' | 'square' | 'whole'. Set sample_method=None
sample_images = False
sample_method = whole
sample_frequency = 30
# toggle saving to the device or external drives only
enable_device_save = False
save_directory = output
# set to True to disable weed detection for data collection only
disable_detection = False
# enable video recording
recording = False
log_fps = False
camera_name = cam1

[Relays]
# defines the relay ID (left) that matches to a boardpin (right) on the Pi.
# Only change if you rewire/change the relay connections.
0 = 13
1 = 15
2 = 16
3 = 18
```

### Parameter definitions

|       **Parameter**       |                  **Options**                   |                                                                                                                                                                 **Description**                                                                                                                                                                  |
|:-------------------------:|:----------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|        **System**         |                                                |                                                                                                                                                                                                                                                                                                                                                  |
|        `algorithm`        | Any of: `gog`,`exg`,`exgr`,`exgs`,`exhu`,`hsv` | Changes the selected algorithm. Most sensitive: 'exg', least sensitive/most precise (least false positives): 'exgr', 'exhu', 'hsv'. `gog` will activate a provided Green-on-Green detection algorithm, a .tflite model in the models folder. Ensure you have connected and installed a Google Coral using the procedure [here](#green-on-green). |
|   `actuation_duration`    |              Any float (decimal)               |                                                                                                                                           Changes the length of time for which the relay is activated.                                                                                                                                           |
| `input_file_or_directory` |  path to a image, video or directory of media  |                                                                                                                            Will iterate over each image at a default 5 FPS, or over a directory of images or videos.                                                                                                                             |
|        `relay_num`        |                    integer                     |                                         Change the number of activation 'lanes' and therefore the number of relays activated. Set to 1 for a single relay. If <4, then the first boardpins will be used by default. More than four will require additional hardware and changes to the [Relays] mapping.                                         |
|          `delay`          |                   Any float                    |                                                                                                                                              Delay between detection and actuation. Defaults to 0.                                                                                                                                               |
|     **Visualisation**     |                                                |                                                                                                                                                                                                                                                                                                                                                  |
|     `image_loop_time`     |                    Integer                     |                                                                                                              How long (ms) to wait on each image when looping over the same image if a single image file or directory is provided.                                                                                                               |
|        **Camera**         |                                                |                                                                                                                                                                                                                                                                                                                                                  |
|    `resolution_width`     |                    Integer                     |                                                                                                                                                                                                                                                                                                                                                  |
|    `resolution_height`    |                    Integer                     |                                                                                                                                                                                                                                                                                                                                                  |
|    `exp_compensation`     |            Integer between -8 and 8            |                                                                                                      Change the target exposure setting for the exposure algorithm. Defaults to -2, preferencing darker settings for faster shutter speeds.                                                                                                      |
|     **GreenOnGreen**      |                                                |                                                                                                                                                                                                                                                                                                                                                  |
|       `model_path`        |                      Path                      |                                                                                                                                                             A path to the model file                                                                                                                                                             |
|       `confidence`        |                                                |                                                                                                                                       The cutoff confidence value for a detection. Defaults to 0.5 or 50%.                                                                                                                                       |
|     `class_filter_id`     |                    Integer                     |                                                                                      Which classes to filter and target. For example, using a out-the-box COCO model, you may want to only detect a specific class. Enter that specific class integer here.                                                                                      |
|     **GreenOnBrown**      |                                                |                                                                                                                                                                                                                                                                                                                                                  |
|         `exgMin`          |         Any integer between 0 and 255          |                                                                                                           Provides the minimum threshold value for the exg algorithm. Usually leave between 10 (very sensitive) and 25 (not sensitive)                                                                                                           |
|         `exgMax`          |         Any integer between 0 and 255          |                                                                                                                                       Provides a maximum threshold for the exg algorithm. Leave above 180.                                                                                                                                       |
|         `hueMin`          |         Any integer between 0 and 128          |                                                                                                Provides a minimum threshold for the hue channel when using hsv or exhsv algorithms. Typically between 28 and 45. Increase to reduce sensitivity.                                                                                                 |
|         `hueMax`          |         Any integer between 0 and 128          |                                                                                          Provides a maximum threshold for the hue (colour hue) channel when using hsv or exhsv algorithms. Typically between 80 and 95. Decrease to reduce sensitivity.                                                                                          |
|      `saturationMin`      |         Any integer between 0 and 255          |                                                                                    Provides a minimum threshold for the saturation (colour intensity) channel when using hsv or exhsv algorithms. Typically between 4 and 20. Increase to reduce sensitivity.                                                                                    |
|      `saturationMax`      |         Any integer between 0 and 255          |                                                                                  Provides a maximum threshold for the saturation (colour intensity) channel when using hsv or exhsv algorithms. Typically between 200 and 250. Decrease to reduce sensitivity.                                                                                   |
|      `brightnessMin`      |         Any integer between 0 and 255          |                                                                   Provides a minimum threshold for the value (brightness) channel when using hsv or exhsv algorithms. Typically between 10 and 60. Increase to reduce sensitivity particularly if false positives in shadows.                                                                    |
|      `brightnessMax`      |         Any integer between 0 and 255          |                                                                 Provides a maximum threshold for the value (brightness) channel when using hsv or exhsv algorithms. Typically between 190 and 250. Decrease to reduce sensitivity particularly if false positives in bright sun.                                                                 |
|   `min_detection_area`    |                    Integer                     |                                                                                                                                                   The minimum area for which to detect a weed.                                                                                                                                                   |
|       `invert_hue`        |                    Boolean                     |                                                                                                                 True/False, inverts the detected hue from everything within the thresholds to everything outside the thresholds.                                                                                                                 |
|    **DataCollection**     |                                                |                                                                                                                                                                                                                                                                                                                                                  |
|      `sample_images`      |             Boolean: True or False             |                                                                                                                      Enables or disables image data collection. Defaults to False. Set to True to start collecting images.                                                                                                                       |
|      `sample_method`      |     Choose from 'bbox', 'square', 'whole'      |                                                                                                            If sample_method=None, sampling is deactivated. Do not leave on for long periods or SD card will fill up and stop working.                                                                                                            |
|    `sample_frequency`     |              Any positive integer              |                                                                                                          Changes how often (after how many frames) image sampling will occur. If sampleFreq=60, images will be sampled every 60 frames.                                                                                                          |
|    `disable_detection`    |             Boolean: True or False             |                                                                                  Disable detection when running data collection. This will reduce the workload on the Pi and increase frame rate. Useful if using the OWL for dedicated image data collection.                                                                                   |
|     `save_directory`      |             Path to save directory             |                                                                                                            Set where you want the images saved. If you insert a USB and would like to save images to it, put the path for that here.                                                                                                             |
|   `enable_device_save`    |               Boolean: True or False               |                                                                                                  Enable saving to the device itself. This is to avoid accidentally filling the device with collected data when it was intended for a USB drive.                                                                                                  |
|        `recording`        |             Boolean: True or False             |                                                                                                                                                   True/False - turn video recording on or off.                                                                                                                                                   |
|         `log_fps`         |             Boolean: True or False             |                                                                                                                                                               Save FPS to a file.                                                                                                                                                                |
|       `camera_name`       |                   Any string                   |                                                                                                                          Changes the save name if recording videos of the camera. Ignore - only used if recording data.                                                                                                                          |
|        **Relays**         |             Integer/GPIO Boardpin              |                                                                                                                                               Maps a relay number to a boardpin on the GPIO header                                                                                                                                               |

 </details>

## Legacy detection settings

<details>
<summary>Legacy instructions to change detection settings</summary>
<br>
Prior to the `config.ini` file, all settings were controlled using command line flags. These have been replaced, however
are listed below for reference.

### Command line flags

Command line flags are let you specify options on the command line within the Terminal window. It means you don't have
to open up the code and make changes directly. OWL now supports the use of flags for some parameters. To read a
description of all flags available type:

```
(owl) owl@raspberrypi:~ $./owl.py --help
usage: owl.py [-h] [--input] [--show-display] [--focus] [--recording] [--algorithm {exg,nexg,exgr,maxg,exhsv,hsv}] [--framerate [10-120]]
                       [--exposure-mode {off,auto,nightpreview,backlight,spotlight,sports,snow,beach,verylong,fixedfps,antishake,fireworks}]
                       [--awb-mode {off,auto,sunlight,cloudy,shade,tungsten,fluorescent,incandescent,flash,horizon}] [--sensor-mode [0-3]]

optional arguments:
  -h, --help            show this help message and exit
  --input               path to image directory, single image or video file
  --show-display        show display windows
  --focus               focus the camera
  --recording           record video
  --algorithm {exg,nexg,exgr,maxg,exhsv,hsv}
  --framerate [10-120]  set camera framerate between 10 and 120 FPS. Framerate will depend on sensor mode, though setting framerate takes precedence over sensor_mode, For example sensor_mode=0 and framerate=120 will reset the
                        sensor_mode to 3.
  --exp-mode {off,auto,nightpreview,backlight,spotlight,sports,snow,beach,verylong,fixedfps,antishake,fireworks}
                        set exposure mode of camera
  --awb-mode {off,auto,sunlight,cloudy,shade,tungsten,fluorescent,incandescent,flash,horizon}
                        set the auto white balance mode of the camera
  --sensor-mode [0-3]   set the sensor mode for the camera between 0 and 3. Check Raspberry Pi camera documentation for specifics of each mode
  --exp-compensation [-24 to 24]
                        set the exposure compensation (EV) for the camera between -24 and 24. Raspberry Pi cameras seem to overexpose images preferentially.
```

Flag | Usage | Description
:-------------: | :-------------: | :-------------:
--input | Specify the path to an image directory, single image or video file. | Use this if you want to run the software on images or videos. Useful when testing new algorithms or setting up the software without a camera connection.
*legacy* --video-file | NOTE: this has been replaced by `--input` fag. Specify the path to the video file. | This is used when a video file is run instead of the live feed from a camera. It is mostly used in testing new algorithms. If this is not included, a connected camera will be used instead.
--show-display | If flag is present, this will return True | When this flag is included, video feeds and threshold adjustments will appear. Without the flag, the OWL will run `headless` with no display. This flag replaces the `Headless=True` variable in the `owl.py` file.
--focus | If the flag is present, focusing mode is activated. | WHen the flag is included, a Fast Fourier Transform is used to estimate image blurriness. The mean of this value is displayed on the video feed. High values mean it is in focus, low values mean it is blurry. 
--algorithm | gog, exg, nexg, exgr, maxg, exhsv, hsv | Select from the list of algorithms to use. Defaults to `exhsv`. GoG will enable the Google Coral and import 'pycoral' and related libraries. Only use if you have followed the instructions under the [Green-on-Green](#green-on-green) section.
--recording | If flag is present, this will return True | Record video to a file
--framerate | between 10 and 120 FPS, default=40 | sets the framerate for the camera.
--exp-mode | off, auto, nightpreview, backlight, spotlight, sports, snow, beach, verylong, fixedfps, antishake, fireworks | Select from the list of exposure modes available on the [Picamera](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.exposure_mode). Defaults to 'sports' for faster shutter speed.
--awb-mode | off, auto, sunlight, cloudy, shade, tungsten, fluorescent, incandescent, flash, horizon | set the automatic white balance mode from [Picamera options](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.awb_mode).
--sensor-mode | 0: default - automatic; modes 1, 2 and 3 are defined in the picamera documentation. | the sensor mode is specific to the camera. The Raspberry Pi v2 camera has 7 modes, whereas the HQ camera has only 4. Framerate is prioritised over sensor mode. WARNING: high framerates and larger resolutions may 'brick' the SD card. Always backup your SD card before testing new settings, or update from this repository if settings are lost.
--exp-compensation | Default: -4, use even values between between -24 and 24. | This sets the target brightness level for the camera. Typically it defaults to being overexposed in bright sun conditions so lower values will improve performance.

### Changing threshold values in `owl.py`

Other parameters such as selecting or modifying sensitivity settings can be adjusted in the owl.py file itself.

To edit this file, connect a screen, keyboard and mouse and boot up the OWL. Navigate to the `owl` directory and open
up `greenonbrown.py` in an editor. If it's an executable file, it will ask you if you want to "Execute", "Execute in
Terminal" or "Open" (see image below). Make sure to select the `Open` option.

Navigate to the `owl` directory  | Open the `owl.py` file
:-------------------------:|:-------------------------:
![owl_dir](https://user-images.githubusercontent.com/51358498/221152779-46c78fe2-92e6-4e65-9ebd-234ae02c33f6.png) | ![open_greenonbrown_py](https://user-images.githubusercontent.com/51358498/221153072-922d9ed6-8120-4c2d-9bd2-a999030b4723.png)

Once you have opened the file in an editor (this can be a text editor, Thonny, Geany or other code editors), scroll down
to the very bottom and you should come across values you can change, such as in the image or written out below.

![image](https://user-images.githubusercontent.com/51358498/221154007-69007ab9-e1b9-4c2f-84dd-efe6b17ff3ca.png)

Editable values for sensitivity:

```
if __name__ == "__main__":
    owl = Owl(input_file_or_directory=args.input,
              show_display=args.show_display,
              focus=args.focus,
              recording=args.recording,
              exgMin=25,
              exgMax=200,
              hueMin=39,
              hueMax=83,
              saturationMin=50,
              saturationMax=220,
              brightnessMin=60,
              brightnessMax=190,
              framerate=args.framerate,
              resolution=(416, 320),
              exposure_mode=args.exposure_mode,
              awb_mode=args.awb_mode,
              sensor_mode=args.sensor_mode)

    # start the targeting!
    owl.hoot(sprayDur=0.15,
             delay=0,
             sampleMethod=None,
             sampleFreq=60,
             saveDir='/home/owl/owl-images',
             algorithm=args.algorithm,
             selectorEnabled=False,
             camera_name='hsv',
             minArea=10)
```

Here's a summary table of what each parameter does. Run `./owl.py --show-display` to view the output results. Without
this `--show-display` flag the video will not appear on the screen.

**NOTE** In older versions ONLY, ff you change the now defunct parameter of `headless` to `False`, you'll be able to see
a real time feed of what the algorithm is doing and where the detections are occurring. This will need to be switched
back to `headless=True` if you decide to run it without the screen connected. Note that the owl program will not run on
startup if `headless=False`.

**Parameter**  | **Options** | **Description** 
:-------------: | :-------------: | :-------------: 
**Owl()** | | All options when the sprayer class is instantiated
`exgMin`|Any integer between 0 and 255| Provides the minimum threshold value for the exg algorithm. Usually leave between 10 (very sensitive) and 25 (not sensitive)
`exgMax`|Any integer between 0 and 255| Provides a maximum threshold for the exg algorithm. Leave above 180. 
`hueMin`|Any integer between 0 and 128| Provides a minimum threshold for the hue channel when using hsv or exhsv algorithms. Typically between 28 and 45. Increase to reduce sensitivity.
`hueMax`|Any integer between 0 and 128| Provides a maximum threshold for the hue (colour hue) channel when using hsv or exhsv algorithms. Typically between 80 and 95. Decrease to reduce sensitivity.
`saturationMin`|Any integer between 0 and 255| Provides a minimum threshold for the saturation (colour intensity) channel when using hsv or exhsv algorithms. Typically between 4 and 20. Increase to reduce sensitivity.
`saturationMax`|Any integer between 0 and 255| Provides a maximum threshold for the saturation (colour intensity) channel when using hsv or exhsv algorithms. Typically between 200 and 250. Decrease to reduce sensitivity.
`brightnessMin`|Any integer between 0 and 255| Provides a minimum threshold for the value (brightness) channel when using hsv or exhsv algorithms. Typically between 10 and 60. Increase to reduce sensitivity particularly if false positives in shadows.
`brightnessMax`|Any integer between 0 and 255| Provides a maximum threshold for the value (brightness) channel when using hsv or exhsv algorithms. Typically between 190 and 250. Decrease to reduce sensitivity particularly if false positives in bright sun.
`resolution`|Tuple of (w, h) resolution| Changes output resolution from camera. Increasing rapidly decreased framerate but improves detection of small weeds.
**hoot()** | | All options when the sprayer.start() function is called
`sprayDur`|Any float (decimal)|Changes the length of time for which the relay is activated.|
`sampleMethod`|Choose from None, 'bbox', 'square', 'whole' | If sampleMethod=None, sampling is deactivated. Do not leave on for long periods or SD card will fill up and stop working.|
`sampleFreq` | Any positive integer | Changes how often (after how many frames) image sampling will occur. If sampleFreq=60, images will be sampled every 60 frames. |
`saveDir` | Path to save directory | Set where you want the images saved. If you insert a USB and would like to save images to it, put the path for that here. |
`algorithm`|Any of: `gog`,`exg`,`exgr`,`exgs`,`exhu`,`hsv`| Changes the selected algorithm. Most sensitive: 'exg', least sensitive/most precise (least false positives): 'exgr', 'exhu', 'hsv'. `gog` will activate a provided Green-on-Green detection algorithm, a .tflite model in the models folder. Ensure you have connected and installed a Google Coral using the procedure [here](#green-on-green). |
`selectorEnabled`|`True` or `False`| Enables algorithm selection based on a rotary switch. Only enable if switch is connected.|
`cameraName` | Any string | Changes the save name if recording videos of the camera. Ignore - only used if recording data.|
`minArea`| Any integer  | Changes the minimum size of the detection. Leave low for more sensitivity of small weeds and increase to reduce false positives.|

 </details>

## Green-on-Green

<details>
<summary>How to detect in-crop weeds with the OWL</summary>
<br>

### OWL Integration

Green-on-Green capability is here!

Deep learning object detection algorithms for in-crop or 'Green-on-Green' (GoG) require much more processing power than
the green detection algorithms we have used previously. If we ran these GoG algorithms directly on the Raspberry Pi, the
frame rate would be prohibitively slow. To overcome this, you can use more powerful computers with GPUs (i.e. any of
NVIDIA's Jetson series), alternatively you can connect a third party processor such as Google Coral's TPU through the
USB3.0 ports of the Raspberry Pi 4. This means increased performance without needing to purchase another embedded
computer.

The [Google Coral USB accelerator](https://coral.ai/products/accelerator) is only $59.99, so it provides performance
upgrades without substantial cost increases. With the added hardware, there are some additional software installation
details that you should follow. And you will need to connect the Google Coral to the Raspberry Pi USB3.0 port too. At
the moment, this won't fit neatly in the case, but we are continuing to work on improving this.

For all the details on how to install the Google Coral, please head over to the `models` directory. We have provided an
installation script to make it as straightforward as possible.

### Model Training

Effective models need training data, so if you're interested in using the Green-on-Green functionality, you will need to
start collecting and annotating images of relevant weeds for training. Alternatively, head over
to [Weed-AI](https://weed-ai.sydney.edu.au/explore?is_head_filter=%5B%22latest+version%22%5D) to see if any image data
may be relevant for your purposes.

**NOTE** There do appear to be some issues with the exporting functionality of YOLOv5/v8 to .tflite models for use with
the Coral. The issue has been raised on the Ultralytics repository and should hopefully be resolved soon. You can follow
the updates [here](https://github.com/ultralytics/ultralytics/issues/1312).

[YOLOv8](https://github.com/ultralytics/ultralytics) and [YOLOv5](https://github.com/ultralytics/yolov5) currently
provide the most user friendly methods of training, optimisation and exporting as `.tflite` files for use with the
Google Coral. There is also a Weed-AI Google Colab
Notebook <a target="_blank" href="https://colab.research.google.com/github/Weed-AI/Weed-AI/blob/master/weed_ai_yolov5.ipynb">
<img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>
which can be used to train models from Weed-AI data directly.

</details>

## Non-Raspberry Pi Installation

<details>
<summary>Installing OWL software on a non-Raspberry Pi system</summary>
<br>
Using OWL software on your laptop/desktop or other non-Raspberry Pi system is a great way to test, develop and learn more about how it works. To start using the software, just follow the steps below. You will need access to virtual environments and your IDE/editor of choice. This method has been successfully tested on PyCharm with Anaconda environments.

```
> git clone https://github.com/geezacoleman/OpenWeedLocator
> cd OpenWeedLocator
```

For the next part, make sure you are in the virtual environment you will be working from. If you're unsure about virtual
environments, read
through [this PyImageSearch blog](https://pyimagesearch.com/2017/09/25/configuring-ubuntu-for-deep-learning-with-python/)
on configuring an Ubuntu environment for deep learning - just skip to the virtual environment
step. [FreeCodeCamp](https://www.freecodecamp.org/news/how-to-setup-virtual-environments-in-python/) has a great blog
describing them too.

Assuming the virtual environment is working and is activated, run through these next couple of steps:

```
> pip install -r non_rpi_requirements.txt     # this will install all the necessary packages, without including the Raspberry Pi specific ones.
```

It may take a minute or two for those to complete installing. But once they are done you are free to run the `owl.py`
software.

```
> python owl.py --show-display
```

From there you can change the command line flags (as described above) or play around with the settings to see how it
works.
</details>

# Image Processing

<details>
<summary>Image processing details and in-field results</summary>
<br>
So how does OWL actually detect the weeds and trigger the relay control board? It all starts by taking in the colour image from the camera using OpenCV and splitting it into its component channels: Red (R), Green (G) and Blue (B) (RGB) or loading and converting into the hue, saturation and value (HSV) colourspace. Following that, computer vision algorithms such as Excess Green `ExG = 2 * G - R - B` or thresholding type approaches on the HSV colourspace can be used to differentiate green locations from the background. 

![image](https://user-images.githubusercontent.com/51358498/152990324-d315672c-fb4b-42d2-b4df-363f702c473d.png)

Once the green locations are identified and a binary (purely black/white) mask generated, a contouring process is run to
outline each detection. If the detection pixel area is greater than the minimum area set in `minArea=10`, the central
pixel coordinates of that area are related to an activation zone. That zone is connected to a specific GPIO pin on the
Raspberry Pi, itself connected to a specific channel on the relay (one of IN1-4). When the GPIO pin is driven high (
activated) the relay switches and connects the solenoid for example to 12V and activates the solenoid. It's all
summarised below.

![OWL - workflow](https://user-images.githubusercontent.com/51358498/152990264-ddce7eb4-0e2e-4f98-ac77-bc2e535c5c54.png)

## Results

The performance of each algorithm on 7 different day/night fields is outlined below. The boxplot shows the range,
interquartile range and median performance for each algorithm. Whilst there were no significant differences (P > 0.05)
for the recall (how many weeds were detected of all weeds present) and precision (how many detections were actually
weeds), trends indicated the ExHSV algorithm was less sensitive (fewer false detections) and more precise, but did miss
more smaller/discoloured weeds compared to ExG.

![results boxplot](https://user-images.githubusercontent.com/51358498/152990178-a53256c0-cfda-46d3-83c8-3ae018b4a40e.png)

The image below gives a better indication of the types of weeds that were detected/missed by the ExHSV algorithm. Large,
green weeds were consistently found, but small discoloured or grasses with thin leaves that blurred into the background
were missed. Faster shutter speed would help improve this performance.

![detection results resized](https://user-images.githubusercontent.com/51358498/152989906-bcc47ad5-360a-414c-8e25-d9b99875f361.png)

</details>

# 3D Printing

<details>
<summary>3D printing instructions and files</summary>
<br>

## Original OWL
There are seven total items that need printing for the Original OWL unit. All items with links to the STL files are 
listed below. There are two options for Original OWL base:

1. Single connector (Bulgin) panel mount
    - Pros: of this method are easy/quick attach/detach from whatever you have connected, more water resistant.
    - Cons: more connections to make, more expensive
2. Cable gland
    - Pros: fewer connections to make, cheaper, faster to build.
    - Cons: more difficult to remove, less water resistant.

We also provide a link to the [3D models on TinkerCAD](https://www.tinkercad.com/things/fhfUCsPEn5q), an online and free
3D modelling software package, allowing for further customisation to cater for individual user needs.

|                                                     Description                                                     |                                                                                                               Image (click for link)                                                                                                                |
|:-------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|                                                  **Original OWL**                                                   |                                                                                                                                                                                                                                                     |
| OWL base, onto which all components are mounted. The unit can be fitted using the M6 bolt holes on the rear panel.  | [![screenshot](https://user-images.githubusercontent.com/51358498/166176068-989cc69b-43c1-48ef-942d-b273fc2f4d98.png)](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Enclosure%20-%20single%20connector.stl) |
|                      OPTIONAL: OWL base with cable glands instead of single Bulgin connector.                       |   [![screenshot](https://user-images.githubusercontent.com/51358498/166175980-e1fcc526-c835-4ea1-88b5-d28a1ab747b7.png)](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Enclosure%20-%20cable%20gland.stl)    |
|       OWL cover, slides over the base and is fitted with 4 x M3 bolts/nuts. Provides basic splash protection.       |      [![OWL Cover](https://user-images.githubusercontent.com/51358498/132754464-8bfe62aa-4487-42ea-a507-71e0b4a4d1a2.png)](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Tall%20enclosure%20cover.stl)       |
|                            OWL base port cover, covers the cable port on the rear panel.                            |         [![OWL base port cover](https://media.github.sydney.edu.au/user/3859/files/12b7f000-cb87-11eb-980b-564e7b4324f6)](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Tall%20enclosure%20plug.stl)         |
|                   Raspberry Pi mount, fixes to the Raspberry Pi for easy attachment to OWL base.                    |          [![Raspberry Pi mount](https://media.github.sydney.edu.au/user/3859/files/5d396c80-cb87-11eb-948c-d60efe433ac8)](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Raspberry%20Pi%20mount.stl)          |
|             Raspberry Pi Camera mount, fixes to the HQ or V2 Camera for simple attachment to the base.              |  [![Screenshot 2022-03-04 180036](https://user-images.githubusercontent.com/40649348/156715282-bea91301-ac6d-4421-b071-4a4304eb02b0.png)](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Camera%20mount.stl)  |
|                   Relay board mount, fixes to the relay board for simple attachment to the base.                    |      [![Relay board mount](https://media.github.sydney.edu.au/user/5402/files/d421aa00-d04c-11eb-9191-bcad7b51c1a4)](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Relay%20control%20board%20mount.stl)      |
| Voltage regulator mount, fixes to the voltage regulator and onto the relay board for simple attachment to the base. |     [![Voltage regulator mount](https://media.github.sydney.edu.au/user/5402/files/8147f280-d04c-11eb-89ec-4af125a8f232)](https://github.com/geezacoleman/OpenWeedLocator/blob/main/3D%20Models/Original%20OWL/Voltage%20regulator%20mount.stl)     |

Ideally supports should be used for the base, and were tested at 0.2mm layer heights with 25% infill on a Prusa MK3S.

**Update 02/05/2022**

* improved camera mounts
* space for 40mm lens cover
* more compact design
* version tracking
* 
## Compact OWL
The Compact OWL has fewer parts to print than the Original OWL and is both more durable and water resistant. A complete
unit requires printing of only 5 parts.

All 3D model files are availabe on to edit and download on [TinkerCAD](https://www.tinkercad.com/things/id1FMJrWtJp-compact-owl) or [Printables](https://www.printables.com/model/875853-raspberry-pi-rugged-imaging-enclosure). 
The 3D printing .stl files are provided under the 3D Models and through the links in the table below.

The backplate comes in three options:
1. Amphenol EcoMate Aquarius receptacle only
2. Amphenol EcoMate Aquarius receptacle + Adafruit RJ45 waterproof ethernet connector
3. 16mm cable gland only

Pick one of these backplates when printing.

|                                                     Description                                                     |                                                                                                               Image (click for link)                                                                                                             |
|:-------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|                                                   **Compact OWL**                                                   |                                                                                                                                                                                                                                                     |
|                                    Enclosure body: houses all components on tray                                    |                                                                 [![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/dc5d4a38-3a76-42b6-bb2b-96e6cae29a8e)]()                                                                  |
|        Frontplate: covers the front of the enclosure. Incorporates a 37 mm lens cover to seal the enclosure.        |                                                                                                                        [![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/54113656-8688-4c58-a6b6-dfd3b35736b9)]()                                                                                                                         |
|                       Lens mount: Securely mounts the 37 mm UV lens filter to the frontplate.                       |                                                                                                                        [![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/b5c9e4a7-5bd9-4c22-8d42-8134f0f96f6f)]()                                                                                                                         |
|                                 Backplate: 1 x Amphenol EcoMate Aquarius Receptacle                                 |                                                                 [![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/a80eb501-f681-4298-a6e1-2fb1595a859a)]()                                                                  |
|                Backplate: 1 x Amphenol EcoMate Aquarius Receptacle, 1 x Adafruit Ethernet Connector                 |                                                                 [![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/4424e47e-f92c-4db2-b20f-26daec9babe0)]()                                                                  |
|                Backplate: blank                 |                                                                 [![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/f724822e-be85-47ee-9ab8-968efd161124)]()                                                                  |
|                                           Backplate: 1 x 16mm Cable Gland                                           |                                                                 [![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/1f318499-fe28-4b97-9e7f-57c53fac8173)]()                                                                  |
|               Tray: Mounts all required hardware and fits into the enclosure body on the second rail. Use M2 heat-set threaded inserts for the lens holder.               |                                                                 [![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/83c7d31d-1b93-4d04-8cff-349998394b2a)]()                                                                  |
|               Lens holder: Secures the lens with two M2 x 6mm screws.               |                                                                 [![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/25a44e01-18cc-44de-a36b-b396d1216653)]()                                                                  |
|                                 OPTIONAL: Camera Module 3/V2 Camera mounting plate                                  |                                                                 [![image](https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/38baf7e4-b05a-48e7-958e-9e8374bc8990)]()                                                                  |

All .stl files for the 3D printed components of this build are available in the 3D Models directory.
Supports are not required but do improve print quality. All parts were printed with a Bambu Labs P1S at 0.16mm layer height
at 25% infill.

</details>

# Updating OWL

<details>
<summary>Updating OWL software</summary>
<br>

We and others will be continually contributing to and improving OWL as we become aware of issues or opportunities to
increase detection performance. Once you have a functioning setup the process to update is simple. First, you'll need to
connect a screen, keyboard and mouse to the OWL unit and boot it up. Navigate to the existing owl directory
in `/home/owl/` and either delete or rename that folder. Remember if you've made any of your own changes to the
parameters/code, write them down. Then open up a Terminal window (Ctrl + T) and follow these steps:

**IMPORTANT**: Before continuing make sure you are in the `owl` virtual environment. Check that `(owl)` appears at the
start of each command line, e.g. `(owl) owl@raspberrypi:~ $`. Run `workon owl` if you are unsure. If you are not in
the `owl` environment, you will run into errors when starting `owl.py`.

```
(owl) owl@raspberrypi:~ $ cd ~
(owl) owl@raspberrypi:~ $ mv owl owl-old      # this renames the old 'owl' folder to 'owl-old'
(owl) owl@raspberrypi:~ $ git clone https://github.com/geezacoleman/OpenWeedLocator        # download the new software
(owl) owl@raspberrypi:~ $ mv OpenWeedLocator owl      # rename the download to 'owl'
(owl) owl@raspberrypi:~ $ cd ~/owl
(owl) owl@raspberrypi:~/owl $ pip install -r requirements.txt
(owl) owl@raspberrypi:~/owl $ chmod a+x owl.py
(owl) owl@raspberrypi:~/owl $ chmod a+x owl_boot.sh
```

And that's it! You're good to go with the latest software.

If you have multiple units running, the most efficient method is to update one and then copy the SD card disk image to
every other unit. Follow these instructions here. ADD INSTRUCTIONS

## Version History

All versions of OWL can be found here. Only major changes will be recorded as separate disk images for use.

|     Version     |                                  File                                  |       Raspbian       |
|:---------------:|:----------------------------------------------------------------------:|:--------------------:|
| v1.0.0-owl.img  | [Download](https://www.dropbox.com/s/ad6uieyk3awav9k/owl.img.zip?dl=0) |  Buster (picamera)   |
| v2.0.0-owl.img  |                              [Download]()                              | Bookworm (picamera2) |

</details>

# Troubleshooting

<details>
<summary>Troubleshooting OWL issues</summary>
<br>


Here's a table of some of the common symptoms and possible explanations for errors we've come across. This is by no
means exhaustive, but hopefully helps in diagnosing any issues you might have. If you come across any others please
contact us so we can improve the software, hardware and guide.

**NOTE** If you are using the original disk image without updating, there are a number of issues that will appear. We
recommend updating to the latest software by following the procedure detailed in the [Updating OWL](#updating-owl)
section above.

|                           Symptom                           |                                             Explanation                                              |                                                                                                                                                     Possible solution                                                                                                                                                        |
|:-----------------------------------------------------------:|:----------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|   Raspberry Pi won't start (no green/red lights)            |                                  No power getting to the computer                                    |                                                     Check the power source, and all downstream components. Such as Bulgin panel/plug connections fuse connections and fuse, connections to Wago 2-way block, voltage regulator connections, cable into the Raspberry Pi.                                                     |
|   Raspberry Pi starts (green light flashing) but no beep    |                                     OWL software has not started                                     |                      This is likely a configuration/camera connection error with many possible causes. To get more information, boot the Raspberry Pi with a screen connected, open up a Terminal window (Ctrl + T) and type `~/owl/./owl.py`. This will run the program. Check any errors that emerge.                      |
| Beep heard, but no relays activating when tested with green | Relays are not receiving (1) 12V power, (2) a signal from the Pi, (3) the Pi is not sending a signal | Check all your connections with a multimeter if necessary for the presence of 12V. Make sure everything is connected as per the wiring diagram. If you're confident there are no connection issues, open up a Terminal window (Ctrl + T) and type `~/owl/./owl.py`. This will run the program. Check any errors that emerge. |

</details>

# Citing OWL

<details>
<summary>Citing OWL</summary>
<br>

OpenWeedLocator has been published in [Scientific Reports](https://www.nature.com/articles/s41598-021-03858-9). Please
consider citing the published article using the details below.

```
@article{Coleman2022,
author = {Coleman, Guy and Salter, William and Walsh, Michael},
doi = {10.1038/s41598-021-03858-9},
issn = {2045-2322},
journal = {Scientific Reports},
number = {1},
pages = {170},
title = {{OpenWeedLocator (OWL): an open-source, low-cost device for fallow weed detection}},
url = {https://doi.org/10.1038/s41598-021-03858-9},
volume = {12},
year = {2022}
}

```

</details>

# Acknowledgements

<details>
<summary>Acknowledgements</summary>
<br>

This project has been developed by Guy Coleman and William Salter at the University of Sydney, Precision Weed Control
Lab. It was supported and funded by the Grains Research and Development Corporation (GRDC) and Landcare Australia as
part of the University of Sydney's Digifarm project in Narrabri, NSW, Australia. We would like to thank all the farmers
that assisted in data collection, validation and feedback on the initial design.

</details>

# Disclaimer and License

<details>
<summary>Disclaimer and License</summary>
<br>

While every effort has been made in the development of this guide to cover critical details, it is not an exhaustive nor
perfectly complete set of instructions. It is important that people using this guide take all due care in assembly to
avoid damage, loss of components and personal injury, and are supervised by someone experienced if necessary. Assembly
and use of OWL is entirely at your own risk and the license expressly states there is no warranty.

```
MIT License

Copyright (c) 2020 Guy Coleman

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

</details>

# References

<details>
<summary>References</summary>
<br>

**Journal Papers**
Woebbecke, D. M., Meyer, G. E., Von Bargen, K., Mortensen, D. A., Bargen, K. Von, and Mortensen, D. A. (1995). Color
Indices for Weed Identification Under Various Soil, Residue, and Lighting Conditions. Trans. ASAE 38, 259–269.
doi:https://doi.org/10.13031/2013.27838.

**Blog Posts**
[How to run a Raspberry Pi script at startup](https://www.makeuseof.com/how-to-run-a-raspberry-pi-program-script-at-startup/)

[How to Run a Script at Boot on Raspberry Pi (with cron)](https://www.tomshardware.com/how-to/run-script-at-boot-raspberry-pi)

[Install OpenCV 4 on Raspberry Pi 4 and Raspbian Buster](https://www.pyimagesearch.com/2019/09/16/install-opencv-4-on-raspberry-pi-4-and-raspbian-buster/)

[How to solder](https://www.makerspaces.com/how-to-solder/)

</details>

# Repository Stats

### Star History

[![Star History Chart](https://api.star-history.com/svg?repos=geezacoleman/OpenWeedLocator&type=Timeline)](https://star-history.com/#geezacoleman/OpenWeedLocator&Timeline)

