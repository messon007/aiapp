## Service Software Architecture
### Communication Matrix Information
1. HU is connected with BCM by Ethernet. BCM is connected with RoofLight by IO.
2. There are three signals defined between HU and BCM:
   - OpenRoofLight
   - CloseRoofLight
   - RoofLightStatus

### Service Frame Base Information
1. All software components deployed in BCM are SOA service.
2. SOA service will process incoming control request, handle it according to service-specific processing logic (send request to other ECU by IO etc), send out response at last.
3. Two common software component are deployed in BCM and they are used to communicate with HU. These two components are: EthReceiver and EthSender.
4. EthReceiver is used to receive incoming request from HU and EthSender is used to send out response to HU.

### RoofLight Service
1. Car user can control RoofLight by touching HU screen.
2. RoofLight Service is deployed in BCM as a SOA service.
