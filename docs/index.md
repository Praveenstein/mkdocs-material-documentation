# Introduction

**Project Overview: Manufacturing Data Management**

This project focuses on streamlining data management in manufacturing plants. It aims to achieve the following:

1. **Data Collection:** Develop a system to gather data from manufacturing machines.

2. **Real-time Analytics:** Provide real-time statistics on production processes.

3. **Documentation Integration:** Seamlessly integrate document management for manufacturing.

4. **Open-Source and Interoperable:** Use open-source technology and standards for compatibility.

5. **Security:** Implement strong security measures for data protection.

This project aims to improve manufacturing efficiency and facilitate data sharing among companies. Feel free to ask for more details on any of these aspects.

## Requirements of the Project

The project requirements are:

- **Machine Maintenace** - Machines (General purpose machines such as cnc and special purpose machines such as laser cladding) need to monitored for any abnormal conditions.

- **Real Time Data Visualization Feature** - A graphical way to visualize the data from all these machines.

- **Spare Part Management** - A system to monitor part count of machines and alerts system to notify maintenace team when a part of a machine needs to be replaced (which is monitored from a critical limit for the part).

- **Alarm Management** - A system to generate a summary of alarms for machines.

- **Email Alerts & Report Generation** - A system to send email alerts when a machine is in abnormal state and to generate summart report of machines under abnormal states.

## Nature of the Current System at CMTI Smart Manufacturing Demo and Development Cell ( SMDDC)

The following table gives the summary of available machines at CMTI's SMDDC:

| S.No 	| Machine Name           	| Type           	| Description                                                              	| Brand                          	| Model            	| Location* 	| Controller Name 	| Controller Model 	| Legacy 	| Ip Address  	|
|------	|------------------------	|----------------	|--------------------------------------------------------------------------	|--------------------------------	|------------------	|----------	|-----------------	|------------------	|--------	|-------------	|
| 1.   	| Ace LT-2               	| Turning Center 	| 2-axes horizontal turning centres                                        	| Ace Micromatic                 	| LT-2-LM-500-PLUS 	| R1       	| Fanuc           	| 0i tf plus       	| No     	| 172.18.30.158 	|
| 2.   	| MONO 200               	| Turning Center 	| MONO-200 is a CNC turning center machine                                 	| Mac Power                      	| Mono 200         	| R2       	| Seimens         	| sinumerik 828d   	| No     	| 172.18.28.35 	|
| 3.   	| AMS MCV - 450          	| Milling Center 	| It's vertical machining center, It has a Fanuc 0i-MF plus CNC controller 	| AMS(ACE MANUFACTURING SYSTEMS) 	| MCV - 450        	| R3       	| Fanuc           	| 0i - Mf Plus     	| No     	| 172.18.30.147 	|
| 4.   	| Mazak - H-400 N        	| Milling Center 	| Mazak H-400N is a horizontal machining center with a Seimens Controller  	| Mazak                          	| H-400N           	| R4       	| Seimens         	| sinumerik 828D   	| No     	| 172.18.30.149 	|
| 5.   	| Mazak - H-400 N        	| Milling Center 	| Mazak H-400N is a horizontal machining center with a Fanuc Controller    	| Mazak                          	| H-400N           	| L4       	| Fanuc           	| 0i -md           	| TBA    	|             	|
| 6.   	| Hmt - vtc 800, seimens 	| Milling Center 	|                                                                          	| HMT                            	| VTC - 800        	| L3       	| Seimens         	| TBA              	| Yes    	|             	|
| 7.   	| Schaublin 33 cnc       	| Milling Center 	|                                                                          	| Schaublin Machines SA          	| 33 CNC           	| L2       	| Seimens         	| 840D             	| Yes    	|             	|
| 8.   	| Hmt Stallion 200       	| Turning Center 	|                                                                          	| HMT                            	| Stallion         	| L1       	| Fanuc           	| ot - Series      	| Yes    	|             	|

 *The location should be viewed, as if the person is standing in SMDDC facing the main exit/entrace gate, so that NMTC building is on the left side.


## Features of the Project

The final product will be a web application with the following features:

- **KPI Dashboard** - This page of the web application will show the KPIs such as oee, availability, performance and quality for individual machines and factory.
- **Real Time Data Visualization Feature** - This page of the web application will display time series data for a given machine, for a given parameter group, for a given axis within a given time range.

- **Alarm Management Feature** This page of the web application will display the summary of alarms and events for a given machine, during a given period of time range.

- **Spare Part Management Feature** This section of the web application will have information about the part count of machines, and information about the parts that needs to be replaced when a critical part limit is reached.

- **Special Purpose Machines Feature** This section of the web application will real time visualization of its parameters over a given range of time.

Apart from the web application, the final project solution should include the following services:

- **4/8 Hour Summary Report Generation Service** - A Service which generates a summary of machines that were under abnormal states for every 4/8 hour.
- **Email Alerts Service** - A Service which sends email alerts as soon as a machines goes to abnormal state.