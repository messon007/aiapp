## Service Software Architecture

### RoofLight Service
1. HU is connected with BCM by Ethernet, BCM is connected with RoofLight by IO. People can interact with Car by touching HU screen.
2. Two common software component are deployed in BCM and they are used to communicate with HU. These two components are: EthReceiver and EthSender.
3. RoofLight Service is deployed in BCM as a SOA service.
