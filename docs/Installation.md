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
  - [Defining Limits](#defining-limits)
  - [Show step time analysis](#show-step-time-analysis
  

## Configure PLC project
1.	Open TIA portal and open the project containing the car production application (Adapt the IP addresses to your system)

![TIA_IP_Adress](graphics/TIA_IP_Adress.png)

2.	Download the PLC program to the PLCs and set the PLCs into RUN
3.	Open the HMI to control the car production applikation

![HMI Overview](graphics/HMI_overview.png)

Global Screen:
* Switch between automatic and manuel mode of the stations
* Select which car typ should be produce
* See which car typ is actually in production in each station
* Check Status of the stations
* See the calculated and measured production time for each car type
* Start and stop the stepper sequence in the stations
* Switch to the screens for every station 

![HMI Stationview](graphics/HMI_stationview.png)

Station Screen:
* Switch between automatic and manuel mode for the selected station ( Only when status is Idle)
* Select the car typ with the dropdown menu in manuel mode
* After selecting the car typ start the stepper sequence
* Stop and reset the stepper sequence
* See the status of the station
* See the car typ in the station in automatic mode
* Switch to the delay select screen ("Simulate values")

![HMI Delayselect](graphics/delay_select.png)

Delay Select Screen:
* Reachable via button “Simulate values” on each station
* Select which step should be delay
* When the step is selected, a random time between 0 and 10 seconds is added to the step

## Configure PLC Connections

We use S7 Connector to read data from the PLCs and provide the data. The data from the CPU are transferred via OPC UA, S7 and S7 +. The data is sent via the S7 connector to the Databus, where the Data Service can use the data. In order to build this infrastructure, these apps must be configured correctly:

* Databus
* S7 Connector

### Configure Databus

Open the IEM and launch the Databus configurator.

When the configurator is open, add a user with the topic: `ie/#`

![Databus_User](graphics/add_user.png)

![Databus_Configuration](graphics/databus_configuration.png)

Deploy the configuration.

### Configure S7 Connector

Open the S7 Connector in your IEM and launch the configurator.

Add a new data source for PLC1:

![S7 PLC1](graphics/S7_Connector_PLC1.png)

Add the needed tags:

The "active" variables of the individual steps are those that end with "_x".


Edit the settings:

![S7 Settings PW](graphics/S7_Connector_PW.png)

Hint: Username and password should be the same for all system apps, e.g. "edge" / "edge".

Deploy the project and start it

## Configure Data Service

Open the web interface of your Edge Device and launch the Data Service app. 

### Configure the adapter

Select the available "adapters" on the left and choose the SIMATIC S7 Connector. Click the edit icon on the right to open the adapter configuration.

![Dataservice Adapter Configuration](graphics/Dataservice_Adapter_Configuration.png)

Add the missing entries for username and password (again "edge"/"edge") and save it.

### Configure an asset with variables

Click on the icon “Assets & Connectivity” on the left bar. Add an child asset for the main “edge asset”.

## Configure Performance Insight

### Configure a dashboard

### Defining Limits

### Show step time analysis
