The following technical and technological information is extracted from the sources, with colloquial language removed:

**Wireless Area Networks**
*   **Wireless Local Area Networks (WLANs)** are larger deployments than Wireless Personal Area Networks (WPANs), with ranges extending to hundreds of meters and supporting higher data rates.
*   WLANs are typically found in home and office buildings and can underpin smart home automation devices.
*   The foundational wireless packet data networking protocol for WLANs was **ALOHAnet**, developed in the 1970s.
*   ALOHA protocol functions by transmitting a data packet immediately upon arrival in the transmission queue without channel sensing.
*   Unsuccessful packet delivery due to collision requires retransmission, indicated by the absence of an acknowledgment. The retransmission involves a backoff mechanism, but the duration of the wait was not specified or optimized based on network conditions.

**IEEE 802.11 (Wi-Fi) Technology**
*   The **IEEE 802.11 family of standards** is the de facto wireless LAN technology, frequently marketed under the **Wi-Fi trademark**.
*   **802.11 networks operate in two modes: infrastructure and ad hoc**.
    *   **Infrastructure mode** is the default and most utilized, where an **access point (AP)** acts as an arbiter, routing all communication through it. The AP can support contention-free operation by periodically polling client stations for transmission.
    *   The widely used operational mode is **contention-based**, where stations manage their individual behavior and contend for channel access using shared parameters. The access point maintains station synchronization, advertises the network's basic service set, and handles client association and authentication.
    *   In **ad hoc mode**, the access point's role is shared among stations, with one station advertising an independent service set for others to join. This role can be swapped among participants.
*   IEEE 802.11 wireless LANs operate in **license-exempt Industrial, Scientific, and Medical (ISM) bands**: 2.4-2.5 GHz and 4.915-5.85 GHz.
*   The **default channel width is 20 MHz**.
*   In the 2.4 GHz range, **12 logical channels** are used, with only **three being non-overlapping**. The 5 GHz band offers more non-overlapping channels, subject to regional regulations and deployment scenarios (indoor/outdoor).

**802.11 Protocol Enhancements (Throughput Improvement)**
*   **802.11n** improves throughput by:
    *   Utilizing **twice the bandwidth through channel bonding** (combining two channels).
    *   Employing **Multiple-Input, Multiple-Output (MIMO)**, a signal processing technique allowing simultaneous transmission of multiple data streams between two pairs.
    *   Encoding **more bits of information per symbol** to increase data rates.
    *   Reducing contention and overhead through **frame aggregation techniques**.
    *   Enabling **retransmission of only erroneous parts of a message** to improve channel efficiency.
*   **802.11ac** further enhances throughput by:
    *   Supporting **channels up to 160 MHz**, making the 5 GHz band exclusively suitable for this standard.
    *   Supporting **up to eight MIMO streams**, multiplying data rates by eight.
    *   Utilizing **new modulation schemes** to transmit up to 16 bits per symbol.
    *   Adopting **Multi-User MIMO (MU-MIMO)**, which allows an access point to transmit to multiple stations concurrently, a technique known as **spatial multiplexing**.

**Low-Power Wide Area Networks (LPWAN)**
*   **LPWAN technologies** support long-range networking for IoT by employing **lower radio frequencies**, which inherently expands collision domains and limits data rates but reduces power consumption due to infrequent messaging.
*   Competing LPWAN technologies include:
    *   **IEEE 802.11ah**: Operates in the **900 MHz band**, typically on 2 MHz channels.
    *   **Weightless-P**: Deployed in **sub-gigahertz bands** on 12.5 kHz channels.
    *   **LoRa and LoRaWAN**: Utilizes a **chirp spread spectrum technique** with typical data rates less than 6 kilobits per second.
    *   **Extended coverage GSM**: Based on cellular GPRS.
    *   **Narrowband IoT (NB-IoT)**: Designed to coexist with LTE.
    *   **LTE Cat-M**: Similar to NB-IoT but with higher data rates and mobility support, requiring more bandwidth and operating in the same band as LTE.
