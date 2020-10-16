# **Photo-voltaic Measurements**

- required:
	- location
	- dateObserved
	- refPhotovoltaicDevice
	- dateEnergyMeteringStarted
	- temperature 
	
- type: "object"
  - allOf:
  	- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
  	- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description

The Data Model is intended to measured the continuous power transferred by the photo-voltaic panel to an Inverter Device.
For most of the attributes there are various ways they can be actually measured. For this purpose, the `measurementType` of the Meta Data Attribute can be used.
It can have following values :
	- instant.	From the specific instant of time
	- average.	The average of a time period
	- rms. 		The root mean square of a time period 
	- maximum.	The maximum of a time period 
	- minimum.	The minimum of a time period.
	
When using [average, rms, maximum, minimum] values another Meta Data attribute called `measurementInterval` should be used to give the length of the measurement period in Seconds. 
Also the `timestamp` Meta Data attribute should be the end time of the measurement period..

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
		- value: "PhotovoltaicMeasurement"
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

	### Information related to the date and period
	
	- dateObserved:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > Date and time of this observation represented by an ISO8601 UTC format. It can be represented by an specific time instant or by an ISO8601 interval to separate attributes `dateObservedFrom`, `dateObservedTo`.
		- type: "string"
			- format: "date-time"
	- dateObservedFrom:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > Observation period: Start date and time in an ISO8601 UTC format. The attribute can be used in addition to the `dateObserved` attribute when it corresponds to a time interval to be highlighted.
		- type: "string"
			- format: "date-time"
	- dateObservedTo:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > Observation period: End date and time in an ISO8601 UTC format. The attribute can be used in addition to the `dateObserved` attribute when it corresponds to a time interval to be highlighted.
		- type: "string"
			- format: "date-time"
	
	### Information about a reference to other Data Models.

	- refPhotovoltaicDevice : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a [Photovoltaic Device](https://github.com/smart-data-models/dataModel.Energy/PhotovoltaicDevice/doc/spec.md) which captured this observation, if the entity is used.
		- type: "string"
			- format: "URL"
	- refPointOfInterest : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a [PointOfInterest](https://github.com/smart-data-models/dataModel.PointOfInterest/blob/master/PointOfInterest/doc/spec.md) linked with the Repository.  
		- type: "string"
			- format: "URL"

	### Information about the measurements
	
	- temperature :   
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: >  Temperature recorded at the time of Observation compared to the  nominal reference temperature of the device. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **CEL** represents Degree Celsius.
		- type: "Number"			
	- dateEnergyMeteringStarted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > The starting date for metering energy in an ISO8601 UTC format.
		- type: "string"
			- format: "date-time"
	- nominalPeakPowerGeneration :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"			
		- description: > nominalPeakPowerGeneration is a number. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **KWT** represents Kilowatt.
		- type: "Number"
	- activePower : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"	
		- description: > Active Power,where “φ” is the phase shift of the current compared to the voltage. The unit code (text) is given using the UN/CEFACT_Common_Codes (max 3 characters). For instance, For instance, **KWT** represents Kilowatt.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
			- measurementType : 
				- x-ngsi:.
					- type: "Property" 
					- model: "http://schema.org/Text"
				- description :> How the measurement was made.
				- type: "string"
			- measurementInterval :   
				- x-ngsi:
					- type: "Property"
					- model: "https://schema.org/DateTime"
				- description: > Date and time of this observation represented by an ISO8601 UTC format. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"
			- temperature :   
				- x-ngsi:
					- type: "Property"
					- model: "https://schema.org/Number"
				- description: >  Temperature recorded at the time of Observation. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **CEL** represents Degree Celsius.
				- type: "Number"				
	- reactivePower : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"	
		- description: >Reactive Power used by circuits. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **K5** represents kilovolt-ampere-reactive.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
			- measurementType : 
				- x-ngsi:.
					- type: "Property" 
					- model: "http://schema.org/Text"
				- description :> How the measurement was made.
				- type: "string"
			- measurementInterval :   
				- x-ngsi:
					- type: "Property"
					- model: "https://schema.org/DateTime"
				- description: > Date and time of this observation represented by an ISO8601 UTC format. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"
			- temperature :   
				- x-ngsi:
					- type: "Property"
					- model: "https://schema.org/Number"
				- description: >  Temperature recorded at the time of Observation. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **CEL** represents Degree Celsius.
				- type: "Number"				
	- Current : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"	
		- description: > Current. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **AMP** represents Ampere..
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
			- measurementType : 
				- x-ngsi:.
					- type: "Property" 
					- model: "http://schema.org/Text"
				- description :> How the measurement was made.
				- type: "string"
			- measurementInterval :   
				- x-ngsi:
					- type: "Property"
					- model: "https://schema.org/DateTime"
				- description: > Date and time of this observation represented by an ISO8601 UTC format. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"
			- temperature :   
				- x-ngsi:
					- type: "Property"
					- model: "https://schema.org/Number"
				- description: >  Temperature recorded at the time of Observation. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **CEL** represents Degree Celsius.
				- type: "Number"			

	### Information about Status of the inverter 
	
	- inverterStatus: 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/String"	
		- description: > Status of the inverter. A combination of :
		- "type": "array",
			- "items": {
			- "type": "string",
				- "enum":
					- 00 - On sector
					- 01 - Power failure / On battery
					- 02 - Loss of communication
					- 03 - Battery fault
					- 04 - System shutdown
					- 05 - Tension dip
					- 06 - Overvoltage
					- 07 - Voltage drop
					- 08 - Voltage increase
					- 09 - Line noise
					- 10 - Frequency variation
					- 11 - Transient distortion
					- 12 - Harmonic distortion		  
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
					- format: "date-time"
			- measurementType : 
				- x-ngsi:.
					- type: "Property" 
					- model: "http://schema.org/Text"
				- description :> How the measurement was made.
				- type: "string"
			- measurementInterval :   
				- x-ngsi:.
					- type: "Property" 
					- model: "https://schema.org/Number"
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "number"