<h1 align="center">Welcome to the HawkV6 Project</h1>

<p align="center">
HawkV6 provides developers, application managers, and sysadmins with an easy-to-use tool that enables end-to-end paths, meeting the specific requirements of each application.
</p>

## Problem
Today's networks are often overly complex and require extensive configuration. Enabling connectivity typically demands manual adjustments on network devices, often necessitating expert knowledge. Moreover, these networks lack the flexibility to adapt to the varying requirements of different applications. Networks are generally configured to deliver a best-effort service to all applications within a specific environment, which is not always ideal. Some applications require low latency, others demand high bandwidth, or high reliability with minimal packet loss. The network should be capable of adapting to these diverse application needs without constant intervention from network administrators.

## Solution
HawkV6 leverages Segment Routing over IPv6 (SRv6) and Intent-Based Networking to establish the desired end-to-end path between clients and servers based on specific application requirements. Users can define their intents, and the rest is handled by the application.

## How It Works
1. **Define Intents:** Users define the application's requirements (intents) such as low latency, high bandwidth, low packet loss, etc., in the HawkWing application.
2. **Intent Processing:** The HawkWing application sends these intents to the HawkEye controller.
3. **Path Calculation:** The HawkEye controller processes the intents and calculates the optimal path between the client and server, represented as a segment list.
4. **Packet Encapsulation:** The calculated segment list is sent back to HawkWing, which encapsulates it in the appropriate packets.
5. **Data Transmission:** The packets are transmitted between the client and server. On the server side, the segments are reversed and sent back after processing the application data.
6. **Continuous Monitoring:** HawkEye continuously monitors the network to ensure the intent is always met, adjusting the segment list as necessary.

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
