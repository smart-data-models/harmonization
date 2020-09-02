# AC Measurement
- required:
	- location
	- dateObserved
	- phaseType
- type: "object"
	- allOf:
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description

The Data Model intended to measure the electrical energies consumed by an electrical system which uses an Alternating Current (AC) for a three-phase (L1, L2, L3) or single-phase (L) and neutral (N). 
It integrates the initial version of the data Modem [THREEPHASEMEASUREMENT], extended to also perform single-phase measurements. 
it includes attributes for various electrical measurements such as power, frequency, current and voltage. 

*Additional Information about Attributes :*
For some attributes such as current and voltage the value is a structured value with properties for the Single-Phase (L) or three different phases (L1, L2 and L3). 
For some measurements such as the different power types (active, reactive and apparent power) there is an attribute for the total from all phases. The rules are defined as below :
	- Three Phase 	- Total = L1 + L2 + L3
	- Single Phase 	- Total = L.

For most of the attributes, there are various ways they can be actually measured. For this purpose the `measurementType` Meta Data Attribute can be used. It can have the following values:

When using the values [average, rms, minimum, maximum], another metadata attribute called `measurementInterval` should be used to give the length of the measurement period in seconds. 
Also the Meta Data `timestamp`  attribute should be the end time of the measurement period.

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
			- model: "https://schema.org/Text"
		- Description: "Entity type, mandatory element for NGSI"
		- type : "string"
		- value: "ACMeasurement"
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
	    
	### Information about the date and period.

	- dateObserved:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > Date and time of this observation represented by an ISO8601 UTC format. It can be represented by an specific time instant or by an ISO8601 interval to separate attributes `dateObservedFrom`,`dateObservedTo`.
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

	- refDevice : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a [Device](https://github.com/smart-data-models/dataModel.Device/blob/master/Device/doc/spec.md) which captured this observation.   
		- type: "string"
		- format: "URL"

	- refTargetDevice : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a list of the [Device(s)](https://github.com/smart-data-models/dataModel.Device/blob/master/Device/doc/spec.md) for which the measurement was taken.  
		- type: "string"
		- format: "URL"

	### Section 1 : Various Electrical parameters.

	- phaseType : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Type of Phase. A unique value of :
		- type: "string"
		- enum : 
			- singlePhase, threePhase
		
	- frequency : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > The frequency of the circuit. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **HTZ** represents Hertz.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- type: "string"
				- format: "date-time"
				- description: > Time stamp when the last update of the attribute happened.
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
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, `SEC` represents Second.
				- type: "Number"
		
	- dateEnergyMeteringStarted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > The starting date for metering energy in an ISO8601 UTC format.
		- type: "string"
			- format: "date-time"

	### Section 2 : Energy.

	### *Section 2.1 : Individual values*

	**Note : For each attribute, the actual values will be conveyed by 1 or 3 sub properties depending type of phase. The names will be equal to the name of each of the alternating current phases :**
		**- Single-Phase : Individual values : L.**
		**- ThreePhase  : Sum of the individual values : L1, L2, L3.**
	**All values are calculated from the start date of the measurement [dateEnergyMeteringStarted]**
	
	- activeEnergyImport :  
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Active energy imported i.e. consumed per phase. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kWh** represents kilowatt hour.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
			- x-ngsi:
				- type: "Property" 
				- model: "https://schema.org/DateTime" 
			- description: > Time stamp when the last update of the attribute happened.
			- type: "string"
			- format: "date-time"
	- reactiveEnergyImport :  
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Fundamental frequency reactive energy imported i.e. consumed per phase. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kVArh** represents kilovolt-ampere-reactive-hour.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
	- apparentEnergyImport : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Apparent energy imported i.e. consumed per phase. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kVAh** represents kilovolt-ampere-hour.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
	- activeEnergyExport : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Active energy exported per phase. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kWh** represents kilowatt hour.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
	- reactiveEnergyExport : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Fundamental frequency reactive energy exported per phase. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kVArh** represents kilovolt-ampere-reactive-hour.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
	- apparentEnergyExport : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Apparent energy exported per phase. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kVAh** represents kilovolt-ampere-hour.
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
	
	### *Section 2.2 : Total values.*

	**Note : The values will be conveyed by 1 or 3 sub properties depending The Type of Phase for each phase :**
		**- Single-Phase  : Individual values : L.**
		**- ThreePhase	: Sum of the individual values : L1, L2, L3.**
	**All values are calculated from the start date of the measurement [dateEnergyMeteringStarted]**

- totalActiveEnergyImport : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Total energy imported i.e. consumed. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kWh** represents kilowatt hour.
  - type: "Number"
 		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
	- totalReactiveEnergyImport : 
		- x-ngsi:
			- type: "Property"
	   		- model: "https://schema.org/Number"
	   	- description: > Total energy imported i.e. consumed (with regards to fundamental frequency reactive power). The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kVArh** represents kilovolt-ampere-reactive-hour.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
	- totalApparentEnergyImport : 
		- x-ngsi:
			- type: "Property"
	   		- model: "https://schema.org/Number"
	   	- description: > Total energy imported i.e. consumed (with regards to apparent power). The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kVAh** represents kilovolt-ampere-hour.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"  
	- totalActiveEnergyExport : 
		- x-ngsi:
			- type: "Property"
	   		- model: "https://schema.org/Number"
	   	- description: > Total energy exported. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kWh** represents kilowatt hour.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
	- totalReactiveEnergyExport : 
		- x-ngsi:
			- type: "Property"
	   		- model: "https://schema.org/Number"
	   	- description: > Total fundamental frequency reactive energy exported. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kVArh** represents kilovolt-ampere-reactive-hour.
		- type: "Number"
	
 		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"
	- totalApparentEnergyExport : 
		- x-ngsi:
			- type: "Property"
	   		- model: "https://schema.org/Number"
	   	- description: > Total energy exported (with regards to apparent power). The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **kVAh** represents kilovolt-ampere-hour.
		- type: "Number"
		- Attribute metadata:
			- timestamp: 
				- x-ngsi:
					- type: "Property" 
					- model: "https://schema.org/DateTime" 
				- description: > Time stamp when the last update of the attribute happened.
				- type: "string"
				- format: "date-time"

	### Section 3 : Power.

	### *Section 3.1 : Individual values.*

	**Note : The actual values will be conveyed by 1 or 3 sub properties depending the Type of Phase. The names will be equal to the name of each of the alternating current phases :**
		**- Single-Phase  : Individual values : L.**
		**- ThreePhase	: Sum of the individual values : L1, L2, L3.**

	- activePower :  
		- x-ngsi:
			- type: "Property"
	   		- model: "http://schema.org/StructuredValue"
		- description: >  Active power consumed per phase. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **WTT** represents Watt.
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
				- x-ngsi:.
					- type: "Property" 
					- model: "https://schema.org/Number"
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"
	- reactivePower :  
		- x-ngsi:
			- type: "Property"
	   		- model: "http://schema.org/StructuredValue"
		- description: >  Fundamental frequency reactive power. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VAr** **K5** represents volts-ampere-reactive.
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
				- x-ngsi:.
					- type: "Property" 
					- model: "https://schema.org/Number"
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"
	- apparentPower : 
	
 		- x-ngsi:
			- type: "Property"
	   		- model: "http://schema.org/StructuredValue"
		- description: > Apparent power consumed per phase. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VA** represents volt-ampere.
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
				- x-ngsi:.
					- type: "Property" 
					- model: "https://schema.org/Number"
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"

	### *Section 3.2 : Total values.*

	**Note : counting all phases.**
		**- Single-Phase : L.**
		**- ThreePhase   : L1, L2, L3.**

	- totalActivePower : 
		- x-ngsi:
			- type: "Property"
	   		- model: "https://schema.org/Number"
	   	- description: > Total Active Power consumed. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **W** represents watt.
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
				- x-ngsi:.
					- type: "Property" 
					- model: "https://schema.org/Number"
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"
	- totalReactivePower : 
		- x-ngsi:
			- type: "Property"
	   		- model: "https://schema.org/Number"
	   	- description: > Total Reactive Power consumed. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VAr** represents volt-ampere-reactive.
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
				- x-ngsi:.
					- type: "Property" 
					- model: "https://schema.org/Number"
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"
	- totalApparentPower : 
		- x-ngsi:
			- type: "Property"
	   		- model: "https://schema.org/Number"
	   	- description: > Total Apparent Power consumed. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VA** represents Volt-ampere.
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
				- x-ngsi:.
					- type: "Property" 
					- model: "https://schema.org/Number"
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"

	### Section 4 : Power Factor.

	### *Section 4.1 : Individual values.*

	**Note : The actual values will be conveyed by one subproperty per alternating current phase:**
		**- Single-Phase : L.**
		**- ThreePhase   : L1, L2, L3.**

	- powerFactor :  
		- x-ngsi:
			- type: "Property"
	   		- model: "http://schema.org/StructuredValue"
		- description: > Power factor for each phase.
		- type: "Number"
			- min : -1
			- max : 1
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
				- type: "Number"
			- onlyPositive : 
				- x-ngsi:.
					- type: "Property" 
					- Type: [Boolean](https://schema.org/Boolean)
				- description: > Is the value always greater than zero or can it also be negative. If not present this is assumed to be false.
				- type: "Booelean"
	- displacementPowerFactor :   
 		- x-ngsi:
			- type: "Property"
	   		- model: "http://schema.org/StructuredValue"
		- description: > Displacement power factor for each phase. The quantity is based on the fundamental frequency of the system.
	
 		- type: "Number"
			- min : -1
			- max : 1
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
				- type: "Number"
			- onlyPositive : 
				- x-ngsi:.
					- type: "Property" 
					- Type: [Boolean](https://schema.org/Boolean)
				- description: > Is the value always greater than zero or can it also be negative. If not present this is assumed to be false.
				- type: "Booelean"
   
	### *Section 4.2 : Total values.*
  
	**Note : including all phases :**
		**- Single-Phase : L**
		**- ThreePhase   : L1, L2, L3.**

	- totalPowerFactor : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/Number"
		- description: > Sum of Power factor including all phases.
		- type: "Number"
			- min : -1
			- max : 1
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
				- type: "Number"
			- onlyPositive : 
				- x-ngsi:.
					- type: "Property" 
					- Type: [Boolean](https://schema.org/Boolean)
				- description: > Is the value always greater than zero or can it also be negative. If not present this is assumed to be false.
				- type: "Booelean"
	- totalDisplacementPowerFactor : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/Number"
		- description: > SSum of Displacement power factor including all phases. The quantity is based on the fundamental frequency of the system.
		- type: "Number"
			- min : -1
			- max : 1
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
				- type: "Number"
			- onlyPositive : 
				- x-ngsi:.
					- type: "Property" 
					- Type: [Boolean](https://schema.org/Boolean)
				- description: > Is the value always greater than zero or can it also be negative. If not present this is assumed to be false.
				- type: "Booelean"

	### Section 5 : Various electrical measures.

	### *Section 5.1 : Electrical Current.*

	**Note : The actual values will be conveyed by one subproperty per alternating current phase and the neutral wire:**
			**- Single-Phase : L and N.**
			**- ThreePhase   : L1, L2, L3 and N.**

	- current : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Electrical current. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **A** represents Ampers.
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
				- x-ngsi:.
					- type: "Property" 
					- model: "https://schema.org/Number"
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"

	### *Section 5.2 : Voltage.*
  
	**Note : The actual values will be conveyed by one subproperty per alternating current phase:**
		**- Single-Phase : L**
		**- ThreePhase : L1, L2, L3**
  
	- phaseVoltage :  
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > The voltage between each phase and neutral conductor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VLT** represents Volts.
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
				- x-ngsi:.
					- type: "Property" 
					- model: "https://schema.org/Number"
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
        				- type: "Number"
	- thdVoltage :  
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Total harmonic distortion of voltage for each phase.
		- type: "Number"
			- min : -1
			- max : 1
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
				- type: "Number"
	- thdCurrent :  
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Total harmonic distortion of electrical current.
		- type: "Number"
			- min : -1
			- max : 1
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
				- type: "Number"

	### *Section 5.3 : Voltage between phases.*
  
	**Note : A value for each phase pair:**
			**- phases 1 and 2 (L12)**
			**- phases 2 and 3 (L32)** 
			**- phases 3 and 1 (L31)**

	- phaseToPhaseVoltage :
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: >  Voltage between phases. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VLT** represents Volts.
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
				- x-ngsi:.
					- type: "Property" 
					- model: "https://schema.org/Number"
				- description: > Measurement period (seconds) . The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "Number"
