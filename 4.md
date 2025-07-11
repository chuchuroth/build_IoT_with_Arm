The following technical and technological information is extracted from the sources, with colloquial language removed:

**Bluetooth Technology Overview**
*   Bluetooth originated as a late 1980s project for wireless serial communication, with the first consumer product being a Hand Street mobile headset launched in 1999.
*   It is a **wireless technology** operating in the **2.4GHz band**.
*   Its core functionality involves enabling **embedded devices to connect, pair, and exchange data securely**.

**Bluetooth Network Architecture (Piconet and Scatternet)**
*   Bluetooth networks are **Wireless Personal Area Networks (WPANs)**.
*   They comprise a **Bluetooth controller** and multiple **Bluetooth agents** connected to it.
*   A controller can manage up to **seven active agents** concurrently and up to **255 parked (inactive) agents**.
*   Bluetooth networks follow a **star architecture**, or **piconet**, where a single controller device coordinates communication with its active agents.
*   A device can function as a controller in one piconet and an agent in another, thereby forming a **scatternet**.
*   Examples of agents include fitness trackers, audio headsets, and printers, which can connect to a mobile phone acting as a controller. A mobile phone, while a controller for these devices, can also be an agent when connected to a desktop PC acting as a controller.

**Bluetooth Protocol Stack and Profiles**
*   The **Bluetooth Protocol** is highly complex; the **Bluetooth 5.2 core specification exceeds 3,000 papers**.
*   Specifications are **iterative**, meaning later versions integrate features from all previous versions.
*   The **protocol stack** and many other characteristics remain consistent across versions, with new elements added to improve energy efficiency, security, or localization.
*   The Bluetooth Protocol stack is **not fully aligned with OSI or TCP/IP models**, though it exhibits a degree of layering; some functions can span multiple layers.
*   A unique aspect is the **definition of profiles**, which define the scope of specific applications.
*   **36 distinct profiles** are defined in Bluetooth Classic, with Bluetooth Low Energy (BLE) adding more.
*   Some profiles, like the **Generic Access Profile (GAP)**, are fundamental, enabling the construction of other profiles and handling connection establishment.
*   **Bluetooth profiles describe an application and its collection of services**.
*   **Services are collections of characteristics** that define a part of a device's behavior.
*   **Characteristics are attribute types** possessing a name, a uniform type identifier, and an assigned number.
*   From an application perspective, profiles span the protocol stack by selecting relevant features from host protocols or other profiles.

**Physical and Link Layer Operations**
*   At the **physical (radio) layer**, Bluetooth operates in the **2.4 GHz Industrial, Scientific, and Medical (ISM) band**, which is license-exempt.
*   To minimize and mitigate interference from other technologies, **frequency hopping spread spectrum** is employed. This involves the communication channel periodically changing in an order agreed upon by the controller and agent, also offering a degree of confidentiality.
*   To enhance robustness against channel errors, data is **modulated using Gaussian Frequency Shift Keying (GFSK)** prior to transmission. GFSK applies a Gaussian filter to data pulses for smoother transitions and reduced sideband power, leading to less interference with adjacent channels.
*   The **default data rate is 1Mb/s**, with support for **2Mb/s and 3Mb/s**.
*   In the **link layer**, Bluetooth devices are uniquely identified by **6-byte addresses**, logically divided into a 3-byte organization part (assigned by the Tripoli Registration Authority to the manufacturer) and a 3-byte device part (assigned by the manufacturer).
*   Bluetooth data transmission is preceded by an **Access Code** and a **Header**. Bluetooth frames do not always contain a payload, for instance, when used for control purposes.
*   The **Access Code** includes a **preamble** (for receiver frame start detection), a **sync word** (identifies the piconet), and an optional **trailer**. The **Header** contains various control information.

**Bluetooth Low Energy (BLE)**
*   **BLE** was introduced in **revision four of the Bluetooth specification** to facilitate adoption on **constrained low-power devices, particularly IoT devices**.
*   BLE hardware is optimized to consume **10% to 50% of the power of Bluetooth Classic transceivers**.
*   The inquiry mechanism in BLE is modified for **faster connection setup**, and transmission power is reduced.
*   A BLE controller can support more active agents, and new application profiles (e.g., for medical and fitness tracking) are introduced.
*   In BLE, the controller is referred to as **central**, and the agent as **peripheral**.
*   The BLE physical layer largely retains **frequency hopping and GFSK modulation**.
*   The BLE spectrum is divided into **40 channels, each with 2MHz bandwidth**.
*   **Channels 37, 38, and 39 are used for continuous device advertising**.
*   The **BLE Protocol Stack** introduces new profiles:
    *   **Generic Attribute Profile (GATT)**: A set of procedures for discovering and accessing attributes.
    *   **Attribute Protocol (ATT)**: Mandatory for all data transfers.
    *   **Generic Access Profile (GAP)**: Controls advertisement and connections, along with device rules.

