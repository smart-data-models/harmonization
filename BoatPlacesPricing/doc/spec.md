# Boat Places Pricing

- required:
	- location
	- dateLastReported
	- refSeaPort
	- spotCategoryRange
	- validFrom
	- validThrough
- type: "object"
	- allOf:
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description

The purpose of the data model is to provide information on the pricing of mooring rings by category (length / Width). The information received relates only to pleasure boats and excludes commercial and passenger transport boats.  
The information on the Spot categories for boats is taken from the ISO 8666 standard.

*Method to design your repository of Boat Pricing*
To describe the different pricing by category (A to Z17) in the section *Information about pricing*, the use of a list is necessary when writing the record.
Depending on the port configuration, a record will be created by `spotCategoryRange` to determine the pricing for a period as repository. 
	Two scenario are possible
	**Scenario 1** : Definition of the length range on a single category .
			`spotCategoryRange`	= ["F"], 
				Boats accepted : length 7.00 to 7.49 and max width =< 2.70.
					**"F"**  length 7.00 to 7.49 / max width =< 2.70
	**Scenario 2** : Definition of the length range with consecutive categories. 
			`spotCategoryRange`	= ["F", "G"],	
				Boats accepted : length 7.00 to 7.99 and max width =< 2.80.
					**"F"** gives maxLength from 7.00 to 7.49 and maxWidth 2.70
					**"G"** gives maxLength from 7.50 to 7.99 and maxWidth 2.80

*Additional Information about this Data Model*
It can be used with the following data Model.
	- **SeaPort** to provide information to the port about authorized Boat in the port.

This Data Model is complementary to the Data Model **BoatPlacesAvailable**.

**Data repository (ISO 8666 standard)**
*Categorie Length Max 	Width Max* 
	A		  4.99		 2.00
	B		  5.49		 2.15
	C		  5.99		 2.30
	D		  6.49		 2.45
	E		  6.99		 2.60
	F		  7.49		 2.80
	G		  7.99		 2.80
	H		  8.49		 2.95
	I		  8.99		 3.10
	J		  9.49		 3.25
	K		  9.99		 3.40
	L		 10.49		 3.55
	M		 10.99		 3.70
	N		 11.49		 3.85
	O		 11.99		 4.00
	P		 12.99		 4.30
	Q		 13.99		 4.60
	R		 15.99		 4.90
	S		 17.99		 5.20
	T1		 20.99		 5.60
	T2		 23.99		 6.00
	U		 28.99		 7.00
	V		 33.99		 8.00
	W		 38.99		 9.00
	X		 43.99		10.00
	Y		 48.99		11.00
	Z		 53.99		12.00
	Z01		 58.99		13.00
	Z02		 64.99		14.00
	Z03		 71.99		15.00
	Z04		 78.99		16.00
	Z05		 85.99		17.00
	Z06		 92.99		18.00
	Z07		 99.99		19.00
	Z08		106.99		20.00
	Z09		113.99		21.00
	Z10		120.99		22.00
	Z11		127.99		23.00
	Z12		134.99		24.00
	Z13		142.99		25.00
	Z14		150.99		26.00
	Z15		158.99		27.00
	Z16		166.99		28.00
	Z17		174.99		29.00 
				
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
		- value: "BoatPlacePricing"

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

	- areaServed:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Zone of level higher to the attributes Location & Address to gather and cross information (ex district, etc)
		- type: "string"

	### Information related to the date of last reporting in case of ENTITY Device

	- dateLastReported:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > A timestamp which denotes the last time when the device successfully reported data. The date and time of this observation in ISO8601 UTCformat.
		- type: "string"
		- format: "date-time"

	### Information about a reference to other Data Models or to SeaPort reference.

	- refSeaPort : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to the entity [Seaport](https://github.com/smart-data-models/dataModel.Port/blob/master/Seaport/doc/spec.md) to use as main link.  
		- type: "string"
			- format: "URL"
	- refPointOfInterest : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a [PointOfInterest](https://github.com/smart-data-models/dataModel.PointOfInterest/blob/master/PointOfInterest/doc/spec.md) linked with the Repository.  
		- type: "string"
			- format: "URL"

	### Information about range of Category 
	
	- spotCategoryRange:
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > List from the lowest to the highest categories: A combination of : 
		- type: "array"
			- items:
				- type: string
					- enum : 
						- A, B, C, D, E, F, G, H, I, J, K, L, M, N, O, P, Q, R, S, T1, T2, U, V, W, X, Y, Z, Z01, Z02, Z03, Z04, Z05, Z06 , Z07, Z08, Z08, Z09, Z10, Z11, Z12, Z13, Z14, Z15, Z16, Z17
	- minLength:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Minimum length allowed to access the spot. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"
	- maxLength:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum length allowed to access the spot. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"
	- maxWidth:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum width allowed to access the spot. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"
	- maxDraft:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum draft allowed to access the spot. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"

	### Information about the pricing according the categories

	- validFrom:
		- x-ngsi:
		- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > Start date and time of the pricing rules.
		- type: "string"
			- format: "date-time"	
	- validThrough:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > End date and time of the pricing rules.
		- type: "string"
			- format: "date-time"
	- period :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Type of period defined the date From and Through  : A free text or a unique value of the different combination allowed "season / offSeason" - "summer / winter" - "low / medium / high"
		- type: string
	- passage :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/StructuredValue"	
		- description: > Ticket price of the place for passing boats for this category / period. A structured value with 3 subproperties where each items is a string in the format `key` : `price` in Euro €
		- type: "object"
			- items : 
				- day 
				- week
				- month
	- resident :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/StructuredValue"	
		- description: > Ticket price of the place for resident boats for this category / period. A structured value with 2 subproperties where each items is a string in the format `key` : `price` in Euro €
		- type: "object"
			- items : 
				- month
				- annual
	- wintering :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/StructuredValue"	
		- description: > Ticket price of the place for wintering boats for this category / period. A structured value with 3 subproperties where each items is a string in the format `key` : `price` in Euro €
		- type: "object"
			- items : 
				- day 
				- week
				- month
	- fairing :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/StructuredValue"	
		- description: > Ticket price of the place for fairing boats for this category / period. A structured value with 3 subproperties where each items is a string in the format `key` : `price` in Euro €
		- type: "object"
			- items : 
				- day 
				- week
				- month