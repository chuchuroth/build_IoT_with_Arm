Here is the technical and technological information extracted from the sources, with colloquial language removed, important parts bolded, and bullet points used for clarity:

**Cloud Computing and Virtualization**
*   **Cloud computing** is a **paradigm** that provides **on-demand access to computer system resources**, such as **data storage** or **compute power**, eliminating the need for user involvement in system administration.
*   The **Cloud** refers to **collections of high-availability servers** that **store and process large volumes of data**, enabling developers to concentrate on software development and data analytics.

**Cloud Service Models**
The Cloud offers three primary service models:
*   **Infrastructure as a Service (IaaS)**: Users access **raw virtual machines** to install and control their own operating systems, **networking fabric**, and **raw storage platforms**. Users request virtual resources from the provider without managing the underlying hardware.
*   **Platform as a Service (PaaS)**: Users access **web servers, application runtimes, databases, and development tools** without managing the underlying operating system. This model operates at a higher level than IaaS.
*   **Software as a Service (SaaS)**: Actual **applications operate within a Cloud environment**, including office productivity suites, email systems, customer relationship management (CRM) systems, and financial systems. Users interact with these applications without knowledge of the underlying hardware architecture.

**Cloud Applications in IoT**
*   The Cloud supports **remote management and configuration of IoT devices**, including managing device connectivity and sending firmware updates.
*   Key applications of compute resources in the Cloud involve **aggregating, processing, storing, analyzing, and visualizing data**.
*   **Sharing computing infrastructure** allows multiple tenants to utilize the same physical compute resources without interference. Providers can offer customized versions of services based on shared operating systems or software libraries.

**Virtualization Concepts**
*   **Virtualization** is a **key enabler for Cloud computing**. It involves creating **logical partitions or copies of a physical resource** to enable sharing and customization among different users. This process creates a **virtual version of a Physical Platform**.
*   Virtualization can be applied across various layers, including **hardware, networks, storage, and operating systems**.
*   A **hypervisor or orchestrator** is responsible for **coordinating access to shared resources** and ensuring **strict partitioning** between different processes. This logical separation inherently provides a **safe execution environment**, preventing different workloads or processes from corrupting others running on the same physical entity.
*   **Hardware security methods**, such as armed trust zones, can further enforce system integrity.
*   The two main approaches for virtualization are **virtual machines** and **containers**.

**Virtual Machines (VMs)**
*   A **hardware virtual machine (VM)** is an offering within **Infrastructure as a Service (IaaS)**.
*   VMs allow **multiple instances of potentially different operating systems** to run on the same physical computing platform.
*   VMs are created, run, and monitored by a **hypervisor**.
    *   **Type 1 (bare-metal) hypervisor**: Runs directly on the physical host machine.
    *   **Type 2 (hosted) hypervisor**: Runs on top of the host operating system.

**Containers**
*   **Containers** are a type of **Platform as a Service (PaaS)** offering, representing **OS Level Virtualization**.
*   Different applications run on **isolated user space partitions** on the **same operating system**.
*   The **OS kernel** manages access to peripherals, computing, and networking resources from the application's perspective, and is responsible for **partitioning between different containers**.
*   A **container engine** is used to create and destroy containers, similar to a hypervisor, but **multiple OS instances are not required**.
*   From a code execution perspective, the kernel is shielded from program bugs or security issues within the containers.
*   Containers are **faster to instantiate** than virtual machines and can be created and destroyed as needed.
*   They only require a **Container Runtime** instead of a hypervisor.
*   **Sharing operating system libraries** among containers is common, and containers are **highly scalable**.

**Serverless Computing**
*   **Serverless computing** is a virtualization technique that combines advantages of both VMs and Containers.
*   The term "serverless" is a misnomer, as server infrastructure is still required, but **application developers are not responsible for managing it**.
*   Applications developed for serverless environments are broken into **individual functions** that execute in the Cloud, potentially across different machines.
*   Unlike containers, which run continuously and require library configuration upon deployment, **serverless functions are stored in the Cloud and can be instantiated much faster**.
*   In serverless computing, the tenant **pays only for the duration the function is actively running**.

