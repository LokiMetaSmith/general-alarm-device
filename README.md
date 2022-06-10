# General Purpose Alarm Device
This General-Purpose- Alarm-Device repository defines a 'general purpose alarm device' GPAD module.
We seek a highly repurposable device that can make lound noises and flash bright lights in order to get the attention of someone, 
especially health-care workers, in response to some condition that requires attention.
The GPAD does not detect the conditions that need to be alarmed.
Presumably, those are sensed by a different device, such as a medical ventilator.
Rather, it offers a simple API, possibly with a JSON or byte-level interface, for commanding it to alarm.

# Example Use Case, The Ventilator

The [Freespireco Project](https://github.com/PubInv/freespireco) is an attempt to build a modular ecosystem of cooperating respiration devices. One need that devices such as ventilators and oxygen concentrators need to have is to be able to alert someone to dangerous conditions. This can be as simple and gentle as "it is time for scheduled maintenance" to a far more dangerous "the hose connected to the patient is disconnected!"
The purpose of the alarm is to get the attention of nurses or doctors who can fix the problem.

# The Abstract Application Programmers Interface

Abstractly, we can imagine a system that supports five levels of alarm severity.
Additionally, an alarm condition normally has a short message associated with it, such as "hose disconnect", which 
should potentially be displayed on a small screen.

The initial version of this API can be extraordinarily simple: Alarm at a level between zero and five, where zero means no alarm.
However, it is clearn this API will have to evolve over time. Issues such as when one alarm level supercedes another, when it is 
acceptable to silence an alarm and for how long, etc. actually become rather complicated quickly.

We hope that by defining a clearly versioned API we can make an evolving device of great utility for a wide variety of purposes.

# Stand-alone or Sub-assembly

We believe a loosely-coupled physical device is the most repurposable.  Such a device would have its own independent power supply.
However, there are clearly use cases when the same module should be integrated into the physical case, power system, and even printed
circuit board of other systems. We therefore seek design flexibility that supports all of these usage modes.

# The Arduino Platform Is Sufficient

The on-board functionality of this device should not exceed the power of the simplest, slowest micropocessors in the Arduino family.
It therefore seems reasonable to confine our efforts to the most "plain vanilla" solutions possible, which at present means
the Arduino platform.

# How is the alarm signal received?

There are many potential ways to communicate an API command to the GPAD. The obvious are:
1. The serial port
2. SPI
3. WiFi
4. Bluetooth

A wireless interface is probably most valuable for hobbyist and makers; and SPI-based protocol is probably most valuable for integration with a\
medical devices, such as [PolyVent Open Source Ventilator](https://www.pubinv.org/project/polyvent/). In general, we favor the use of JSON for a
serial or wireless interface binding to the API, and a byte-level binding for an SPI connection.

Initial implementations should support a serial port, because this is the easiest to test and widely available on stand-alone Arduino devices. 
If the GPAD is integrated, it may forgo the serial port in favor of SPI.

# The Potential Evolution of the Project

## Phase I

The most important action at the beginning of the project is define a simple API.
Additionally, an initial selection of a loudspeaker or siren and a flashing light of some kind should be made.
We imagine these hardware choices will evolve over time. We want the API to insulate the user of the GPAD 
from specific details of how the noise is made.

Nonetheless, we can make a few comments.
1. It is now possible to get very bright LEDs which are efficent. The initial version might simply use a single very bright LED, or some combination of LEDS supporting 5 levels of alarm color or brightness.
2. Although "buzzers" and "sirens" of various kind are available, we eventually want a loudspeaker that can make various noises to provide information about the alarm level. Someday it may even support recorded messages in a human voice speaking a natural language. Imagine the voice of Scotty saying "She canna' take the strain, Captain!" in a Scottish accent.

The physical implementation at this level might be a breadboard solution or a soldered Arduino UNO shield.

## Phase II

In Phase II, we can imagine a large number of improvements:
1. An enclosure for the electronics which is designed to be easily mounted (for example, with flanges for zip ties.)
2. A Printed-circuit board that integrates the simple electronics with an Arduino Nano or Micro-sized solution on a single board.
3. Improvements in the API.
4. A display screen which allows a short message to be displayed.
5. One of more buttons of controls which allows the GPAD to be silenced to avoid "alarm fatigue".
6. A simple JST connector to suport an SPI interface.

## Phase III

In Phase III, we could expland the usability of the device by allowing it to be made physically versatile, which feature such as:
1. A backup battery on board.
2. Sturdiness to the level of being a "throwie" that can be deployed by tossing it across the room.
3. WiFi, Bluetooth, or LoRa enablement.

In each of these phases, we imagine the API improving substantially.

# Volunteer Skills Needed

We would like to form a small team with diverse skills around this. Mr. Lee Erickson is offering to act as a mentor and invention coach,
in addition to Robert L. Read, founder of Public Invention.

We need:
1. Arduino engineers who can both code and make very simple circuits.
2. PCB layout designers.
3. Mechanical engineers who can design sturdy enclosures that keep the system bright and loud.
4. Software enginers who can design an effective, evolving API and the transport bindings that they require.
5. GUI experts who can address issues such as how to effective alarm and silence.
6. Marketers who can promote and evangelize the project.
7. Possible a project manager who can organizae volunteers and keep them enthused and motivated to move forward.

# The Potential for a Product

Like everything done by Public Invention, this is a fully open project that will be released under fully open hardware and software licenses.
However, unlike many of our projects which are very "researchy" this project could become a salable product pretty easily.
One can imagine it being sold at Sparkfun, Adarfuit, or DigiKey if we do a good job.
Because it could be used for a wide variety of purposes by makers and could be sold at a price of perhaps $15USD or $25USD,
it could have enough market so support a production run of a few hundred.
Potential uses as a product (by hobbiest) include:
1. Alarming a cat door
2. Alarming when a visual signal, such as an animal moving in a game camera is detected
3. Detection of life-threatening conditions in medical devices
4. Overheating conditions in almost any device
...but the reader can probably imagine a great many more.

Public Invention does not wish to become a manufacturer; but we will impartially support anyone who wants to take these designs and manufacture them 
so long as they abide by the licenses.



