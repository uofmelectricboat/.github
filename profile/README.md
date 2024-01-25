# UMEB Software Projects

The list below provides an overview of the main software projects on the University of Michigan Electric Boat team:
* [VCU programming](#vcu-programming) (MATLAB Simulink, CANalyzer)
* [Driver display](#driver-display) (Qt, QML, C++)
* Website development (HTML/CSS, Javascript)
* Debug display*
* Shore display*
* Data analytics*

Projects marked with an asterisk are not yet started. Questions? Please contact these team members:
* Michael Sharashenidze (msharash), Electrical Lead
* Adam Lake (adamlake), Controls Lead
* Megan Miller (megmil), Software Engineer

## VCU Programming

The Vehicle Control Unit (VCU) is essentially the central processing unit of the boat. It activates electrical components, records important data, and controls elements like sensors and actuators. It also serves as the central communication hub between different parts of the boat via the Controller Area Network (CAN) bus, a vehicle bus standard that allows microcontrollers and devices on the boat to communicate with each other without a host computer.

We use the [Raptor General Control Model GCM196](https://store.neweagle.net/shop/raptor/raptor-hardware/raptor-controllers-with-software/1793-196-1503-general-control-module-raptor/) as our VCU.

### Raptor Toolchain

The electronic hardware components on our boat (like sensors and actuators) are programmed using software provided by New Eagle. We have free access to New Eagle’s Raptor Toolchain (i.e. Raptor-Dev and Raptor Cal) ($9600 worth of software!) due to our use of the Raptor GCM.

#### Programming Environment

Typically, we would program our electronic hardware using languages like C or Python to implement low-level driver code provided by manufacturers. The Raptor Toolchain simplifies this process, allowing us to use MATLAB Simulink (supplemented with additional Raptor libraries) to program the VCU. Additionally, we use Vector CANalyzer software to program the CAN bus.

See the software setup guide [here](https://docs.google.com/document/d/1cnFTK1jpPUwSgk5_LYbEjfsr6MsOQiAcEhOZyKOdtkA).

#### Platform Compatibility

Please note that all Raptor tools are only compatible with Windows. For Mac users who wish to view and operate the Raptor software, we recommend using CAEN computers.

### System Block Diagram

Below is an image of the current system block diagram (source: [Lucidchart](https://lucid.app/lucidchart/c0bbbfa5-0525-45ad-8ec3-776604d7f318/edit?invitationId=inv_6c9863e5-fb13-4fd6-8d17-4680908d763c&page=0_0#)):

<img src="https://github.com/uofmelectricboat/.github/assets/101139170/32fef8ed-8dbb-4f66-82f4-b4bcb79485ca" alt="drawing" width="500"/>

For more details or access to the Lucidchart file, contact the Electrical Lead.

## Driver Display

The driver display is the main dashboard inside the boat, displaying essential information for the driver to check with a glance. It implements the following hardware components in the driver display:

* Tablet: [Dell Latitude 12 Rugged Tablet](https://www.dell.com/support/manuals/en-us/latitude-7202-tablet/lat12rugged7202_ug/specifications?guid=guid-dc9c68cb-09a4-4844-b470-4bb1e155c8b1&lang=en-us)
* CAN adapter: [Vector VN1610](https://www.vector.com/us/en/products/products-a-z/hardware/network-interfaces/vn16xx/#c66319) (connects to tablet via USB)

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
