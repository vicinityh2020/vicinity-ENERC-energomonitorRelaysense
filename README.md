# Vicinity-ENERC-energomonitorRelaysense

The adapter bridges communication with the Energomonitor Relaysense sensors which will be installed at the Martim Longo Municipal Cluster. This adapter will get data from the sensors (water consumption) and make it available to Vicinity. This data will be used by the "Smart School" and "Dynamic Audit" Value-Added Service (VAS). 

# 1. Infrastructure Overview
This is a Vicinity Adapter for ENERC Pilot Infrastructure. It is used to describe the Relaysense sensors from Energomonitor which will be deployed at the mentioned facilities and connected to Energomonitor Cloud Service.

# 2 - Configuration and deployment

## Requirements
- JDK 1.8 or higher
- Node Red v0.18

## Device Specific Information
The Relaysense sensor collects data every X minutes and sends it to the Energomonitor Homebase which then sends data to the Energomonitor Cloud Platform. Then the Energomonitor API can be used to retrieve data from the Energomonitor Cloud platform to a Raspberry Pi that will act as a Vicinity Gateway and make the adapter to run locally.

The Raspberry Pi located in the SolarLab and/or School and running Raspbian with Node-Red will perform the following actions:
	1. Every X seconds a Node Red trigger node triggers an HTTP Request node which gets data from the Energomonitor Cloud platform
	2. Gathered information is parsed and made available to Vicinity
	3. A function node takes values and performs Smart School and Dynamic Audit VAS Logic
	4. Dashboard nodes will be used to build an initial version of the VAS UI

This same Raspberry Pi will be running Vicinity Gateway and Agent. An HTTP Request Node on NodeRed will be able to make GET and POST Requests to Vicinity.

# 3 - Functionality and API

## Endpoints
- GET /objects (optional): Retrieve all devices Thing Descriptions (TDs) for registration to VICINITY. This functionality is optional since auto-registration of devices will be performed.
- GET /objects/{oid}/properties/{pid} - Returns last known value and time the value was received by the device. {oid} is UUID of device and {pid} is a property identifier.

## Functions
- Send device TD to the Vicinity Agent at Start Up
- Publish every new measurement to a specific Vicinity event topic.

