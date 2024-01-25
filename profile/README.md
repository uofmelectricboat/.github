# UMEB Software Projects

The list below provides an overview of the main software projects on the University of Michigan Electric Boat team:
* VCU programming (MATLAB Simulink, CANalyzer)
* Driver display (Qt, QML, C++)
* Website development (HTML/CSS, Javascript)
* Debug display*
* Shore display*
* Data analytics*

Projects marked with an asterisk are not yet started. Questions? Please contact these team members:
* Michael Sharashenidze (msharash), Electrical Lead
* Adam Lake (adamlake), Controls Lead
* Megan Miller (megmil), Software Engineer

## VCU Programming

The Vehicle Control Unit (VCU) is essentially the central processing unit of the boat. It activates electrical components, records important data, and controls elements like sensors and actuators. It also serves as the central communication hub between different parts of the boat via the Controller Area Network (CAN) bus. The CAN bus is a vehicle bus standard that allows the sensors, actuators, and microcontrollers on the boat to communicate.

We use the [Raptor General Control Model GCM196](https://store.neweagle.net/shop/raptor/raptor-hardware/raptor-controllers-with-software/1793-196-1503-general-control-module-raptor/) as our VCU.

### Raptor Toolchain

The electronic hardware components on our boat (like sensors and actuators) are programmed using software provided by New Eagle. We have free access to New Eagle’s Raptor Toolchain (i.e. Raptor-Dev and Raptor Cal) ($9600 worth of software!), courtesy of our use of the Raptor GCM.

#### Programming Environment

Typically, we would program our electronic hardware using languages like C or Python to implement low-level driver code provided by manufacturers. The Raptor Toolchain simplifies this process, allowing us to use MATLAB Simulink (supplemented with additional Raptor libraries) to program the VCU. Additionally, we use Vector CANalyzer software to program the CAN bus.

See the software setup guide [here](https://docs.google.com/document/d/1cnFTK1jpPUwSgk5_LYbEjfsr6MsOQiAcEhOZyKOdtkA).

#### Platform Compatibility

Please note that all Raptor tools are only compatible with Windows. For Mac users who wish to view and operate the Raptor software, we recommend using CAEN computers.

### System Block Diagram

Below is an image of the current system block diagram (source: [Lucidchart](https://lucid.app/lucidchart/c0bbbfa5-0525-45ad-8ec3-776604d7f318/edit?invitationId=inv_6c9863e5-fb13-4fd6-8d17-4680908d763c&page=0_0#)):

<img src="https://github.com/uofmelectricboat/.github/assets/101139170/32fef8ed-8dbb-4f66-82f4-b4bcb79485ca" alt="drawing" width="500"/>

For more details or access to the Lucidchart file, contact the Electrical Lead.
