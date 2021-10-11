# Configuration Steps

- [Configuration steps](#configuration-steps)
- [Configure PLC project](#configure-plc-project)
- [Configure PLC Connections](#configure-plc-connections)
  - [Configure Databus](#configure-databus)
  - [Configure S7 Connector](#configure-s7-connector)
- [Configure Data Service](#configure-data-service)
  - [Configure the adapter](#configure-the-adapter)
  - [Configure an asset with variables](#configure-an-asset-with-variables)
- [Configure Performance Insight](#configure-performance-insight)
  - [Configure a dashboard](#configure-a-dashboard)
  

## Configure PLC project
1.	Open TIA portal and open the project containing the car production application
2.	Download the PLC program to the PLCs and set the PLCs into RUN
3.	Open the HMI to control the car production applikation

## Configure PLC Connections

We use S7 Connector to read data from the PLCs and provide the data. The data from the CPU are transferred via OPC UA, S7 and S7 +. The data is sent via the S7 connector to the Databus, from where the Data Service can use the data. In order to build this infrastructure, these apps must be configured correctly:

* Databus
* S7 Connector

### Configure Databus

Open the IEM and launch the Databus configurator.
When the configurator is open, add a user with the topic: `ie/#`

![Databus_User](graphics/add_user.png)

![Databus_Configuration](graphics/databus_configuration.png)

Deploy the configuration.

### Configure S7 Connector

## Configure Data Service

### Configure the adapter

### Configure an asset with variables

## Configure Performance Insight

### Configure a dashboard
