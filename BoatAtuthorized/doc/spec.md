# Boat Authorized in the harbor 

- required:
	- location
	- dateObserved
	- refSeapPort
- type: "object"
	- allOf:
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description

The data model is intended to provide information on the boats authorized to operate within the port.
This repository is created by type of boat (pleasure craft, trade, passengers, ...). For each type, a list of optional subtypes can be associated. 

*Method to design your repository of Boat Authorized*
	Create a record for each `boatType` authorized to circulate in the harbor with all corresponding `BoatSubType`.
	- *record 1*
		- "id": "BoatAuthorized:MNCA-NCE-BA-001-yatching"
		- `refSeapPortName`: "MyPort"
		- `boatType`: "yatching"
		- `boatSubType`: ["zodiac", "monoHull", "catamaran", "yacht", "sailboat", "jetSki"]
	- *record 2*
		- "id": "BoatAuthorized:MNCA-NCE-BA-001-passenger"
		- `refSeapPortName`: "MyPort"
		- `boatType`: "passenger"
		- `boatSubType`: ["cruise", "ferrie"]
	- *record 3*
		- "id": "BoatAuthorized:MNCA-NCE-BA-001-passenger"
		- `refSeapPortName`: "MyPort"
		- `boatType`: "passenger"
		- `boatSubType`: ["factoryShip", "seiner","artisanVessels","trawler"]
		
*Rules about the date - section Information about the date and period of authorization*
There are several scenarios possibles :
	- **Case 1** Definition of a range starting on a specific date and ending without date binding.
					Allows to define a permanent authorization for example
					`dateObserved`, 	"2020-01-01T00:00:01Z" 
					`dateObservedFrom`	"2020-01-01T00:00:01Z"
					`dateObservedTo`	""
	- **Case 2** Definition of a range starting on a specific date and ending date.
					Allows to define a specific authorization for example for a boatshow or for a type of boat.
					`dateObserved`, 	"2020-10-10T00:00:01Z:2020-10-14T23:59:59Z" 
					`dateObservedFrom`	"2020-10-10T00:00:01Z"
					`dateObservedTo`	"2020-10-14T23:59:59Z"

*Additional Information about this Data Model*
It can be used with the following data Model.
	- **SeaPort** to provide information to the port about authorized Boat in the port.
	
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
		- value: "BoatAuthorized"

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
		- description: > Name given to the Repository. 
		- type: "string"
	- alternateName:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/alternateName"
		- description: > Alternative Name given to the Repository
		- type: "string"
	- description:
		- x-ngsi:
			- type: "Property"
			- model: "https://uri.etsi.org/ngsi-ld/description", "https://schema.org/description"
		- description: > Description of the Repository.
		- $ref: 'https://jason-fox.github.io/swagger-datamodel-test/common.yaml#/Description'
	- seeAlso:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text", "https://schema.org/URL"
		- description: > Text or Link that can provide additional information.
		- type: "string"

	### Information about AreaServed.

	- areaServed:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Zone of level higher to the attributes Location & Address to gather and cross information (ex district, etc)
		- type: "string"

	### Information about the date and period of authorization. 

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

	### Information about a reference to other Data Models or to SeaPort reference.

	- refSeaPort : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to the entity [Seaport](https://github.com/smart-data-models/dataModel.Port/blob/master/SeaPort/doc/spec.md) to use as main link.  
		- type: "string"
			- format: "URL"
	- refPointOfInterest : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a [PointOfInterest](https://github.com/smart-data-models/dataModel.PointOfInterest/blob/master/PointOfInterest/doc/spec.md) linked with the Repository.  
		- type: "string"
			- format: "URL"

	### Information detailing Boat Type

	- boatType:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"			
		- description: > Type of Boat. A unqiue value of : 
		- type: string
			- enum : 
				- yatching, cargo, passenger, specialist, Tanker, fishing, war, historic 
	- boatSubType:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"			
		- description: > Sub Type for a boatType. A combination of : 
		- type: "array"
			- items:
				- type: string
					- enum : 
						- *yatching* : canoe, zodiac, monoHull, catamaran, trimaran, yacht, gondola, sailboat, houseBoat, jetSki 
						- *cargo* : bargeCarrier, containerCarrier, cargoCarrier, bulkCarrier, lngCarrier, lpgCarrier, butanerCarrier, timberCarrier, livestockCarrier, referCarrier, roroCarrier
						- *tankers* : CrudeCarrier, ProductCarrier, LiquefiedGasCarrier, ChemicalCarrier, tankers
						- *passenger* : cruise, ferrie, highSpeedVessel, CoastalFerrie, barge, bac, liner, harbourFerrie
						- *specialist* : pipeLayer, cableLayer, supplyShip, craneBarge, drillRig, productionPlatform, floatingStorageUnit, floatingProductionStorageUnit, researchVessel, salvageOperation, lightShip, anchorHandlingVessel, divingVessel, iceBreakerShip, dredger, buoyTenderBoat, mooringBoat, lifeBoat, flagshipBoat, fireBoat, pilotBoat, tugBoat, oceanographicBoats
						- *fishing* : factoryShip, trawler, seiner, longLiner, drifter, lineVessel, multipurposeVessel, fisheriesResearchVessel, artisanVessels
						- *war* : frigate, corvette, destroyer, cruiser, amphibiousAssaultShip, aircraftCarrier, helicopterCarrier, littoralCombatShip, mineSweeping, submarineAttack, submarineBallisticMissile, submarineCruiseMissile, speedBoat, hovercraft, tankers 
						- *historic* : canoe, galleon, caravel, carrack, cog, dhow, djong, fluyt, koch, pinisi, saillingShip, clipper, gabare, viking, paddleSteamer, galley, junks  other

	### Information about the Opening Hours specification for boat authorized.

	- openingHoursSpecification : 
		- x-ngsi:
			- type: "Property"
			- model: http://schema.org/openingHoursSpecification
		- description: > General Opening hours specification. 
		- type: "Object"

	### Information detailing port constraints for the Type of boat. 
					
	- maxTonnage:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum tonnage authorized to access the harbor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **TNE** represents Tonne Metric.
		- type: "number"
	- minLength:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Minimum length allowed to access the harbor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"
	- maxLength:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum length allowed to access the harbor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"
	- maxWidth:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum width allowed to access the harbor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"
	- maxDraft:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum draft allowed to access the harbor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"