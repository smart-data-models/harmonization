# Rain Fall Radar Observation

- required:
	- location
	- dateObserved
	- rainFallradarContent
- type: "object"
	- allOf:
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description

The Data Model is intended to measure the water slides on a predefined area by a set of 4 Location represented by a Geo property format. The content is provided by setting up a URL link to upload a file.

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
		- value: "RainFallRadarObserved"
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
		- description: > Reference to a [Device](https://github.com/smart-data-models/dataModel.Device/blob/master/Device/doc/spec.md) which captured this observation..  
		- type: "string"
		- format: "URL"
	- refPointOfInterest : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a [PointOfInterest](https://github.com/smart-data-models/dataModel.PointOfInterest/blob/master/PointOfInterest/doc/spec.md) linked with the observation.  
		- type: "string"
		- format: "URL"

	### Information related to the measures 

	- rainFallradarContent : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/URL"
		- description: >  Path and filename which provided the information observed.
		- type: "string"
	- numberOfRow : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Number of Rows allowing the reading of the `rainFallradarContent` attribute.
		- type: "number"
	- numberOfCol : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Number of Cols allowing the reading of the `rainFallradarContent` attribute.
		- type: "number"
	- cellsSize : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Size of each cell constituting the radar. The unit code (text) of measurement is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **MTR** represents **Meters**.
		- type: "number"		
	- mapScale : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Map Scale. Relationship between the length of the cellSize and its representation on the map. 
		- type: "string"
	- measuredArea:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- type: "number"
		- minimum: 0
		- description: > Reference of the surface measured. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). FOR instance, **MTK** represents Square Meters.		