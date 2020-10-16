# Electro Magnetic Observed

- required:
	- location
	- dateObserved
	- eMF
- type: "object"
	- allOf:
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description

The Data Model  is intended to measure excessive electric and magnetic fields (EMFs), radiation in a work or public environment according to the level of exposure to electromagnetic fields in the air (`inside` or `outside`).
For the attributes `eMF`, there are various ways they can be actually measured. For this purpose the `measurementType` Meta Data Attribute can be used. It can have the following values:
	- Instant.	From the specific instant of time
	- average.	The average of a time period
	- maximum.	The maximum of a time period
	- minimum.	The minimum of a time period.

When using the [average, minimum, maximum] values another Meta Data attribute called `measurementInterval` should be used to give the length of the measurement period in Seconds. 
Also the `timestamp` Meta Data attribute should be the end time of the measurement period.

The frequency of the hertzian waves is conventionally lower than 300 GHz, propagating in space without artificial guide. They are between 9 kHz and 300 GHz.

The following attributes are used to qualify the measurements and must be part of the description of the [device] as a configuration element.
	- FrequencyBands 	Range of limits for the frequency.
						- Lower  : Unit Code Mega Hertz (MHz) 
						- Higher : Unit Code Giga Hertz (A86)
	- detectionLimits	Range of limits for the detection limits.
						- Lower  : Unit Code Volt Per Meter (D50) 
						- Higher : Unit Code Volt Per Meter (D50)
	- Installation		How the device is installed
						- C1: Positioning of the device in relation to a ground reference system.
							- Value = Ground, Wall, Pole, aerial, roofing, other
						- C2: Positioning of the device in relation to an external / internal reference 
							- Value = Inside / Outside

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
		- value: "ElectroMagneticObserved"
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

	### Information related to a reference to another DataModel

	- refDevice : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a [Device](https://github.com/smart-data-models/dataModel.Device/blob/master/Device/doc/spec.md) which captured this observation.
		- type: "string"
			- format: "URL"
	- refPointOfInterest : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a [Point Of Interest](https://github.com/smart-data-models/dataModel.PointOfInterest/blob/master/PointOfInterest/doc/spec.md) linked with the observation.  
		- type: "string"
			- format: "URL"  

	### Information related to the measures 

	- eMF : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/Number"
		- description: > Level corresponding to the observed survey. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **MHz** represents Mega Hertz.
			- type: [Number](http://schema.org/Number) 
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
				- description: > Measurement period (From 1 to 60 seconds). The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, [SEC] represents Second.
				- type: "number"
	- reliability :  
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/Number"
		- description: > Percent for confidence Factor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percent.
		- type: "number"		
