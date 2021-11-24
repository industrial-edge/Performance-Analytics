# Configuration Steps

- [Configuration steps](#configuration-steps)
- [Configure PLC project in TIA Portal](#configure-plc-projectin-tia-portal)
- [Configure PLC connections in Industrial Edge](#configure-plc-connectionsin-industrial-edge)
  - [Configure Databus](#configure-databus)
  - [Configure S7 Connector](#configure-s7-connector)
- [Configure Data Service](#configure-data-service)
  - [Configure the adapter](#configure-the-adapter)
  - [Configure an asset with variables](#configure-an-asset-with-variables)
- [Configure Performance Insight](#configure-performance-insight)
  - [Defining limits](#defining-limits)
  - [Show step time analysis](#show-step-time-analysis)
  

## Configure PLC project in TIA Portal
This use case contains a TIA project which simulates the process. The project also inclundes a HMI visualization to operate the demonstration process. Download the TIA Portal project [here](src/StepTimeAnalysis.zip). The first steps are to configure the PLC project and the intruduction into the HMI screens.

1.	Open TIA portal and open the project containing the car production application (Adapt the PLC type and IP addresses to your system for each PLC and HMI)

![TIA_IP_Adress](graphics/TIA_IP_Adress.png)

2.	Download the PLC program to the PLCs and set the PLCs into RUN
3.	Open the HMI to control the car production application

![HMI Overview](graphics/HMI_overview.png)

Global Screen:
* Switch between automatic and manual mode of the stations
* Select which car type should be produced
* See which car type is actually in production in each station
* Check status of the stations
* See the calculated and measured production time for each car type
* Start and stop the sequential control system in the stations
* Switch to the screens for every station 

![HMI Stationview](graphics/HMI_stationview.png)

Station Screen:
* Switch between automatic and manual mode for the selected station (Only when status is Idle)
* Select the car type with the dropdown menu in manual mode
* After selecting the car type start the sequential control
* Stop and reset the sequential control
* See the status of the station
* See the car type in the station in automatic mode
* Switch to the delay select screen ("Simulate values")

![HMI Delayselect](graphics/delay_select.png)

Delay Select Screen:
* Reachable via button “Simulate values” on each station
* Select which step time should be delayed
* When the step is selected, a random time between 0 and 10 seconds is added to the step

## Configure PLC Connections in Industrial Edge

We are now switching to the Edge part of this use case. Each of the following steps is done in the Industrial Edge system. We use the S7 Connector at the Edge side to read data from the PLCs and provide the data. The data from the PLC are transferred via OPC UA, S7 and S7+. The data is sent via the S7 connector to the Databus, where the Data Service can use the information. In order to build this infrastructure, these apps must be configured correctly:

* Databus
* S7 Connector

### Configure Databus

Open the Industrial Edge Management App and launch the Databus configurator.

When the configurator is open, add a user with the topic: `ie/#`. In this use case we use the credentials "edge" / "edge". The credentials can be chosen freely but must be the same in all system apps.

![Databus_User](graphics/add_user.png)

![Databus_Configuration](graphics/databus_configuration.png)

Deploy the configuration.

### Configure S7 Connector

Open your Management App and launch the S7 Connector configurator.

Add a new data source for PLC1 with the OPC UA connector:

![S7 PLC1](graphics/S7_Connector_PLC1.png)

Add the needed tags. This can be done by browsing or adding them manually:

The "active" variables of the individual steps are those that are in DB_HMI and named with "DB_HMI"."ARG1_Seq1_S1" to "DB_HMI"."ARG1_Seq1_S19". This variables indicates if the respective step is active right now. Also add the String variable for the product "DB_Process_Var"."Car_Type_inProduction_Text".

![S7 PLC1 Data](graphics/S7_Connector_PLC1_Data.png)

Add a second data source for PLC2 also with the OPC UA connector:

![S7 PLC2](graphics/S7_Connector_PLC2.png)

Add the needed tags for PLC2 in the same way. Add the tags for the steps and the tag for the product.

The third PLC is added as a data source with the following parameters with the S7 Connector:

![S7 PLC3](graphics/S7_Connector_PLC3.png)

Also add the same tags from PLC3. Tag browsing also works with the S7+ protocol or add the tags manually.

PLC4 and PLC5 are used as data sources with the S7 protocol:

![S7 PLC4](graphics/S7_Connector_PLC4.png)
![S7 PLC5](graphics/S7_Connector_PLC5.png)

Add for these PLCs the tags respectively. With the S7 classic protocol it is only possible to add the tags manually.

Edit the settings:

![S7 Settings PW](graphics/S7_Connector_PW.png)

Hint: Username and password should be the same as was set in the IE Databus configuration, e.g., "edge" / "edge".

Deploy the project and start it.


## Configure Data Service
Steps are created for an asset as aspects in the data service. An asset represent the stations and for each asset the aspects represents the steps. 

![Dataservice Structure](graphics/Dataservice_Struktur.jpg)

Performance Insight will use this structure of assets and aspects in the Data Service. Open the web interface of your IED and launch the Data Service app. 

### Configure the adapter

Select the available "adapters" on the left and choose the SIMATIC S7 Connector. Click the edit icon on the right to open the adapter configuration.

![Dataservice Adapter Configuration](graphics/Dataservice_Adapter_Configuration.png)

Add the missing entries for username and password (again "edge"/"edge") and save it.

### Configure an asset with variables

Click on the icon "Assets & Connectivity" on the left bar. Add a child asset for the main "edge" asset. Into this child asset add 5 subassets for the stations.

![Dataservice_Assets](graphics/Dataservice_Assets.png)

Create an aspect for every step. The first step of each branch (step 2 and step 11) must be configured as initial step. This is necessary to mark the beginning of the sequence and to link the corresponding product for the branch.

First step of the branch:

![Dataservice_Aspects1](graphics/Dataservice_aspect1.png)

Following steps of the branch:

![Dataservice_Aspects2](graphics/Dataservice_aspect2.png)

Link the variables that have been created by adding the aspects to the corresponding S7 Connector tags.

![Dataservice_Aspects3](graphics/Dataservice_aspect3.png)

Repeat this process for every station.

![Dataservice_Aspects4](graphics/Dataservice_aspect4.png)

## Configure Performance Insight

After finishing the configuration of the Data Service, open the Performance Insight application on the IED. With this appliation it is possible to get information about the duration of defined steps and observe limits of individual steps and sequences.

The asset structure that was created in Data Service can also be found in Performance Insight. The next step is to specify the limits for each step in the asset configuration.

### Defining Limits

If no Step time analysis has yet been configured in Performance Insight, the "Define Limits" button is visible. Click on the button.

![Performance Insight Setting Icon_1](graphics/PerformanceInsight_Settings_icon_1.png)

To change the limits for the steps in the sequential control system, click on the gear icon on the right.

![Performance Insight Setting Icon](graphics/PerformanceInsight_Settings_icon.png)

Choose a product from the list of available products. Click on the gear icon of the product. 

A list with all steps of this product is displayed. Open the dropdown menu with the text "Apply to all step limits". Specify a percentage (e.g. 5%) that is added to the initial value and click Apply. A limit is calculated for all steps based on the respective limits and entered in the "Planned step time limit" column.

![Performance Insight Set Limit](graphics/PerformanceInsight_setLimit.png)

The time limits are set in the fields. Click the "Save" button.

![Performance Insight Set Time](graphics/PerformanceInsight_setTime.png)

### Show step time analysis

When you have created steps for the asset in the Data Service and when you have defined the limits then the step time analysis is automatically 
displayed in the "Step time analysis" dashboard.

With the help of the "Overview" screen you can get all information about the sequences of a specific product for a specified time period. When the step is gray the step time is within the defined limits. A step displayed in red is outside the defined limits.

![Performance Insight Overview](graphics/PerformanceInsight_Overview.png)

The analysis overview is displayed in the "Step time analysis" dashboard with the following options:
* Switching to the trend view
* Displaying the number of faulty sequences
* Execution time of the faulty sequences
* Selecting a product for which the step time analysis is to be displayed
* Selecting a time period for which the step time analysis is to be displayed
* Downloading a report in CSV format
* Switching to the limit definition in the Asset Configuration
* Displaying the steps with highest fault rate
* Sequence overview: Display and selection of a specific sequence for detailed display
* "Show all sequences"
* Sequence details: Displaying all sequences in the selected time period and defined steps. When selecting a single step, the Trend view of the step opens.