**Bluetooth Pairing and Security**
*   **Pairing** is a technique for **securing a link through data encryption**, providing **data confidentiality guarantees**.
*   The pairing procedure follows connection setup to establish link encryption.
*   Pairing involves three phases: **I/O capabilities exchange, association, and key distribution**.
*   Devices exchange information about their **Input/Output (I/O) capabilities** (e.g., input availability, button count, keyboard presence, output availability).
*   Based on I/O capabilities, three **association modes** are possible: **Just Works, PassKey entry, and Out of Band**.
*   **Out of Band** is the most secure but requires additional hardware. **Just Works** is the least secure due to default passcode usage. **PassKey entry** provides intermediate security.
*   Upon device association, a **temporary key** is generated, from which a **short term key** is derived.
*   Intercepting initial communication may allow an attacker to brute-force a temporary key.
*   Once the link is secured with the short term key, a **key distribution protocol** transmits a **long-term key (LTK)** for encrypting all communication, an **identity resolving key** for private device addresses, and a **connection signature resolving key** for data signing.
*   To address LTK compromise, **Diffie-Hellman key exchange technology** was introduced in later Bluetooth Standard revisions.

**Bluetooth 5 and Subsequent Revisions**
*   The **Bluetooth 5 specification** was released in **August 2018**, introducing two subversions.
*   It features **four physical layer modes**, all GFSK-based, categorized as **uncoded and coded**.
*   **Coded packets increase range** by utilizing **forward error correction** in parts of frames to combat bit errors from signal fading, though this diminishes the effective data rate.
*   **Bluetooth 5.1** introduced features for **positioning in IoT applications**.
*   Positioning relies on **direction finding through computed phase delay between signals arriving at different antennas**.

**Zigbee Technology**
*   **Zigbee** operates in the **868MHz band in Europe** and multiple channels in the **2.4GHz band**.
*   Zigbee data rates are slower than Bluetooth: **20kb/s in the 868MHz band** and **250kb/s in the 2.4 GHz band**.
*   It is suitable for applications where messages are less frequent and shorter, including **home and building automation and industrial control**.
*   A Zigbee network has three device types:
    *   **Coordinator**: Sends beacons and manages network-specific addresses.
    *   **Router**: Runs applications and forwards packets between other Zigbee nodes.
    *   **Zigbee end device**: Possesses reduced functionality and communicates only with the Zigbee coordinator or router.
*   Zigbee has a **well-structured protocol stack** largely conforming to the **OSI reference model**.
*   The **PHY and MAC layers are specified by the IEEE802.15.4 standard**, while other layers are specified by the Zigbee alliance.
*   Applications running on Zigbee devices are termed **Zigbee device objects (ZDOs)**, managed by the network and application support sublayers above the MAC layer.

**Practical BLE Application Development**
*   A lab involves communicating with the outside world via **Bluetooth Low Energy (BLE)** by programming an **embedded device to transmit live on-board sensor data to a mobile app** that communicates with BLE devices.
*   Required hardware includes the **Disco L465VG IOT01A board** and an **Android mobile phone with a Bluetooth LE scanner app**.
*   Software access to **Keil Studio Cloud** and the **BLE utility library** are necessary. Reference documentation for the **Mbed OS Bluetooth API** and GitHub examples are suggested for deeper understanding.
*   The application's structure involves:
    *   **Initializing Bluetooth Low Energy**.
    *   **Advertising the presence of the embedded device**.
    *   **Accepting connections and periodically transmitting sensor readings**.
    *   **Responding to write events to toggle an on-board LED remotely**.
*   Development involves creating **utility classes to manage the BLE API interface**, such as a "lab three server process" class for advertising the device name and a "lab three server" class to manage services and characteristics.
*   The application initializes and utilizes **temperature, humidity, and pressure sensors**.
*   For each sensor, a **BLE characteristic** is created and associated with an "**environmental**" service.
*   A helper class tracks the sensor's current value, converting it into a string representation for BLE transmission.
*   These characteristics are configured to be **readable** and to **notify the client upon value changes**, allowing repeated updates.
*   The sensor values are updated **once every second** by a function (`update sensors`) connected to an event queue, which calls `update value` on each characteristic with the latest sensor reading.
*   Remote LED control is implemented using a **writable characteristic**, where writing a '0' turns the LED off and a '1' turns it on.
*   The **`read write gatt characteristic` class** from the BLE API is utilized for LED functionality. This characteristic is initialized with a custom identifier (0xA000), and a method is implemented to control the LED based on client-written data.
