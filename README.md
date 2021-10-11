# Anchor-Use-Case-Plug-and-Analyze 

Bellow you can find the structure of IE tow-to/tutorial

* [Writing good how-to or tutorial](#writing-good-how-to-or-tutorial)
  * [Description](#description)
    * [Overview](#overview)
    * [General Task](#general-task)
  * [Requirements](#requirements)
    * [Prerequisites](#prerequisites)
    * [Used components](#used-components)
  * [Installation](#installation)
  * [Usage](#usage)
  * [Documentation](#documentation)
  * [Contribution](#contribution)
  * [Licence and Legal Information](#licence-and-legal-information)

## Description

### Overview
This use case shows how to monitoring the production cycles of a discrete manufacturing process with identification of delayed process steps which allows localization the root cause.

![overview](docs/graphics/overview.png)

### General Task

This sample application based on five S7-1500 PLCs to control the manufacturing process of a car. A stepper sequence that was implemented with the TIA Portal Tool “Graph” runs on each PLC. The Industrial Edge Device shall be connected to PLC 1 + 2 via OPC UA, to PLC 3 via S7+ and to PLC 4 + 5 via S7 using the Essential Edge App “S7 Connector”. For each implemented step the connectivity shall provide a tag that carries the step activity status. For each stepper sequence an asset model with the activity status needs to be configured and aligned with the related status tags. The option “Cycle Time Analyses” of the Edge App “Performance Insight” needs to be aligned with the asset model that represents the implemented stepper sequences in order to assign a reference duration for each step. The dash boards of the Edge App “Performance Insight” compares the configured and measured duration which allows localizing the steps that are causing delays.

## Requirements

### Prerequisites

*	Onboarded Industrial Edge Device on Industrial Edge Management
*	Installed system configurators
*	Installed system applications
*	Installed Performance Insight 
*	Edge device is connected to PLC
*	TIA portal project downloaded to PLC

### Used components

*	TIA Portal V16
*	PLC1: CPU 1518F-4 PN/DP FW 2.8
*	PLC2: CPU 1518F-4 PN/DP FW 2.8
*	PLC3: CPU 1517TF-3 PN/DP FW 2.8
*	PLC4: CPU 1517F-3 PN/DP FW 2.8
*	PLC5: CPU 1517TF-3 PN/DP FW 2.8
*	HMI: TP900 Comfort
*	Industrial Edge Device V 1.XX
*	SIMATIC S7 Connector V 1.XX
*	SIMATIC S7 Connector Configurator V 1.XX
*	IE Databus V 1.XX
*	IE Databus Configurator V 1.XX
*	Performance Insight V 1.3


## Installation

You can find the further information about the following steps in the [docs](docs/installation.md)
*	Configure PLC projects
*	Configure PLC Connections
  *	Configure Databus
  *	Configure S7 Connector
*	Configure Data Service
  *	Configure the adapter
  *	Configure an asset with variables
*	Configure Performance Insight
  *	Configure a dashboard


## Usage

As soon as the program has been transferred to the PLCs and the edge system has been configured with performance insight, the process can be started. The car to be produced can be selected via the HMI. An HMI picture can be called up for each station. There you can see an overview of the step chains that are executed on the CPU. With the help of the button "Simulate values" the steps in each station can be extended with the help of a randomly generated value.

![usage](docs/graphics/delay_select.png)

If there is a delay in any of the steps, it will be visible in Performance Insight. With the help of Performance Insight, it can then be found out which step has led to the planned production duration and the measured production duration being different.
## Documentation

You can find further documentation and help in the following links

* [Industrial Edge Hub](https://iehub.eu1.edge.siemens.cloud/#/documentation)
* [Industrial Edge Forum](https://www.siemens.com/industrial-edge-forum)
* [Industrial Edge landing page](https://new.siemens.com/global/en/products/automation/topic-areas/industrial-edge/simatic-edge.html)
* [Industrial Edge GitHub page](https://github.com/industrial-edge)

## Contribution

Thank you for your interest in contributing. Anybody is free to report bugs, unclear documentation, and other problems regarding this repository in the Issues section. Everybody is free to propose any changes to this repository using Pull Requests.

## Licence and Legal Information

Please read the [Legal information](LICENSE.md).