*   Factors influencing the choice of LPWAN technology include:
    *   **Coverage-throughput trade-off** (low frequency narrow bandwidth vs. higher frequency larger bandwidth).
    *   Deployment cost and interference.
    *   Licensed versus unlicensed spectrum.
    *   Complexity (e.g., centralized vs. decentralized access).
    *   Compatibility with existing wireless or cellular systems (e.g., 3G or LTE).
    *   Support for mobility (e.g., automotive IoT).
    *   Latency (guaranteed scheduled airtime vs. contention-based multiplexing).
    *   **Security**, which is a key factor in all LPWAN solutions.

**LoRaWAN Technology**
*   **LoRaWAN** is deployed in various **unlicensed frequency bands** based on geographic location and regulations, including 433 MHz and 868 MHz in Europe, 915 MHz in Australia and North America, and 923 MHz in Asia.
*   **Channel time occupation is restricted** via duty-cycle regimes due to the long range supported, with variations depending on the carrier frequency.
*   It is underpinned by a **proprietary physical layer** using **chirp spread spectrum modulation**.
*   Data rates are in the order of **kilobits per second**, with higher rates in some regions facilitated by **frequency shift keying modulation**.
*   **LoRaWAN networks consist of end node IoT devices, gateways, and network servers**.
    *   **End nodes** connect wirelessly to **gateways** using LoRa modulation.
    *   **Gateways relay information** between end nodes and network servers. They are also responsible for end node activation, access authorization, and link security.
    *   **Network servers** host applications that consume and provide data to end nodes.
    *   **Backhaul links** transport TCP/IP traffic over various networking technologies.
*   Communication between end nodes and applications is **end-to-end secured**.
*   LoRaWAN is the **protocol stack layered on top of the LoRa physical layer**.
*   The channel is **slotted and multiplexed**, following an ALOHA-like protocol.
*   Data transmitted by end nodes (e.g., sensor readings) is **encrypted**, and only the intended application can decrypt it. Commands from cloud-based applications to actuators are similarly encrypted.
*   The LoRaWAN specification defines **three device classes**, all mandating bidirectional communication:
    *   **Class A**: A node can transmit within duty-cycle limits, with each transmission followed by two short downlink receive windows.
    *   **Class B**: Devices operate with additional precisely scheduled receive windows, ensuring controlled latency.
    *   **Class C**: Devices listen continuously unless transmitting, limiting battery operation.
*   **Two layers of security** exist in LoRaWAN, both using **AES-128 encryption**:
    *   **Link security**: Uses a **network key** shared between the end device and the gateway.
    *   **Payload security**: Uses an **application key** known to the end node and the service logic consuming/controlling data. This ensures confidentiality as intermediate network entities cannot inspect message content.

**Narrowband IoT (NB-IoT)**
*   **NB-IoT** is suitable for applications requiring **strict delay guarantees and reliability**, where cost is not a primary concern.
*   It can be deployed alongside existing LTE systems (in the same band, in a guard band adjacent to an LTE carrier, or stand-alone in a different licensed band).
*   NB-IoT systems operate with a **bandwidth of 180 kHz**.
*   Achievable data rates are **25 kb/s downlink and 64 kb/s uplink**.
*   Latency less than **10 milliseconds** is achievable because transmissions are aligned with LTE frames.
*   NB-IoT implements a **hybrid Automatic Repeat Request (HARQ)** scheme for reliability.
*   Energy efficiency is maintained as the **base station controls transmit power and sleep modes via signaling**.

