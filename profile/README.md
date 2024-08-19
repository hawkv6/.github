<h1 align="center">Welcome to the HawkV6 Project</h1>

<p align="center">
HawkV6 empowers developers, application managers, and sysadmins with an easy-to-use tool for creating end-to-end paths—from client to server—that meet the specific requirements of each application.
</p>

## Problem
Today's networks are often overly complex, requiring extensive manual configuration and expert knowledge to enable connectivity. They typically operate at the network level, lacking the flexibility to adapt to the varying requirements of different applications. Networks are generally configured to provide best-effort service to all applications, which is not always sufficient. Additionally, policies are often applied at the network edge, interfering with the true end-to-end path between client and server. Some applications need low latency, others require high bandwidth, or high reliability with minimal packet loss. Networks should be capable of adapting to these diverse application needs without constant intervention from administrators.

## Solution

HawkV6 leverages Segment Routing over IPv6 (SRv6) and Intent-Based Networking principles to establish and maintain the optimal end-to-end path between clients and servers based on specific application requirements.

HawkV6 consists of several components, with two key components: **HawkEye** and **HawkWing**.

- **HawkWing**: This is the client/server application where users define application service level objectives, called intents. HawkWing is also responsible for gathering the segment list from the HawkEye controller and encapsulating it into the appropriate packets.

- **HawkEye**: This controller calculates the path based on the user-defined intents and translates it into a segment list. HawkEye continuously monitors the network and returns an adjusted segment list as needed to ensure that the intents are always met.

By using these components, HawkV6 ensures that application traffic is dynamically steered over the best possible path without requiring manual configuration.

## Interacting with HawkV6

<p align="center">
  <img src="/img/Hawkv6-Intent-Interaction.drawio.svg" alt="HawkV6 Workflow">
</p>

Users can define their intents, and the rest is handled by the application.

1. **Define Intents:** The user defines the HawkWing configuration, specifying the desired intents for the application. 
2. **Path Request:** The HawkWing application sends a path request, including the specified intents, source, and destination addresses, to the HawkEye controller.
3. **Intent Translation and Path Calculation:** The HawkEye controller translates these intents, calculates the optimal path, and maps the path to the corresponding segments. It also saves the session for possible updates in the future.
4. **Segment List Delivery:** The HawkEye controller returns the path result, including the segment list, to HawkWing.
5. **Packet Encapsulation:** HawkWing encapsulates each matching application packet with the Segment Routing Header (SRH), ensuring the packets follow the intended path.
6. **Continuous Network Monitoring:** The network continuously sends updates, which the HawkEye controller receives and processes.
7. **Recalculation and Adjustment:** The HawkEye controller triggers a recalculation based on received network and service updates and sends an updated segment list to the HawkWing application if necessary to adjust the packet routing accordingly.


## Repositories
The HawkV6 project comprises several key components:

| Repository | Description |
| --- | --- |
| [HawkEye](https://github.com/hawkv6/hawkeye) | Controller application that translates path requests with intents into segment lists, ensuring the intents are always fulfilled. |
| [HawkWing](https://github.com/hawkv6/hawkwing) | Client/Server application that turns intents into requests, sends them to the controller, and encapsulates the segment list into the appropriate packets. |

Additional repositories that support the HawkV6 project:

| Repository | Description |
| --- | --- |
| [network](https://github.com/hawkv6/network) | Virtual containerlab SRv6 test network. |
| [generic-processor](https://github.com/hawkv6/generic-processor) | Generic processor to complement the standard [Jalapeno](https://cisco-open.github.io/jalapeno/) processors. |
| [clab-telemetry-linker](https://github.com/hawkv6/clab-telemetry-linker) | Enriches telemetry messages with the applied impairments in containerlab. |
| [deployment](https://github.com/hawkv6/deployment) | HawkV6 Deployment Guide, showing how to deploy the necessary elements. |
| [proto](https://github.com/hawkv6/proto) | Protobuf API definition used for communication between HawkEye and HawkWing. |
