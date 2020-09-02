# **Storage Battery Device**

- required:
	- location
	- dateLastReported
	- batteryType
	- rechargeEnergySource
- type: "object"
	- allOf:
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description

The Data Model is intended to describe the technical characteristics of the battery and the charging and discharging conditions of the energy.
The charging functionalities apply from a power source which can be an "on-board system, solar panel, wind turbine, generator, power supply". Hydraulic sources are not included in this version.
The discharge functions apply to all types of system requiring energy consumption from a storage battery. 

*Additional Information about this data Model :*
This Data Model can be used directly as a main entity to describe the Device [STORAGEBATTERY] or as a sub-entity of the Data Model [DEVICE] using a reference by the `refDevice` attribute.

## Data Model

- properties:

	### Common parameters for data identification.

	- id:
		- x-ngsi:
			- type: "Property"
			- type : "string"
		- Description: "mandatory element for NGSI"
		- format: "uri"
	- type:
		- x-ngsi:
			- type: "Property"
		- Description: "Entity type, mandatory element for NGSI"
		- type : "string"
		- value: "StorageBatteryDevice"
	- dataProvider:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/URL"
		- description: > Specifies the URL to information about the provider of this information
		- type: "string"
			- format: "URL"
	- source:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text", "https://schema.org/URL"
		- description: > A sequence of characters giving the source of the entity data.
		- type: "string"
	- name:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/name"
		- description: > Name given to the observation.
		- type: "string"
	- alternateName:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/alternateName"
		- description: > Alternative Name given to the observation
		- type: "string"
	- description:
		- x-ngsi:
			- type: "Property"
			- model: "https://uri.etsi.org/ngsi-ld/description", "https://schema.org/description"
		- description: > Description of the observation.
		- $ref: 'https://jason-fox.github.io/swagger-datamodel-test/common.yaml#/Description'
	- seeAlso:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text", "https://schema.org/URL"
		- description: > Text or Link that can provide additional information.
		- type: "string"

	### Information about Location and Address.

	- location
		- x-ngsi:
			- type: type: "Geo Property".
		- $ref: "https://github.com/smart-data-models/data-models/blob/master/common-schema.yaml#/Geometry"
		- description: > Location represented by a GeoJSon geometry [Point, LineString, Polygon, MultiPoint, MultiLineString, MultiPolygon]
	- address:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/address"
		- description: > Civic Address
		- $ref: "https://github.com/smart-data-models/data-models/blob/master/common-schema.yaml#/Address"
	- areaServed:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Zone of level higher to the attributes Location & Address to gather and cross information (ex district, etc)
		- type: "string"

	### Information related to the date of last reporting

	- dateLastReported:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > A timestamp which denotes the last time when the device successfully reported data. Date and time in an ISO8601 UTCformat.
		- type: "string"
			- format: "date-time"

	### Information about a reference to other Data Models.

	- refDevice : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to the Main Entity [Device](https://github.com/smart-data-models/dataModel.Device/blob/master/Device/doc/spec.md) if used as second link.  
		- type: "string"
			- format: "URL"
	- refPointOfInterest : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a [PointOfInterest](https://github.com/smart-data-models/dataModel.PointOfInterest/blob/master/PointOfInterest/doc/spec.md) linked with the observation 
		- type: "string"
			- format: "URL"

	### Information related to the model 

	- brandname:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/brand"
		- description: > Brand Name.
		- type: "string"
	- modelName:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/model"
		- description: > Model Name.
		- type: "string"
	- manufacturerName:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/manufacturer"
		- description: > Manufacturer Name.
		- type: "string"
	- serialNumber:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/serialNumber",
		- description: > Serial numbers.
		- type: "number"
	- application:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Target application of the Device regarding the storage. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- electricMobility, energyStorage, emergencyStorage, lighting, industrialStorage, houseHoldStorage, robotics, production, other
	- typeOfUse :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Accepted use regarding its positioning in an indoor / outdoor environment. A unique value of :
		- type: "string"
		- enum : 
			- indoor, outdoor, mixed, other
	- instalationMode:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Positioning of the device in relation to a ground reference system. A unique value of :
		- type: "string"
		- enum : 
			- ground, underGround, aerial, wall, pole, roofing, other
	- instalationCondition:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Condition and possibility of use in the following environments. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- extremeHeat, extremeCold, extremeHumidity, extremeClimate, desert, sand, marine, saline, dust, seismic, other
	- possibilityOfUse:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Possibility of use. A unique value of :
		- type: "string"
		- enum : 
			- stationary, mobile, mixed, other
	- documentation:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text", "https://schema.org/URL"
		- description: > Technical Documentation (Installation / maintenance / used).
		- type: "string"
	- owner:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text" included references to "http://schema.org/Person", "https://schema.org/Organization", "https://schema.org/URL".
		- description: > The owners of the Device. A list of [Text], [Person], [Organisation] or [URLs].
		- type: "array"
			- items:
				- type: string

	### Information related to type of battery

	- batteryType:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Type of battery used. A unique value of :
		- type: "string"
		- enum : 
			- lead, lead-AGM, Ni-Cd, Ni-MH, Ni-Zn, Na-NiCl2(Zebra), alkaline, Li-Ion, Li-Po, Li-Po4, LMP, Li-Air, gel, other

	- rechargeEnergySource:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Recharge Energy Source. A unique value of :
		- type: "string"
		- enum : 
			- electric, hydraulic, windTurbine, other

	- typeEnergySource:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Type of Energy Source regarding `RechargeEnergySource` attribute. A combination of :
		- type: "array"
			- Items:
			- type: "string"
				- enum : 
					- for `electric` : network, photovoltaic, generator, other
					- for `hydraulic` : sea, river, dam, fall, waterTurbine, other 
					- for `windTurbine` : wind, other

	### Information related to Mechanical Data 

	- dimension : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > External dimension of a Panel. The format is structured by a sub-property of 3 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **CMT** represents Centimeter.
		- type: "number"
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items:
				- width
				- height
				- depth
	- weight :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Weight. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **KGM** represents KiloGramme.
		- type: "Number"

	### Information about Security Classification

	- protectionIP :   
		- x-ngsi:
			- type: "Property"
			- model: [IP_Code/EN 60529](https://en.wikipedia.org/wiki/IP_Code),
		- description: > IP "*Ingress Protection*" for the Junction Box. This is the level classifies and rates the degree of protection provided by mechanical casings and electrical enclosures against intrusion, dust, accidental contact, and water according to International Electrotechnical Commission standard (EN 60-529).
			- First digit: Solid particle protection (Single numeral: 0–6 or "X"). 
			- Second digit: Liquid ingress protection (Single numeral: 0–9 or "X" ).
			- Third digit: Personal Protection  against access to dangerous parts (optional additional letter).
			- Fourth digit: Other protections (optional additional letter).
		- type: "string"
	- protectionIK :   
		- x-ngsi:
			- type: "Property"
			- model: [IP_Code/EN 60529](https://en.wikipedia.org/wiki/IP_Code),
		- description: > IK "*Mecanic Protection*" level relating to numeric classification for the degrees of protection provided by enclosures for electrical equipment against external mechanical impacts, according to International Electro technical Commission standard (EN 62-262).
			- IK varies from 0 (minimum resistance) to 10 (maximum resistance) which represents an Impact Energy (Unit Joule)
		- type: "Number"

	### Information about Temperature Characteristics  

	- temperature :   
		- x-ngsi:
			- type: "Property"
			- model: [IP_Code/EN 60529](https://en.wikipedia.org/wiki/IP_Code),
		- description: >  This is the nominal reference temperature (25° `CEL` normally) for the calculation of all measurements. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **CEL** represents Degree Celsius.
		- type: "Number"
		- The `temperature` is used as reference for the following sections. 
			- *Nominal Value*
			- *Life of the battery*
			- *Discharge Measurements*
			- *Power Measurements during Charge and Discharge*
			- *Volt Measurement during Charge and Discharge*
	
	- operatingTemperature : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Ambient operating temperature range. This is the minimum and maximum resistance to cold and heat for an [event]. The format is structured by a sub-property of 3 items with the format  {`event`:[`min`,`max`]}. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **CEL** represents Degree Celsius.
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- charge
				- storage
				- discharge

	### Information related to the Nominal Value  

	- nominalVoltage : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Nominal battery voltage. *(Code U)* The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VLT** represents Volt.
		- type: "Number"
	- nominalAmpere : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Nominal Amperage. *(Code I)*. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **AMP** represents Ampere.
		- type: "Number"
	- nominalFrequency : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Nominal Frequency. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **HTZ** represents Hertz.
		- type: "Number"
	- nominalCapacity :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Nominal Energy capacity. *(Code C)* to link with the attribute [CapacityCnnn] to measure the predefined levels parameters C / xx h of discharge regimes. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **AMH** represents Ampere Hour.
		- type: "Number"
	- storableEnergy :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Total Storage Energy = [nominalVoltage] * [nominalCapacity]. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **KWH** represents Kilowatt Hour.
		- type: "Number"
	- UsableEnergy :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Usable Energy. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **KWH** represents Kilowatt Hour.
		- type: "Number"
	- OperatingVoltage :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Minimum and Maximum voltage allowed. The format is structured by a sub-property of 2 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VLT** represents Volt.
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- min
				- max
	- operatingAmpere :  
		- x-ngsi:
	   		- type: "Property"
	   		- model: "https://schema.org/Number",
	   	- description: > Minimum and Maximum Ampere allowed. The format is structured by a sub-property of 2 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **AMP** represents Ampere.
	   	- type: [StructuredValue](http://schema.org/StructuredValue)
	   		- type: string
	   		- items :
	   			- min
	   			- max
	- operatingFrequency : 
		- x-ngsi:
			- type: "Property"
	   		- model: "https://schema.org/Number",
	   	- description: > Minimum and Maximum frequency allowed. The format is structured by a sub-property of 2 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **HTZ** represents Hertz.
	   	- type: [StructuredValue](http://schema.org/StructuredValue)
	   		- type: string
	   		- items :
	   			- min
	   			- max
	- massEnergyDensity :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Mass Energy density *(Code D)*. Ratio between the capacity of the battery to deliver a certain power for a certain time and its weight. The format is structured by a sub-property of 2 items. The unit code (text) of measurement is **Wh/Kg** WattHour per Kilogram.
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- min
				- max
	- volEnergyDensity :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Voume Energy density *(Code D)*. The format is structured by a sub-property of 2 items. The unit code (text) of measurement is **Wh/L** WattHour per Liter.
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- min
				- max
	- maxOutputPower :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum Power.. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **KWT** represents Kilowatt.
		- type: "Number"
	- peakPower :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum intensity extractable over a short period. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **KWT** represents Kilowatt.
		- type: "Number"
	- durationPeakPower :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Reference Time recorded for the attribute [peakPower]. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **SEC** represents Second.
		- type: "Number"
	- communication :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > List of communication protocol with others device depending manufacturers. A combination of :
		- type: "array"
			- Items:
			- type: "string"
				- enum : 
					- CAN2.0B, RS485, RS485Inverter, RS485BMS, maintenanceInterface, dryContactterminal, other
	- operatingAltitude :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Operating altitude with minimum and maximum resistance to height and depth. The format is structured by a sub-property of 2 items with the keys [min] =<0 and [max] >=0. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **MTR** represents Meter.
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- min
				- max
	
	### Information about the life Cycle of the battery 
	
	- averageLife :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > average life under normal battery usage conditions at reference temperatures. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **ANN** represents Year.
		- type: "Number"
	- lifeCycleNumber :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
	   	- description: > Number of admissible charge / discharge life cycles. The format is structured by a sub-property of 2 items.
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- min
				- max
	- toolBMS :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Boolean"
		- description: > Use of a Battery Management System tool to protect, guarantee and optimize battery life. (`true` for yes) 
		- type: "Boolean"
	
	### Constraint on battery charges
	
	- chargingModeAllowed:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Charging mode permitted to avoid damage to the battery. A unique value of:
		- type: "string"
		- enum : 
			- normal, quick, fast
	- overloadAccepted :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Boolean"
		- description: > Overload is permitted after exceeding the threshold.(`true` for yes)
		- type: "Boolean"
	- overloadAcceptedTime :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > Accepted overcharge time without damage to the battery.
		- type: "Number"
	
	### Discharge Measurements
	
	- selfDischargeRate :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Battery discharge rate without any use on a baseline of 1 month according the [temperature of reference]. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percentage.
		- type: "Number"
	
	- CapacityCnnn : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Remaining energy as a function of the discharge time for 6 keys according the temperature of reference. Each Key is a structured value with the format {`Cnnn`:[`value1`,`value2`]} describing the different measurement of [CapacityCnnn].
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
				- Cnnn:  
					- x-ngsi:
						- type: "Property"
						- model : "http://schema.org/Text"
					- description: > Discharge reference time. `nnn` corresponds to the time spent since the start of discharge and without connection to a generator. 
					- type: string
						- enum : 
							- C001, C005, C010, C020, C050, C100
				- value1: 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Number"
					- description: > Remaining Capacity for the reference time `Cnnn` of discharge. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **AMH** represents Ampere Hour.
				- value2: 
					- x-ngsi:
						- type: "Property"
						- model: "http://schema.org/Number"
					- description: > Voltage reference for the reference time [Cnnn] of discharge. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VLT** represents Volt.
	
	### Power Measurements during Charge and Discharge 
	
	- roundTripEfficiency :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Round-Trip Efficiency. Efficiency, defined as the ratio between stored energy and returned energy. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percent.
		- type: "Number"
	- chargeDischargeReactivity :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Charge and Discharge Reactivity which characterizes the reactive behavior of the system. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **SEC** represents Second.
		- type: "Number"
	- chargePower : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Load Power. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VLT** represents Volt.
		- type: "Number"
	- chargeEfficiency :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Charge Efficiency *(code PV-BAT)*. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percent.
		- type: "Number"
	- maximumVoltageEOC : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum authorized voltage after end of charge and Battery still connected to to a charge generator. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VLT** represents Volt.
		- type: "Number"
	- dischargePower : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Discharge Power. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VLT** represents Volt.
		- type: "Number"
	- dischargeEfficiency :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Discharge Efficiency *(code PV-OND)*. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percent.
		- type: "Number"
	- minimunVoltageEOD : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Minimum voltage after end of discharge and not connected to to a charge generator. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VLT** represents Volt.
		- type: "Number"