**IoT Application Development with Google Cloud**
*   An embedded device can be programmed to communicate with a cloud service by **transmitting sensor data through a WiFi interface to a publish/subscribe system hosted by Google**.
*   Hardware requirements: Disco L465VG IOT01A board.
*   Software requirements: Keil Studio Cloud, a free Google Cloud account, and the Mbed OS Example for Google IoT Cloud.
*   Steps for setting up Google Cloud for IoT communication:
    *   Create a Google Cloud project (e.g., "arm ed-x lab 4") and ensure it is active.
    *   Enable the **IoT Core Service** within the Google Cloud console.
    *   Create a **registry key** (e.g., "lab 4") and an associated **Pub/Sub topic** (e.g., "sensors") in IoT Core.
    *   Generate a **public/private keypair** (e.g., `private_key.pem` and `public_key.pem`) for authentication.
    *   Create a device (e.g., "my board") in the registry configuration and upload the public key for authentication, selecting **ES256 format**.
    *   Configure the Mbed project by editing the `mbed_app.json` file with Google Cloud project information and WiFi credentials. This includes escaping quotation marks in configuration values.
    *   Insert the private key content into the `google_cloud_credentials.h` file.
    *   Create a **subscription** for the message topic (e.g., "sensors") in the Pub/Sub management screen within the IoT Core console.
*   After configuration, the embedded program should build and run, displaying "connected" and "publishing" messages. Messages can be verified in the cloud console's messages tab by clicking "pull".
*   To send sensor readings, initialize sensors and modify the publish function to send a **JSON message** containing sensor data, using `sprintf` for formatting, then publish it to the cloud.

**Storing and Accessing Sensor Data with Cloud Functions and Datastore**
*   **Sensor readings can be stored in a database** for web application querying.
*   Database setup: Navigate to the **Datastore section** in Google Cloud Console to activate the service.
*   Create a **service account credential** (e.g., "datastore") under "APIs and Services" > "Credentials", assigning it the "**Datastore User**" role. Generate and download a new key in **JSON format**.
*   A **Cloud Function** is executed in response to an event. A Cloud Function can be created to process new sensor data from the embedded system and store it in a database.
*   Create a new function (e.g., "Process Sensor Data") in the "Cloud Functions" section, attach it to a region (e.g., `europe-west2`), and trigger it on the "sensors" Pub/Sub topic.
*   Use the "Node.js 14" runtime for the function. After deployment, embedded device initialization and sensor data transmission will trigger the function, with logs showing execution and sensor data output.
*   To store data in Datastore, the function code needs modification: it parses the incoming sensor data into an object and stores it in the Cloud Datastore using the receive timestamp as the key, also storing the timestamp as a data field for future queries.
*   The Datastore constructor settings must be updated with the project ID and the name of the secret key JSON file, which must also be uploaded. A dependency in `package.json` needs to be added.
*   Upon deployment and embedded device operation, data should be inserted into the Datastore database.

**Web Application for Data Display**
*   A web application can display the stored sensor data.
*   Another **Cloud Function** (e.g., "Get Sensor Data") is created, triggered by **HTTP**, set for anonymous triggering, and requiring **HTTPS**.
*   This function queries the database for the last 10 sensor data items, ordering them by timestamp, and returns these records.
*   **Cross-origin Resource Sharing (CORS)** must be enabled to allow the function to be called from web pages on different domains. The provided example is lenient, allowing access from any web page.
*   The project ID and secret key filename must be updated, and the secret key uploaded, before deploying this function.
*   The function's invocation URL can be tested in a web browser or using command-line tools like `curl`.
*   A **basic web interface (HTML file)** can be created to read data from the "Get Sensor Data" function and display it in a table.
*   The HTML file includes a heading, an empty table with headings, and a script.
*   The script uses `getElementById` to reference the table body.
*   A `loadData` function clears existing table contents.
*   It calls the "Get Sensor Data" Cloud Function using the **Axios web request library**.
*   Upon receiving data, a loop iterates through each data item, creates a new table row (`TR`), and adds four cells (`TD`):
    *   **Timestamp**: Formatted using `toLocaleString`.
    *   **Temperature**: Reduced to one decimal place using `toFixed` and appended with "degrees celsius".
    *   **Humidity**: Decimal places reduced and appended with a percentage sign.
    *   **Pressure**: Formatted using `toFixed`.
*   The `loadData` function is executed every five seconds, with an initial invocation.
*   The HTML file is uploaded to **Cloud Storage** by creating a new bucket (e.g., "sensor-data-viewer") and uploading the file. The "Authenticated URL" property of the uploaded file provides access, with options to change permissions for public access.