**MQTT Protocol**
*   **MQTT (MQ Telemetry Transport)** is a **publish/subscribe protocol** designed for **distributing short messages between IoT devices**.
*   In MQTT, **publishers** transmit information to a central entity known as the **MQTT broker**, and **subscribers** receive this information when changes occur.
*   MQTT is an **application layer protocol**, similar to HTTP, implemented on top of **TCP/IP**.
*   Communication can be secured through **Transport Layer Security (TLS) encryption**.
*   Due to its small packet size, MQTT is particularly suitable for **low-bandwidth network deployments** in IoT.
*   Mainstream versions include **3.1 and 5**. Version 5 introduces features such as **session and message expiry, shared subscriptions, maximum packet size specification, enhanced authentication, and OAuth**.
*   MQTT nodes are interconnected in a **star topology**, with the broker mediating between publishers and subscribers. This topology offers **privacy** (clients are unaware of each other's addresses) and **scalability** (additional clients can be added).
*   **Topics** serve as **virtual communication channels** governing message distribution. Multiple topics can be combined under a single topic level for improved efficiency.

**MQTT Quality of Service (QoS)**
*   Publishers can select different **Quality of Service (QoS) levels** for messages sent to the broker, impacting delivery guarantees and speed. Lower QoS numbers indicate fewer delivery guarantees but faster delivery in the absence of packet loss.
*   **QoS Level 2**: The highest QoS level, guarantees a message is delivered **exactly once** using a **four-way handshake**.
    *   A published message with QoS2 must first be acknowledged with a **PUBREC packet**.
    *   If the sender does not receive PUBREC, it re-sends the published message with a duplicate flag.
    *   Upon receiving PUBREC, the sender responds with a **PUBREL message**.
    *   A broker receiving PUBREL discards all stored states and responds with a **PUBCOM packet**.
    *   The transaction is considered complete when PUBCOM is received by the sender.
*   **QoS Level 1**: Faster delivery, with equivalent reliability possible if the service can manage duplicate messages.
*   **QoS Level 0**: Messages are transmitted **at most once** with **best-effort delivery**. The message is not acknowledged by the broker, not stored, and re-delivery is not attempted if the message is lost in transit.
*   QoS primarily provides guarantees for message delivery to the broker, but **not to subscribers**.
*   **Retained messages** address subscriber delivery issues by having brokers store messages with the retained flag set. New subscribers immediately receive the latest published message on a topic, regardless of when it was published.

**CoAP Protocol**
*   **CoAP (Constrained Application Protocol)** is an alternative to MQTT, functioning similarly to HTTP but specifically targeting **IoT environments, constrained devices, and low-power or lossy networks**.
*   CoAP operates on top of **UDP**, which avoids connection setup/teardown overhead and carries smaller message overhead compared to TCP.
*   Due to UDP's limitations (no re-transmissions or packet reordering), CoAP handles reliability at the application level.
*   CoAP packets feature a minimal **4-byte header**, with message body constraints.
*   When using **IPV6 over low-power wireless personal area networks (6LoWPAN)**, CoAP messages are designed to fit within a single **IEEE 802.15.4 frame**.
*   **CoAP nodes** can **cache request and response messages** for operation over lossy links.
*   Unlike HTTP, CoAP supports **multicast**, useful in machine-to-machine communication, and provides a **mechanism for resource discovery**.
*   Constrained servers can use **Constrained RESTful Environments (CoRE) link format** to describe hosted resources.
*   Unlike MQTT's star topology, a **CoAP device can function as both a client and a server**.
*   CoAP messages embed a **token** to match requests to responses in lossy link environments.
*   **Options** can be enclosed in a packet; the **observe option** is used to monitor resources (e.g., firmware updates, device state). Setting the observe option to zero registers interest in receiving updates, establishing a notification mechanism that significantly reduces network traffic.
*   For transferring larger content that exceeds CoAP message size, **block-wise transfer mode** is defined, introducing **block options** for transmitting multiple information blocks via multiple request-response pairs, avoiding IP fragmentation.
*   **Datagram TLS** can be optionally added for high-level communication security.
*   A CoAP packet includes a **version flag**, a **type flag** (confirmable/non-confirmable, acknowledgment/reset), a **TKL field** (token length), a **code field** (status code similar to HTTP), a **message ID** (for duplicate detection), and an optional **token** (0-8 bytes request-response matching identifier). These are followed by additional options and the message payload.

**Data Processing Pipelines and Big Data**
*   **Data Processing Pipelines** are sequences of computing elements that process or perform computations on data from sensors or IoT devices. Data flows through these pipelines, undergoing transformation.
*   In IoT settings, data sources originate from sensed phenomena converted into digital signals.
*   **Edge processing** involves performing initial data processing (e.g., noise removal, conversion to higher-level summaries like step counts) close to the device, potentially on an IoT Hub, before transmission to the Cloud.
*   Data streams arriving in the Cloud from IoT devices may undergo **real-time computation**, such as online machine learning or real-time analytics, facilitated by platforms like **Apache Storm**.
*   **Stream processing** and **topic-based publishing** are facilitated by platforms like **Apache Kafka** for feeding data streams to multiple systems.
*   For big data storage and later processing (when real-time analytics are not required), **non-relational distributed databases** enable rapid querying and selection across large numbers of records.
    *   **Apache HBase** is an open-source example of such a database.
    *   These databases often integrate with **distributed storage solutions** like the **Hadoop Distributed File System (HDFS)**, where clusters of nodes store vast amounts of data.
    *   **Split-apply-combine strategy programming models**, such as **MapReduce**, are used for data analysis on stored data.
*   **Apache Hive** offers an **SQL-like interface** to query data across different databases and file systems, integrating with Hadoop.
*   **Workload scheduling tools** are beneficial for managing parallel processes or pipelines. The core concept is to combine complex jobs and define their execution order to achieve larger tasks.
*   **Distributed File Systems (DFS)** handle large data volumes and fast retrieval. Unlike conventional storage, DFS data resides on **inter-networked machines and/or sites**.
*   A DFS provides a **unified, transparent view to the client**. A **namespace augmented with metadata** allows rapid content location without exposing storage details to the client.
*   **Concurrency** is critical in DFS, where data blocks may be replicated across multiple machines or sites, to ensure all clients have a consistent view of the data.

**Workflows and Scheduling**
*   **Workflows** can be modeled as **directed acyclic graphs (DAGs)**, consisting of **control flow nodes** and **action nodes**.
*   **Control flow nodes** define the start and end of workflows and mechanisms for controlling execution paths.
*   **Action nodes** trigger the execution of processing and computation tasks.
*   Multiple jobs can be run in parallel within a workflow.
*   **Apache Oozie** is an example of a **workflow scheduler** that integrates tightly with Hadoop and can incorporate various Apache jobs.

**IoT Application Components and Processes (from Lab context)**
*   **Sensor data collection**: Gyroscope and accelerometer data can be collected, batched, and sent to a cloud service.
*   **Data representation**: Sensor readings can be structured as **JSON data** for transmission.
*   **Cloud Functions for data processing**: Cloud functions can be triggered by new batches of sensor data.
    *   They can **analyze data**, compute **average and standard deviation**, and simulate **machine learning (ML) models** for classification.
    *   The classification results can be stored in a **database**.
    *   Another cloud function can be invoked when classified activity data is presented on a Pub/Sub topic, which can normalize data and send it to an ML model for classification.
*   **Data exposure via HTTP endpoint**: Activity data can be exposed as an **HTTP endpoint** using a Cloud Function to allow mobile applications to request historical data.
*   **Mobile Application Architecture (Android)**:
    *   **User Interface (UI)** elements are organized hierarchically.
    *   UI components include progress indicators, scroll views, table layouts, and switch components.
    *   **Constraint layout** is a method for positioning UI components relative to each other.
    *   An **Android Activity class** represents a screen or view of the application.
    *   The **`onCreate` method** is invoked during the view creation lifecycle.
    *   **Event listeners** (e.g., `checked change event listener`) detect user interactions.
    *   A **Timer object** can schedule recurring tasks, such as making web requests at regular intervals.
    *   A **Handler** is used to perform actions on the **UI thread**, as UI elements cannot be modified directly from other threads.
    *   A **request queue** (e.g., using the Volley library) dispatches HTTP requests asynchronously without blocking threads.
    *   Android applications require explicit **internet access permissions**.
    *   Returned data (e.g., JSON) is parsed. Adjacent activities of the same type can be merged for display.
    *   **Error handling** is implemented using `try...catch...finally` blocks to manage exceptions and ensure cleanup actions.
