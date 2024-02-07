# UMEB Software Projects

## Overview

Main software projects on the University of Michigan Electric Boat team:
* [VCU programming](#vcu-programming)
  * [Programming Environment Overview](#programming-environment-overview)
  * [Making the CAN DBC Files: Kvaser Database Editor](#making-the-can-dbc-files-kvaser-database-editor)
  * [Programming the VCU: MATLAB Simulink + Raptor Toolkit](#programming-the-vcu-matlab-simulink-and-raptor-toolkit)
  * [Debugging](#debugging)
* [Driver display](#driver-display)
* Website development (HTML/CSS, Javascript)
* Debug display*
* Shore display*
* Data analytics*

Projects marked with an asterisk are not yet started.

### Contact Information

Questions? Please contact these team members:
* Megan Miller (megmil), Software Lead
* Michael Sharashenidze (msharash), Electrical Lead
* Adam Lake (adamlake), Controls Lead

### Electrical System Block Diagram

Below is an image of the current system block diagram (source: [Lucidchart](https://lucid.app/lucidchart/c0bbbfa5-0525-45ad-8ec3-776604d7f318/edit?invitationId=inv_6c9863e5-fb13-4fd6-8d17-4680908d763c&page=0_0#)):

<img src="https://github.com/uofmelectricboat/.github/assets/101139170/32fef8ed-8dbb-4f66-82f4-b4bcb79485ca" alt="drawing" width="350"/>

For more details or access to the Lucidchart file, contact the Electrical Lead.

## VCU Programming

The Vehicle Control Unit (VCU) is essentially the central processing unit of the boat. It activates electrical components, records important data, and controls elements like sensors and actuators. It also serves as the central communication hub between different parts of the boat via the Controller Area Network (CAN) bus, a vehicle bus standard that allows microcontrollers and devices on the boat to communicate with each other without a host computer.

We use the [Raptor General Control Model GCM48](https://store.neweagle.net/shop/raptor/raptor-hardware/raptor-controllers-with-software/raptor-general-control-module-gcm48-2/) as our VCU. Note that you need a New Eagle account (which takes a few business days to get approved) to view the documentation on the New Eagle / New Eagle Wiki site.

### Programming Environment Overview

The electronic hardware components on our boat (like sensors and actuators) are programmed using software provided by New Eagle. We have free access to New Eagle’s Raptor Toolkit (i.e. Raptor-Dev and Raptor Cal) ($9600 worth of software!) due to our use of the Raptor GCM.

Typically, we would program our electronic hardware using languages like C or Python to implement low-level driver code provided by manufacturers. The Raptor Toolkit simplifies this process, allowing us to use MATLAB Simulink (supplemented with additional Raptor libraries) to program the VCU. Additionally, we use Vector CANalyzer software to program the CAN bus and Kvaser Database Editor to create the DBC files.

#### Getting Started: Setup Guide & Platform Compatibility

See the software setup guide [here](https://docs.google.com/document/d/1cnFTK1jpPUwSgk5_LYbEjfsr6MsOQiAcEhOZyKOdtkA). Please note that all Raptor tools are only compatible with Windows. For Mac users who wish to view and operate the Raptor software, we recommend using CAEN computers.

### Making the CAN DBC Files: Kvaser Database Editor

A CAN DBC file (CAN database) is a text files that contains information for decoding raw CAN bus data to 'physical values'. We use Kvaser Database Editor, which includes the ability to create and edit DBC files, append DBC files, and visualize the signal construction.

#### Useful Links

* [CAN DBC file explained](https://www.csselectronics.com/pages/can-dbc-file-database-intro)
* [Raw data to decimal converter](https://www.h-schmidt.net/FloatConverter/IEEE754.html)
* [Snowfinkle DBC files](https://github.com/uofmelectricboat/Lightning-McSeas/tree/main/dbc%20files) (Summer 2023 PEP Competition)

#### Datasheets

We make the DBC files based on the datasheets of components that are wired to the VCU.

| Datasheet | Owner | Notes |
| :---- | :---- | :---- |
| [GPS](https://drive.google.com/file/d/1ul1OAEmG7b7VrABJoXp_SV_jphUSG7cG/view?usp=drive_link) | Controls | Speed |
| [Actuators](https://drive.google.com/file/d/1GDaTBgGlo1CWdFGQUcA6tW-RRGx30Len/view?usp=drive_link) | Controls | Trim plate, jack plate, and wings (2) |
| [Inverters](https://drive.google.com/file/d/18Th4eHXrSkIGqwOTOoMu3LJCJ8r8Z_f1/view?usp=drive_link) | Drivetrain | May be through the BMS rather than the VCU |
| Steering wheel | Controls | Controls is working on making/sourcing a CAN-enabled wheel |
| [Cooling sensors](https://docs.google.com/spreadsheets/d/15f9kN0e133HEVDk-F0HdmYhkDNpvvALMN1A2owysBZE/edit#gid=1640551761) | Cooling | Must record flow/temp/pressure. Too many inputs for the VCU, we'll have to use an Arduino. |
| [BMS](https://www.orionbms.com/manuals/utility_o2/) | Powertrain | Powertrain has it's own control unit (Orion BMS 2) with a completely different programming environment. It involves thermistors (6 per pack, with 12 packs), contactors, and chargers. The VCU may need to send signals to the contactors. |
| [VCU](https://drive.google.com/file/d/1WkTzCAFvSJtV45WaHHaHLx2UFPWbgUJL/view?usp=sharing) | Controls |  |

### Programming the VCU: MATLAB Simulink and Raptor ToolKit

We use MATLAB Simulink with Raptor-DEV and Raptor-CAL to program the VCU. Importing our DBC files allows us to define the CAN messages and signals.

TODO

### Debugging Tools

CANalyzer, TODO

## Driver Display

The driver display is the main dashboard inside the boat, displaying essential information for the driver to check with a glance. It implements the following hardware components in the driver display:

* **Tablet**: [Dell Latitude 12 Rugged Tablet](https://www.dell.com/support/manuals/en-us/latitude-7202-tablet/lat12rugged7202_ug/specifications?guid=guid-dc9c68cb-09a4-4844-b470-4bb1e155c8b1&lang=en-us)
* **CAN adapter**: [Vector VN1610](https://www.vector.com/us/en/products/products-a-z/hardware/network-interfaces/vn16xx/#c66319) (connects to tablet via USB)

We designed this display based on those of similar speedboats, simplifying last year’s Snowfinkle dashboard.

| Snowfinkle Shore Dashboard  | TiDE Main Display |
| :----: | :----: |
| <img width="451" alt="Screenshot 2024-01-25 at 5 06 59 PM" src="https://github.com/uofmelectricboat/.github/assets/101139170/56c28f31-ae76-4181-b6f9-cfb3ef4fe4a0"> |  <img width="451" alt="Screenshot 2024-01-25 at 5 06 59 PM" src="https://github.com/uofmelectricboat/.github/assets/101139170/70f9f015-ac96-4432-ae9e-e0d2c5744185"> |

### Qt

The driver display is a Windows application built with Qt (pronounced “cute”). Qt is open-source cross-platform software for creating graphical user interfaces that run on major desktop platforms and mobile or embedded platforms. It is not a coding language–it is a framework written in C++. See more on the [Qt wiki](https://wiki.qt.io/About_Qt).

Qt provides different IDEs for different use cases:

* **Qt Creator** is more programmer-focused, providing tools for coding, debugging, and profiling. It allows users to open/edit an .ui or .qml file and create Qt/C++ applications.
* **Qt Design Studio** is a UI design tool that focuses on creating user interfaces.

They should be used together to develop a Qt Quick application with a visual UI designer. Both can be downloaded from the [Qt main website](https://www.qt.io/) (**Products** > **Qt Development Tools** > **Download Qt and Products** > **Qt Design Studio** > Get **Qt Design Studio**).

#### Qt CAN Bus Plugin

Qt’s Serial Bus module allows us to access the CAN bus via the VectorCAN plugin, which works with our CAN adapter. See the official documentation here:

* [QtSerialBus](https://doc.qt.io/qt-6/qtserialbus-index.html)
* [QtCANBus](https://doc.qt.io/qt-6/qtcanbus-backends.html)
* [VectorCAN plugin](https://doc.qt.io/qt-6/qtserialbus-vectorcan-overview.html)

#### Licensing
Qt is a free tool under GPLv3 and LGPLv3. Software created with Qt can be released under any approved open source license.

### Warning System
In the event of any issues, the main display must promptly alert the driver. We use a color-coded system to indicate operational health: yellow denotes warning levels, while red signifies a dangerous state. However, it is not always safe to assume that the driver is continuously monitoring the display. A stretch goal for this project is to incorporate an audible alarm system, which would alert the driver when they need to check the display for potential issues.
