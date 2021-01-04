# **Station Description (Bus, Subway, Tram, ...)**

- required: "object"
	- location
	- dateObserved
	- dateLastReported
	- routeType
	- locationType
- type: "object"
	- allOf:
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description

The data model is a general description of urban stations (Subway, Bus, Tram, Heliport, ...) according to the GFTS standard https://developers.google.com/transit/gtfs/reference/#stopstxt, as well the detailed description of these (means of access, platform, assistance, ...).

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
		- value: "Station"
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
		- description: > Name given to the station or platform.
		- type: "string"
	- alternateName:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/alternateName"
		- description: > Alternative Name given to the station or platform.
		- type: "string"
	- description:
		- x-ngsi:
			- type: "Property"
			- model: "https://uri.etsi.org/ngsi-ld/description", "https://schema.org/description"
		- description: > Description of the station or platform.
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
			- type: type: "Property".
		- $ref: "https://github.com/smart-data-models/data-models/blob/master/common-schema.yaml#/Geometry"
		- description: > Location represented by a GeoJSon geometry [Point, LineString, Polygon, MultiPoint, MultiLineString, MultiPolygon]
	- address:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/address"
		- description: > Adress civic.
		- $ref: "https://github.com/smart-data-models/data-models/blob/master/common-schema.yaml#/Address"
	- areaServed:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Zone of level higher to the attributes `Location` & `Address` to gather and cross information (ex district, etc)
		- type: "string"
	    
	### Information related to the date of last reporting 

	- dateLastReported:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > A timestamp which denotes the last time when the device successfully reported data. The date and time of this observation in ISO8601 UTCformat.
		- type: "string"
			- format: "date-time"

	### Information about a reference to other Data Models .

	- refPointOfInterest : 
		- x-ngsi:
		- type: "Relationship"
		- model: "https://schema.org/URL"
	- description: > Reference to a [PointOfInterest](https://github.com/smart-data-models/dataModel.PointOfInterest/blob/master/PointOfInterest/doc/spec.md) linked with the Repository.  
	- type: "string"
		- format: "URL"
	
	### Information about the identification of the station and platform. GTFS Stantard [STOP](https://developers.google.com/transit/gtfs/reference/#stopstxt)
	
	- stationType:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > A unique value composed only of the attribut 'description' (subway, Bus, Tram, ...) from the urban transport Mode GFTS standard [STOP](https://developers.google.com/transit/gtfs/reference/#stopstxt). 
		- type: "string"
			- enum : tram, subway, rail, bus, ferry, cableTram, aerialLift, funicular, trolleybus, monorail
	- locationType : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Link to the GTFS standard repository describing the different location [Location Type]. A unique value of:
		- type: "Number"
			- enum : 
				- 0 Stop or platform (place where users get on or off in a public transport vehicle).
				- 1 Station (area or physical structure comprising one or more platforms)
				- 2 Entrance or Exit (place where users can enter / exit a station from the street).
				- 3 Generic intersection (location in a station that does'nt correspond to any other `location_type` value).
				- 4 Boarding area of a specific location on a platform where users can get on / off in a vehicle.
	- parentStation  :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/string"
		- description: > Link to the GTFS standard repository describing the different link between Station and Platform [Parent STATION].  A unique value of :
		- type: "string"
			- enum : 
				- Case 1 `location_type` = 0 (Stop / platform ), the parent_station field contains the ID of a station.
				- Case 2 `location_type` = 1  (Station), this field must be empty.
				- Case 3 `location_type` = 2 (Input / output) or `location_type` = 3 (generic intersection), the parent_station field contains the ID of a station `location_type` = 1.
				- Case 4 `location_type` = 4 (boarding area), the parent_station field contains the ID of a platform..
	- levelId:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Floor on which the location is located. Numerical index associated with the floor. Indicates the relative position of this stage in relation to the others. The index 0 indicates the ground floor. The floors above ground level are indicated by positive indices, and the underground stages by negative indices..
		- type: "Number"
	- platformCode:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Platform identifier for a platform type stop `location_type` = 0 when the stop is in a station.
		- type: "Number"
	- zoneId:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/string"
		- description: > Pricing zone of the station.
		- type: "string"
	- wheelChairAccessible
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Access possible for Person with Reduced Mobility. A unique value of :
		- type: "Number"
			- enum : 
				- For stops without parents
					0 no information is available regarding the accessibility of the stop.
					1 some vehicles at this stop can board a PMR user.
					2 PRM user cannot board  at this stop.
				- For a stop that is part of a station
					0 the stop inherits the wheelchair_boarding behavior of the parent station, if it is filled in.
					1 lanes provide wheelchair access to the stop / platform  from outside the station.
					2 no lane provides wheelchair access to the stop / platform from outside the station.
				- For station inputs / outputs
					0 the station entry inherits the wheelchair_boarding behavior of the main station, if specified.
					1 the station entrance is wheelchair accessible.
					2 no wheelchair accessible route connects the station entrance to the stops / platforms.
	
	### Information about the Opening Hours specification for `locationType` = 0 or 1.

	- openingHoursSpecification : 
		- x-ngsi:
			- type: "Property"
			- model: http://schema.org/openingHoursSpecification
		- description: > General Opening hours specification. 
		- type: "string"
	
	### Information related to the owner and contracting company for `locationType` = 1
	
	- owner:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text" included references to "http://schema.org/Person", "https://schema.org/Organization", "https://schema.org/URL".
		- description: > The owners of the station. A list of [Text], [Person], [Organisation] or [URLs].
		- type: "array"
			- items:
				- type: string
	- contractingAuthority : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Name of the contracting authority. 
		- type: "string"

	### Information related to the manager by delegation and contact point for `locationType` = 1

	- contractingCompany : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Name of the contracting company responsible for the exploitation of the station.
		- type: "string"	
	- contactPoint:
		- x-ngsi:
			- type: "Property"
			- model: [Contact Point](https://schema.org/ContactPoint)
		- description: > Contact point for the station manager of the contracting company.
		- type: "string"
	- webSite:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Link to the official website for more information..
		- type: "string"    
	
	### Information about Mechanical Data depending the value of `locationType` attribut 
	
	- instalationMode:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Location  relative to the ground reference. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- ground, underGround, underSea, aerial, 
	- dimension : 
		- x-ngsi:
	   		- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Global dimension. The format is structured by a sub-property of 3 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **MTR** represents Meters.
		- type: "number"
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- items:
				- length
				- height
				- width
	- inventory : 
		- x-ngsi:
	   		- type: "Property"
			- model: [StructuredValue](http://schema.org/StructuredValue)
		- description: > General data mapping only for `locationType` = 0, 1, 3, 4. The format is structured by a sub-property of 4 items.
		- type: "String"
			- items:
				- nbOfIOPoint
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Number",
					- description: > Number of entry / exit Points.
					- type: "number"
				- nbOfLane
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Number",
					- description: > Number of traffic lanes.
					- type: "number"
				- nbOfPlatform
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Number",
					- description: > Number of platform.
					- type: "number"
				- PlatformType
					- x-ngsi:
					- type: "Property"
						- model: "https://schema.org/Text",
					- description: > Type of platform. A combination of :
					- type: "array"
						- items:
						- type: string
							- enum :  
								- lateral, central
	
	### Information related to the connexion with other transport type from the station or platform for `locationType` = 0 or 1. 
	
	- stationConnected:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/StructuredValue"
		- description: > Connections possible from this station. A structured value from 0 to N occurrences where each items is a string in the format `stationType` : [List of Lines connected, separated by a comma]
		- type: "array"
			- items : 
				- stationType : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > Station or plateform connected. A value composed only of the attribut 'description' (subway, Bus, Tram, ...) from the urban transport Mode GFTS standard [STOP](https://developers.google.com/transit/gtfs/reference/#stopstxt). 
					- type: "string"
						- enum : tram, subway, rail, bus, ferry, cableTram, aerialLift, funicular, trolleybus, monorail
				- linesConnected: 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > Line connected. Free text or geographic properties or reference to an entity that describes the lines of the different types of transport. 
					- type: "array"
						- type: "string"	
	
	### Information about Services or assistance provided by the station or platform for `locationType` = 0 or 1. 
	
	- services : 
		- x-ngsi:
	   		- type: "Property"
			- model: [StructuredValue](http://schema.org/StructuredValue),
		- description: > General information on the services and assistance provided by the station. The format is structured by several sub-properties. All Sub properties are Boolean attributs. 
		- type: "array"
			- items : 
				- purchaseDevice
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Interactive ticket purchase kiosks.
					- type: "Boolean"
				- interactiveDevice 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Interactive passenger information terminals (BIV).
					- type: "Boolean"
				- timetableDevice
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Dynamic timetable display system.
					- type: "Boolean"
				- voiceDevice
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Sound system for passenger information.
					- type: "Boolean"
				- informationBoardDevice
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Static passenger information table.
					- type: "Boolean"
				- messageDevice 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Dynamic message display system.
					- type: "Boolean"
				- shelters
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Covered shelters.
					- type: "Boolean"
				- restBench
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Rest bench.
					- type: "Boolean"
				- emergencyPhone
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Emergency telephone.
					- type: "Boolean"					
				- videoSurveillance
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Video surveillance camera.
					- type: "Boolean"
				- defibrillator
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > defibrillator.
					- type: "Boolean"
				- wheelChairAccessible
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/booelean",
					- description: > Access possible for Person with Reduced Mobility.
					- type: "Boolean"
					
	### Information related to the means of payment for services provided by the station for `locationType` = 0 or 1
	
	- paymentAccepted:
		- x-ngsi:
			- type: "Property"
			- model: [Payment Accepted](https://schema.org/paymentAccepted)
		- description: > Accepted payment. A combination of a list of active codes defined in the model :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- Cash, CreditCard, CryptoCurrency, other 
	- currencyAccepted:
		- x-ngsi:
			- type: "Property"
			- model: [Currencies Accepted](https://schema.org/currenciesAccepted), [Norme ISO 4217](http://en.wikipedia.org/wiki/ISO_4217), [Crypto Currencies](https://en.wikipedia.org/wiki/List_of_cryptocurrencies) , [Exchange Trading System](https://en.wikipedia.org/wiki/Local_exchange_trading_system)
		- description: > Currency accepted for payment. A combination of a list of active codes defined in the model :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- EUR, USD, GBP, CHF, Bitcoin, Neo, ...
	
	### Information about general information about lifecycle for `locationType` = 0 or 1 
	
	- constructionDate:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > Date of station construction in ISO8601 UTCformat..
		- type: "string"
			- format: "date-time"
	- commissioningDate:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > Date of station commissioning in ISO8601 UTCformat.
		- type: "string"
			- format: "date-time"
	- architecte : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Architect of the station. 
		- type: "string"
	- featuredArtist  : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Name of the featured Artist(ss) who decorated the station (Work / Sculpture / Painting / ..) or having a work within the station. 
		- type: "array"
			- items:
				- type: string