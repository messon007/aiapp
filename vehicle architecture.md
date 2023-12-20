## Vehicle System Architecture
In this vehicle, the system architecture is divided into hardware architecture and software architecture.

### Vehicle Hardware Architecture
In this vehicle, there are several physical ECUs which can be used to deploy software component. 
There physical ECUs are: HU, BCM, RoofLight. 
The physical connection between physical ECUs are: HU is connected with BCM by Ethernet. BCM is connected with RoofLight by IO.
The software signals transfered over the physical connection will be defined in communication matrix. 
The communication matrix will be defined in Vechicle Software Architecture section and will be described later.

### Vehicle Software Architecture
SOA(service oriented architecture) is designed as software architecture for this vehicle. 
In SOA, there are still three layers(same as AUTOSAR CP), the bottom layer is BSW, the middle layer is ADP, the upper layer is ASW.
The software components defined in BSW are still AUTOSAR SWC and they are mainly worked to control hardware such as IO, the detail components in BSW will be described later.
The software components defined in ADP are still AUTOSAR SWC  and they are mainly worked to adapt BSW signal to ASW signal, the detail components in ADP will be described later.
Many software components defined in ASW are called service, but there are still some traditional Autosar SWC which can not migrated to service due to some limitation.
Signal is used to communicate between software components which may be deployed in different physical ECUs or same physical ECUs.
The communication matrix define all signals between physical ECUs.
The signals used to communicate between different software components is waiting to be designed.
The signal flow in BCM will follow the layered architecture common rules: 
* All incoming signals will arrive ASW software component through BSW software component and then ADP software component.
* All outgoing signals will be sent out by BSW software component through ASW software component and then ADP software component.
The software components defined in HU and RoofLight is not cared and the signal flow in HU and RoofLight is also not cared.

#### Communication Matrix Information
1. There are three signals defined between HU and BCM:
   - signal 'OpenRoofLight' and 'CloseRoofLight' are sent from HU to BCM.
   - signal 'RoofLightStatus' is sent from BCM to HU.
2. There are two signals defined between BCM and RoofLight:
   - signal 'ControlCommand' is sent from BCM to RoofLight.
   - signal 'LightStatus' is sent from RoofLight to BCM.
     
#### Software Components defined in BCM's BSW layer
1. 'IOInOut' is software components used to control IO and read IO status.
2. 'EthReceiver' is used to receive incoming request from Ethernet.
3. 'EthSender' is used to send out response to Ethernet.

#### Software Components defined in BCM's ADP layer
1. 'SOAFrame' is used to forward signals from BSW to ASW and from ASW to BSW.

#### Software Components designed in BCM's ASW layer
1. All software components deployed in BCM physical ECU are SOA service.
2. All services will process incoming control request, handle it according to service-specific processing logic (such as send request to other ECU by IO etc), send out response at last.
3. The specific services will be described in following section.

##### RoofLight Service
1. Car user can control RoofLight by touching HU screen.
2. RoofLight Service is deployed in BCM's ASW layer as a SOA service.
